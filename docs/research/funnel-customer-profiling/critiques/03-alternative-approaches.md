# 03 - Alternative Approaches

## Overview

This document presents **superior alternatives** to the Item2Vec + NMF pipeline, based on recent literature (2019-2025). Each alternative addresses specific weaknesses identified in the critique.

---

## 1. Disentangled VAE (MacridVAE)

### Source
[Learning Disentangled Representations for Recommendation](https://proceedings.neurips.cc/paper/2019/file/a2186aa7c086b46ad4e8bf81e2a3a19b-Paper.pdf) (NeurIPS 2019)

### Core Idea

Instead of Item2Vec + NMF (two separate stages), use a **single VAE** that learns:
- **Macro-disentanglement**: High-level concepts (e.g., "buying intent", "browsing mode")
- **Micro-disentanglement**: Low-level factors (e.g., "price sensitivity", "brand loyalty")

```
┌─────────────────────────────────────────────────────────────────┐
│                         MacridVAE                               │
│                                                                 │
│  Customer Journey → Encoder → Latent z → Decoder → Reconstruct │
│                         │                                       │
│                         ▼                                       │
│                  [z1: intent, z2: price, z3: brand, ...]       │
│                  (Each dimension is interpretable!)             │
└─────────────────────────────────────────────────────────────────┘
```

### Advantages over Item2Vec + NMF

| Aspect | Item2Vec + NMF | MacridVAE |
|--------|----------------|-----------|
| End-to-end learning | No (3 stages) | Yes |
| Interpretability | Post-hoc (NMF) | Built-in (disentanglement) |
| Handles sequences | Partially (context window) | Fully (sequential encoder) |
| Negative values | Requires shifting | Native handling |
| Uncertainty | No | Yes (probabilistic) |

### Implementation Sketch

```python
class MacridVAE(nn.Module):
    def __init__(self, n_items, n_intents, d_latent):
        self.item_embedding = nn.Embedding(n_items, d_model)
        self.intent_encoder = nn.Linear(d_model, n_intents)  # Macro
        self.factor_encoder = nn.Linear(d_model, d_latent)   # Micro

    def encode(self, sequence):
        item_embs = self.item_embedding(sequence)
        pooled = item_embs.mean(dim=1)  # Or attention

        # Macro: Which intent cluster?
        intent_logits = self.intent_encoder(pooled)
        intent_probs = F.softmax(intent_logits, dim=-1)

        # Micro: What factors within intent?
        mu = self.factor_encoder(pooled)
        logvar = self.factor_var_encoder(pooled)

        return intent_probs, mu, logvar

    def reparameterize(self, mu, logvar):
        std = torch.exp(0.5 * logvar)
        eps = torch.randn_like(std)
        return mu + eps * std

    def decode(self, z, intent):
        # Reconstruct interaction probabilities
        return self.decoder(torch.cat([z, intent], dim=-1))
```

### Why This is Better

1. **Single objective**: Reconstruction + KL divergence
2. **Interpretable latent space**: Each z dimension forced to be independent
3. **Handles sequences natively**: Can use LSTM/Transformer encoder
4. **No shifting hack**: VAE naturally handles mixed-sign latents

---

## 2. seqNMF (Convolutional NMF for Sequences)

### Source
[Unsupervised discovery of temporal sequences](https://elifesciences.org/articles/38471) (eLife 2019)

### Core Idea

Classical NMF: `V ≈ W × H` (static factorization)
seqNMF: `V ≈ W ⊛ H` (convolutional factorization)

```
Standard NMF:
  Data = Basis × Coefficients
  [time × features] = [features × k] × [k × time]

seqNMF:
  Data = Basis_patterns ⊛ Activations
  [time × features] = [τ × features × k] ⊛ [k × time]

  Where τ = pattern duration (temporal extent)
```

### Why This Matters for Funnel Data

seqNMF discovers **recurring temporal patterns**, not just static factors:

```
Discovered pattern 1 (τ=5 steps):
  [view] → [view] → [cart] → [view] → [buy]
  = "Research-then-buy" pattern

Discovered pattern 2 (τ=4 steps):
  [view] → [cart] → [remove] → [leave]
  = "Abandonment" pattern
```

Each customer is described by **which patterns occur** and **when**, not just average embedding.

### Advantages over Item2Vec + NMF

| Aspect | Item2Vec + NMF | seqNMF |
|--------|----------------|--------|
| Temporal patterns | Lost in aggregation | Explicitly discovered |
| Pattern length | Fixed context window | Learned pattern duration |
| Pattern occurrence | Not tracked | Tracked with timestamps |
| Interpretability | Factor loadings | Visual pattern inspection |

### Implementation Considerations

1. **Data format**: Time × Action matrix (one-hot encoded actions)
2. **Pattern count (k)**: Chosen via cross-validation
3. **Pattern length (τ)**: Can vary per pattern or be fixed
4. **Sparsity**: Encouraged on activations (patterns occur sparsely)

### Application to Funnel Data

```python
# Convert funnel to matrix
# Rows: time steps, Columns: action types

funnel_matrix = np.zeros((sequence_length, n_action_types))
for t, (action, product) in enumerate(customer_journey):
    action_idx = action_to_idx[f"{action}_{product}"]
    funnel_matrix[t, action_idx] = 1

# Apply seqNMF
W, H = seqNMF(funnel_matrix, K=10, L=5)  # 10 patterns, length 5

# W[k]: Pattern k (temporal profile)
# H[k, t]: Activation of pattern k at time t
```

---

## 3. Transformer with Disentangled Attention

### Source
[Automated Disentangled Sequential Recommendation](https://dl.acm.org/doi/10.1145/3675164) (TOIS 2024)

### Core Idea

Use Transformer's attention mechanism but **disentangle** it into interpretable heads:

```
Standard Multi-Head Attention:
  Attention = softmax(Q × K^T / √d) × V
  Heads are uninterpretable

Disentangled Attention:
  Head 1: Attends to "intent" signals (cart, buy actions)
  Head 2: Attends to "exploration" signals (view diversity)
  Head 3: Attends to "recency" (recent actions weighted higher)
  ...
  Each head has interpretable meaning!
```

### How Disentanglement is Achieved

1. **Constrained attention patterns**: Force each head to attend to specific action types
2. **Knowledge-guided**: Use external knowledge (product categories) to guide heads
3. **Regularization**: Encourage heads to be orthogonal/independent

### Advantages over Item2Vec + NMF

| Aspect | Item2Vec + NMF | Disentangled Transformer |
|--------|----------------|--------------------------|
| Attention mechanism | None | Learnable, interpretable |
| Long-range dependencies | Lost (local window) | Full sequence |
| Directionality | Symmetric (Skip-gram) | Causal (Transformer) |
| End-to-end | No | Yes |

### Implementation Sketch

```python
class DisentangledTransformer(nn.Module):
    def __init__(self, config):
        # Standard transformer components
        self.embedding = nn.Embedding(config.vocab_size, config.d_model)
        self.pos_encoding = PositionalEncoding(config.d_model)

        # Disentangled attention heads
        self.intent_head = AttentionHead(config.d_model, mask_type='intent_actions')
        self.explore_head = AttentionHead(config.d_model, mask_type='view_actions')
        self.recency_head = AttentionHead(config.d_model, mask_type='recency_decay')

        # Trait decoder
        self.trait_decoder = nn.Linear(config.d_model * 3, config.n_traits)

    def forward(self, sequence):
        x = self.embedding(sequence) + self.pos_encoding(sequence)

        # Each head focuses on different aspects
        intent_repr = self.intent_head(x)     # Captures purchase intent
        explore_repr = self.explore_head(x)   # Captures browsing behavior
        recency_repr = self.recency_head(x)   # Captures recent preferences

        # Combine for final representation
        combined = torch.cat([intent_repr, explore_repr, recency_repr], dim=-1)
        traits = F.softmax(self.trait_decoder(combined), dim=-1)

        return traits
```

---

## 4. β-VAE for Interpretable Factors

### Source
[β-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework](https://openreview.net/forum?id=Sy2fzU9gl) (ICLR 2017)

### Core Idea

Standard VAE: `Loss = Reconstruction + KL(q(z|x) || p(z))`
β-VAE: `Loss = Reconstruction + β × KL(q(z|x) || p(z))`

When β > 1, the model is **forced** to learn disentangled representations.

### Why This Works

Higher β creates a stronger "information bottleneck":
- Latent z must be compressed
- The most efficient compression is disentangled (one factor per dimension)
- Each latent dimension becomes interpretable

### For Funnel Data

```
Latent dimensions (automatically discovered):
  z1: Price sensitivity (low → high)
  z2: Purchase intent (browsing → buying)
  z3: Category focus (narrow → broad)
  z4: Decision speed (impulsive → deliberate)
```

### Trade-off

| β Value | Disentanglement | Reconstruction | Interpretability |
|---------|-----------------|----------------|------------------|
| β = 1 | Low | High | Low |
| β = 4 | Medium | Medium | Medium |
| β = 10 | High | Low | High |
| β = 100 | Very High | Very Low | Very High (but lossy) |

### Implementation

```python
class BetaVAE(nn.Module):
    def __init__(self, beta=4.0):
        self.beta = beta
        self.encoder = SequenceEncoder()  # LSTM or Transformer
        self.decoder = SequenceDecoder()

    def forward(self, x):
        mu, logvar = self.encoder(x)
        z = self.reparameterize(mu, logvar)
        recon = self.decoder(z)
        return recon, mu, logvar

    def loss(self, x, recon, mu, logvar):
        recon_loss = F.binary_cross_entropy(recon, x, reduction='sum')
        kl_loss = -0.5 * torch.sum(1 + logvar - mu.pow(2) - logvar.exp())
        return recon_loss + self.beta * kl_loss  # β > 1 for disentanglement
```

---

## 5. Attention-Based Aggregation (Learned Pooling)

### Source
[Attentive Temporal Pooling](https://www.emergentmind.com/topics/attentive-temporal-pooling-mechanism) (2024)

### Core Idea

Replace fixed aggregation (mean, TF-IDF) with **learned attention**:

```
Fixed pooling:
  customer_emb = mean(token_embeddings)

Attention pooling:
  weights = softmax(W @ token_embeddings)  # Learned W
  customer_emb = weights @ token_embeddings
```

### Advantages

1. **Learns what matters**: Automatically discovers important tokens
2. **Interpretable weights**: Attention scores show which actions drove the profile
3. **Handles variable length**: Naturally works with any sequence length
4. **End-to-end**: Can be trained with downstream task

### Implementation

```python
class AttentivePooling(nn.Module):
    def __init__(self, d_model):
        self.attention = nn.Sequential(
            nn.Linear(d_model, d_model // 2),
            nn.Tanh(),
            nn.Linear(d_model // 2, 1)
        )

    def forward(self, token_embeddings, mask=None):
        # token_embeddings: (batch, seq_len, d_model)
        scores = self.attention(token_embeddings).squeeze(-1)  # (batch, seq_len)

        if mask is not None:
            scores = scores.masked_fill(mask == 0, -1e9)

        weights = F.softmax(scores, dim=-1)  # (batch, seq_len)
        pooled = torch.bmm(weights.unsqueeze(1), token_embeddings).squeeze(1)

        return pooled, weights  # Return weights for interpretability
```

### Can Be Combined with Item2Vec

```
Stage 1: Train Item2Vec (as before)
Stage 2: Train attention pooling on customer task
Stage 3: Apply NMF to attention-pooled embeddings

Improvement: Stage 2 replaces fixed mean with learned aggregation
```

---

## Comparison Matrix

| Approach | Sequences | Interpretability | End-to-End | Complexity | Novelty for Paper |
|----------|-----------|------------------|------------|------------|-------------------|
| Item2Vec + NMF | Partial | Medium | No | Low | None |
| MacridVAE | Full | High | Yes | High | Low (published) |
| seqNMF | Full | High | N/A | Medium | Medium (new domain) |
| Disentangled Transformer | Full | High | Yes | High | Medium |
| β-VAE | Full | High | Yes | Medium | Medium |
| Attention Pooling | Partial | High | Partial | Low | High (if novel design) |

---

## Recommendation

### For Immediate Production Improvement

**Add Attention Pooling** to the current pipeline:
- Minimal architectural change
- Significant improvement in interpretability
- Can be done incrementally

### For Research Publication

**Develop a novel combination:**

```
Proposed: Directional Skip-gram + Attention Pooling + Disentangled Decoder

1. Directional Skip-gram: Asymmetric context (only predict forward)
   → Novel contribution: Causal awareness in embeddings

2. Attention Pooling: Learned aggregation with interpretable weights
   → Novel contribution: Explains which actions matter

3. Disentangled Decoder: β-VAE style output layer with KL regularization
   → Novel contribution: Forces interpretable factor structure

Combined: End-to-end interpretable customer profiling for sequential data
```

See [04-novel-research-directions.md](./04-novel-research-directions.md) for detailed proposal.
