# 03 - Sequence-Aware Techniques

## Overview

This document covers modern techniques designed to handle sequential data while producing useful embeddings for customer profiling.

---

## 1. Item2Vec / Prod2Vec

### Core Idea
Treat customer sessions as "sentences" and products as "words", then apply Word2Vec (Skip-gram or CBOW).

### How It Works

```python
# Customer sessions become "sentences"
sessions = [
    ["product_a", "product_b", "product_a", "product_c"],  # Customer 1, Session 1
    ["product_x", "product_y"],                            # Customer 2, Session 1
    ["product_a", "product_d", "product_e"],               # Customer 1, Session 2
]

# Skip-gram objective: predict context from target
# For "product_a" with context window=2:
#   Predict: product_b, product_a, product_c from product_a
```

### Extension: Action-Item Pairs
Instead of just products, encode action-item pairs:

```python
# Original sequence
sequence = [
    {"action": "view", "product": "a"},
    {"action": "cart", "product": "a"},
    {"action": "remove", "product": "a"},
    {"action": "cart", "product": "d"},
]

# Tokenized as action-item pairs
tokens = ["view_a", "cart_a", "remove_a", "cart_d"]
```

### Strengths
| Strength | Description |
|----------|-------------|
| **Local sequence awareness** | Context window captures nearby co-occurrence |
| **Scalable** | O(n) training, works on millions of sequences |
| **Interpretable** | Similar items cluster; can inspect nearest neighbors |
| **Proven** | Production-validated at Spotify, Airbnb, Alibaba |

### Weaknesses
| Weakness | Description |
|----------|-------------|
| **Fixed context window** | Typically 5-10 items; misses long-range patterns |
| **Symmetric context** | Skip-gram doesn't distinguish "before" vs "after" |
| **No explicit temporal modeling** | Time gaps between events ignored |
| **Action-item vocabulary explosion** | `n_actions × n_items` tokens |

### Best For
- Cold-start fallback
- Interpretability requirements
- Resource-constrained environments
- Baseline comparison

---

## 2. GRU4Rec / LSTM-based Models

### Core Idea
Use Recurrent Neural Networks to process sequences step-by-step, maintaining hidden state.

### How It Works

```python
# Sequence input
sequence = [item_1, item_2, item_3, ..., item_n]

# GRU processes sequentially
h_0 = initial_state
h_1 = GRU(item_embedding[item_1], h_0)
h_2 = GRU(item_embedding[item_2], h_1)
h_3 = GRU(item_embedding[item_3], h_2)
...
h_n = GRU(item_embedding[item_n], h_{n-1})

# h_n is the sequence representation
```

### Extending for Action Types

```python
# Combine item and action embeddings
def encode_event(item_id, action_type):
    item_emb = item_embedding(item_id)
    action_emb = action_embedding(action_type)
    return item_emb + action_emb  # or concatenate

h_t = GRU(encode_event(item_t, action_t), h_{t-1})
```

### Strengths
| Strength | Description |
|----------|-------------|
| **Full sequence modeling** | Captures long-range dependencies |
| **Variable length** | Naturally handles different sequence lengths |
| **Temporal ordering** | Strict left-to-right processing |
| **Action integration** | Easy to add action type embeddings |

### Weaknesses
| Weakness | Description |
|----------|-------------|
| **Sequential bottleneck** | Cannot parallelize training |
| **Vanishing gradients** | Struggles with very long sequences (100+) |
| **Attention to early items** | First events may be "forgotten" |
| **Inference latency** | Must process entire sequence sequentially |

### Best For
- Medium-length sequences (10-50 events)
- When temporal order is critical
- Moderate compute budgets

---

## 3. Transformer-Based Models (SASRec, BERT4Rec)

### Core Idea
Use self-attention to model relationships between ALL positions in a sequence simultaneously.

### SASRec (Self-Attentive Sequential Recommendation)

```python
# Causal (left-to-right) attention
# Each position can only attend to previous positions

sequence = [item_1, item_2, item_3, item_4]

# Attention pattern:
# item_1: attends to [item_1]
# item_2: attends to [item_1, item_2]
# item_3: attends to [item_1, item_2, item_3]
# item_4: attends to [item_1, item_2, item_3, item_4]

# Output: contextualized representations for each position
```

### BERT4Rec (Bidirectional)

```python
# Bidirectional attention with masked item prediction
# Each position attends to ALL other positions

sequence = [item_1, [MASK], item_3, item_4]

# Training objective: predict masked item from context
# Attention: every position sees every other position
```

### Action-Aware Transformer

```python
class ActionAwareTransformer:
    def encode_event(self, item_id, action_type, position, timestamp):
        item_emb = self.item_embedding(item_id)        # What product
        action_emb = self.action_embedding(action_type) # What action
        pos_emb = self.position_embedding(position)     # Where in sequence
        time_emb = self.time_encoding(timestamp)        # When

        return item_emb + action_emb + pos_emb + time_emb

    def forward(self, sequence):
        # Embed all events
        embeddings = [self.encode_event(**event) for event in sequence]

        # Self-attention (causal mask for prediction)
        output = self.transformer_layers(embeddings, causal_mask=True)

        return output[-1]  # Final position = sequence representation
```

### Strengths
| Strength | Description |
|----------|-------------|
| **Parallel training** | All positions computed simultaneously |
| **Long-range attention** | Any position can attend to any other |
| **Flexible architecture** | Easy to add features (action, time, etc.) |
| **State-of-the-art performance** | Best results on most benchmarks |
| **Attention visualization** | Can inspect which items influenced prediction |

### Weaknesses
| Weakness | Description |
|----------|-------------|
| **Quadratic complexity** | O(n^2) attention for sequence length n |
| **Fixed max length** | Must truncate or pad sequences |
| **Data hungry** | Needs substantial training data |
| **Less interpretable** | Complex attention patterns |

### Best For
- Large-scale production systems
- Long sequences (50-200 events)
- When compute is available
- Maximum prediction accuracy

---

## 4. Variational Autoencoders (VAE, Seq-VAE)

### Core Idea
Learn a compressed latent representation that can reconstruct the input sequence.

### Standard VAE (for aggregated features)

```python
# Encoder: Input → Latent distribution
def encode(user_features):
    h = neural_network(user_features)
    mu = linear(h)      # Mean of latent distribution
    sigma = linear(h)   # Std of latent distribution
    return mu, sigma

# Reparameterization: Sample from distribution
z = mu + sigma * random_normal()

# Decoder: Latent → Reconstructed input
reconstructed = decode(z)

# Loss = Reconstruction + KL divergence
loss = reconstruction_loss(input, reconstructed) + KL(q(z|x) || p(z))
```

### Sequence VAE

```python
# Encoder: LSTM/Transformer processes sequence → latent
encoder_output = lstm_encoder(sequence)
mu, sigma = latent_projection(encoder_output)
z = reparameterize(mu, sigma)

# Decoder: Latent → reconstructed sequence
reconstructed_sequence = lstm_decoder(z)
```

### Strengths
| Strength | Description |
|----------|-------------|
| **Generative capability** | Can sample new customer profiles |
| **Disentangled representations** | Each latent dim can have meaning |
| **Uncertainty quantification** | Distribution over representations |
| **Regularization** | KL term prevents overfitting |

### Weaknesses
| Weakness | Description |
|----------|-------------|
| **Training instability** | KL collapse, posterior collapse |
| **Reconstruction vs compression** | Trade-off is hard to balance |
| **Interpretability not guaranteed** | Need special techniques (β-VAE) |
| **Sequence modeling challenges** | Decoding sequences is hard |

### Best For
- When generative modeling is needed
- Customer journey simulation
- Anomaly detection
- When uncertainty matters

---

## 5. Graph Neural Networks (GNN)

### Core Idea
Model customer journeys as graphs where nodes are products/actions and edges are transitions.

### Approaches
- **Session graphs**: Each session is a directed graph
- **Global product graphs**: Products connected by co-purchase
- **Heterogeneous graphs**: Different node/edge types for actions

### Strengths
| Strength | Description |
|----------|-------------|
| **Structural patterns** | Captures graph topology |
| **Multi-hop reasoning** | Information propagates across edges |
| **Heterogeneous data** | Can model different entity types |

### Weaknesses
| Weakness | Description |
|----------|-------------|
| **Complexity** | Graph construction and message passing |
| **Scalability** | Large graphs are expensive |
| **Strict ordering lost** | Graphs are not inherently sequential |

### Best For
- Complex multi-entity relationships
- When graph structure is natural (social networks)
- Knowledge graph integration

---

## Summary Comparison

| Technique | Sequence Order | Action Types | Interpretability | Compute | Scale |
|-----------|---------------|--------------|------------------|---------|-------|
| Item2Vec | Local (window) | Via tokenization | High | Low | Excellent |
| GRU4Rec | Full | Via embedding | Low | Medium | Good |
| SASRec | Full | Via embedding | Medium | High | Good |
| BERT4Rec | Bidirectional | Via embedding | Medium | Very High | Moderate |
| Seq-VAE | Full | Via embedding | Medium | High | Moderate |
| GNN | Partial | Via edge types | Low | High | Moderate |

---

## Recommendation for This Use Case

Given requirements:
- **High interpretability** needed
- **Automatic weight learning** desired
- **Near real-time updates** required
- **Exploratory** data scale

**Primary recommendation:** Hybrid approach
1. **Item2Vec** for sequence-aware embeddings (interpretable, fast)
2. **NMF** on top for dimension reduction to interpretable traits

→ See [05-recommended-approach.md](./05-recommended-approach.md) for details.
