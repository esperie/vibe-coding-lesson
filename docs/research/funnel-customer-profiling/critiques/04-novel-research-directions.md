# 04 - Novel Research Directions

## Overview

This document identifies **gaps in the literature** that could form the basis of a conference paper or thesis. Each direction addresses weaknesses in existing approaches while providing genuine novelty.

---

## Assessment: What Makes a Paper Publishable?

| Venue | Requirements |
|-------|--------------|
| **Top ML (NeurIPS, ICML, ICLR)** | Novel method + theoretical analysis + strong empirical results |
| **RecSys** | Novel method OR significant empirical contribution + production relevance |
| **SIGIR/CIKM** | Novel application OR comprehensive empirical study |
| **KDD Applied** | Production deployment evidence + business impact |
| **Workshop/Demo** | Interesting idea + preliminary results |

---

## Research Direction 1: Directional Skip-gram for Causal Sequences

### The Gap

Standard Skip-gram (used in Item2Vec) has **symmetric context**:
- Predicts both left and right context from center word
- Cannot distinguish "A before B" from "B before A"
- This contradicts the causal nature of customer journeys

**No existing work** specifically addresses asymmetric Skip-gram for e-commerce sequences.

### The Novel Contribution

**Causal Skip-gram**: Modify Skip-gram to only predict forward context

```
Standard Skip-gram objective:
  L = Σ [log P(w_{t-k} | w_t) + log P(w_{t+k} | w_t)]
      Both directions!

Causal Skip-gram objective:
  L = Σ [log P(w_{t+k} | w_t)]
      Only forward! (what happens AFTER this action?)
```

### Why This Matters

```
Sequence: [view_A] → [cart_A] → [remove_A] → [cart_B] → [buy_B]

Standard Skip-gram learns:
  view_A ↔ cart_A (bidirectional, loses causality)
  remove_A ↔ cart_A (bidirectional, confuses relationship)

Causal Skip-gram learns:
  view_A → cart_A (viewing leads to carting)
  cart_A → remove_A (carting sometimes leads to removal)
  remove_A → cart_B (removal leads to alternative)

The embeddings capture CAUSAL relationships!
```

### Research Questions

1. Does causal Skip-gram improve customer profiling accuracy?
2. Do the learned embeddings better capture purchase intent?
3. How does the asymmetry affect the embedding geometry?
4. Can we prove theoretical properties of causal embeddings?

### Novelty Assessment

| Aspect | Score | Notes |
|--------|-------|-------|
| Technical novelty | High | Novel objective function |
| Theoretical contribution | Medium | Needs formal analysis |
| Empirical contribution | Medium | Needs comprehensive experiments |
| Practical relevance | High | Addresses real problem |

**Venue fit**: RecSys, CIKM, SIGIR (with strong experiments)

### Implementation Outline

```python
class CausalSkipGram(nn.Module):
    def __init__(self, vocab_size, embedding_dim, window_size):
        self.center_embedding = nn.Embedding(vocab_size, embedding_dim)
        self.context_embedding = nn.Embedding(vocab_size, embedding_dim)
        self.window_size = window_size

    def forward(self, center_words, context_words, negative_words):
        center_emb = self.center_embedding(center_words)
        context_emb = self.context_embedding(context_words)
        negative_emb = self.context_embedding(negative_words)

        # Positive: center predicts FUTURE context
        pos_score = (center_emb * context_emb).sum(dim=-1)

        # Negative sampling
        neg_score = (center_emb.unsqueeze(1) * negative_emb).sum(dim=-1)

        # Loss: maximize positive, minimize negative
        loss = -F.logsigmoid(pos_score).mean() - F.logsigmoid(-neg_score).mean()
        return loss

    def get_training_pairs(self, sequence):
        pairs = []
        for i, center in enumerate(sequence):
            # Only forward context (causal)
            for j in range(i + 1, min(i + self.window_size + 1, len(sequence))):
                pairs.append((center, sequence[j]))
        return pairs
```

---

## Research Direction 2: Disentangled Sequential VAE for Customer Traits

### The Gap

Existing work on disentangled recommendations (MacridVAE, etc.) focuses on:
- Item-level disentanglement
- Static user preferences
- Implicit feedback (ratings)

**No existing work** applies disentangled learning to **sequential funnel data** with **explicit action types**.

### The Novel Contribution

**FunnelVAE**: A sequential VAE that disentangles customer traits from funnel journeys

```
┌─────────────────────────────────────────────────────────────────────────┐
│                              FunnelVAE                                  │
│                                                                         │
│  Journey: [view_A, view_B, cart_A, remove_A, cart_B, buy_B]            │
│                            │                                            │
│                            ▼                                            │
│  ┌─────────────────────────────────────────────────────────┐           │
│  │              Bidirectional LSTM Encoder                  │           │
│  │  Captures: temporal patterns, action sequences           │           │
│  └─────────────────────────────────────────────────────────┘           │
│                            │                                            │
│                            ▼                                            │
│  ┌─────────────────────────────────────────────────────────┐           │
│  │         Disentangled Latent Space (β > 1)               │           │
│  │  z1: Purchase intent    (low → high)                    │           │
│  │  z2: Price sensitivity  (insensitive → sensitive)       │           │
│  │  z3: Decision style     (impulsive → deliberate)        │           │
│  │  z4: Category focus     (narrow → broad)                │           │
│  └─────────────────────────────────────────────────────────┘           │
│                            │                                            │
│                            ▼                                            │
│  ┌─────────────────────────────────────────────────────────┐           │
│  │              Action-Aware Decoder                        │           │
│  │  Reconstructs: sequence of (action, product) pairs       │           │
│  └─────────────────────────────────────────────────────────┘           │
└─────────────────────────────────────────────────────────────────────────┘
```

### Key Innovations

1. **Action-type aware encoding**: Separate embeddings for action and product
2. **Funnel-specific decoder**: Predicts action type AND product
3. **Disentanglement via β-VAE**: Forces interpretable latent dimensions
4. **Temporal structure preservation**: LSTM captures sequence dynamics

### Research Questions

1. Can we achieve disentanglement on funnel data?
2. Do the learned factors correspond to meaningful customer traits?
3. How does β affect the quality-interpretability tradeoff?
4. Can we use the factors for controllable recommendations?

### Novelty Assessment

| Aspect | Score | Notes |
|--------|-------|-------|
| Technical novelty | High | Novel architecture for funnel data |
| Theoretical contribution | Medium | Extends β-VAE theory to sequences |
| Empirical contribution | High | New domain application |
| Practical relevance | High | Directly addresses interpretability need |

**Venue fit**: NeurIPS, RecSys, KDD (with deployment evidence)

### Implementation Outline

```python
class FunnelVAE(nn.Module):
    def __init__(self, n_products, n_actions, d_model, d_latent, beta=4.0):
        self.product_emb = nn.Embedding(n_products, d_model)
        self.action_emb = nn.Embedding(n_actions, d_model)
        self.encoder = nn.LSTM(d_model * 2, d_model, bidirectional=True)
        self.fc_mu = nn.Linear(d_model * 2, d_latent)
        self.fc_logvar = nn.Linear(d_model * 2, d_latent)
        self.decoder = nn.LSTM(d_latent, d_model)
        self.product_head = nn.Linear(d_model, n_products)
        self.action_head = nn.Linear(d_model, n_actions)
        self.beta = beta

    def encode(self, products, actions):
        # Combine product and action embeddings
        x = torch.cat([self.product_emb(products), self.action_emb(actions)], dim=-1)
        _, (h, _) = self.encoder(x)
        h = h.transpose(0, 1).reshape(h.size(1), -1)  # Combine bidirectional
        return self.fc_mu(h), self.fc_logvar(h)

    def decode(self, z, seq_len):
        # Expand z for each timestep
        z_expanded = z.unsqueeze(1).repeat(1, seq_len, 1)
        output, _ = self.decoder(z_expanded)
        return self.product_head(output), self.action_head(output)

    def loss(self, products, actions, recon_products, recon_actions, mu, logvar):
        # Reconstruction loss (product + action)
        recon_loss = (
            F.cross_entropy(recon_products.view(-1, recon_products.size(-1)), products.view(-1)) +
            F.cross_entropy(recon_actions.view(-1, recon_actions.size(-1)), actions.view(-1))
        )
        # KL divergence with β weighting
        kl_loss = -0.5 * torch.sum(1 + logvar - mu.pow(2) - logvar.exp())
        return recon_loss + self.beta * kl_loss
```

---

## Research Direction 3: seqNMF for Behavioral Pattern Discovery

### The Gap

seqNMF has been applied to:
- Neuroscience (neural spike patterns)
- Audio (music motifs)
- Video (action recognition)

**No existing work** applies seqNMF to **customer journey patterns**.

### The Novel Contribution

**BehaviorNMF**: Apply seqNMF to discover recurring behavioral patterns in funnels

```
Discovered patterns (examples):

Pattern 1 (length 4): "Research-Buy"
  [view] → [view] → [cart] → [buy]

Pattern 2 (length 5): "Comparison-Abandon"
  [view_A] → [view_B] → [cart_A] → [view_B] → [abandon]

Pattern 3 (length 3): "Impulse"
  [view] → [cart] → [buy]

Pattern 4 (length 6): "Deliberate-Switch"
  [view_A] → [cart_A] → [remove_A] → [view_B] → [cart_B] → [buy_B]
```

### Key Innovations

1. **Pattern library discovery**: Automatically find recurring journey structures
2. **Customer characterization**: Each customer = mixture of patterns
3. **Temporal localization**: Know WHEN patterns occur in journeys
4. **Interpretable by design**: Patterns can be visualized and named

### Research Questions

1. What behavioral patterns exist in funnel data?
2. Are patterns universal across domains or domain-specific?
3. Can patterns predict conversion probability?
4. How do patterns correlate with customer lifetime value?

### Novelty Assessment

| Aspect | Score | Notes |
|--------|-------|-------|
| Technical novelty | Low | seqNMF exists; application is novel |
| Theoretical contribution | Low | No new theory |
| Empirical contribution | High | New domain, insights |
| Practical relevance | Very High | Directly actionable insights |

**Venue fit**: RecSys Industry Track, KDD Applied, CIKM

---

## Research Direction 4: Interpretable Attention Aggregation

### The Gap

Attention mechanisms are used in recommendations (SASRec, BERT4Rec) but:
- Attention weights are not explicitly interpretable
- No constraint that attention should correspond to meaningful factors
- Post-hoc interpretation is unreliable

### The Novel Contribution

**InterpAttn**: Attention aggregation with built-in interpretability constraints

```
Standard attention:
  weights = softmax(Q × K^T)
  (Weights are computed but not constrained to be meaningful)

InterpAttn:
  weights = softmax(Q × K^T) subject to:
  - Sparsity constraint (only few tokens should dominate)
  - Diversity constraint (different heads attend to different things)
  - Alignment constraint (attention should align with action types)
```

### Key Innovations

1. **Sparse attention**: Force most weights to be near-zero
2. **Diverse heads**: Different heads must attend to different action types
3. **Aligned attention**: Head 1 = intent actions, Head 2 = exploration actions
4. **Interpretable by construction**: Not post-hoc explanation

### Research Questions

1. Can we constrain attention without hurting performance?
2. Do the constraints produce more faithful explanations?
3. How do users perceive interpretable vs. standard attention?
4. What's the performance-interpretability tradeoff?

### Novelty Assessment

| Aspect | Score | Notes |
|--------|-------|-------|
| Technical novelty | High | Novel constraints |
| Theoretical contribution | Medium | Formalizes interpretability |
| Empirical contribution | Medium | Needs user studies |
| Practical relevance | High | XAI is important |

**Venue fit**: AAAI, FAccT, RecSys

---

## Research Direction 5: Unified Framework with Theoretical Analysis

### The Gap

Existing approaches are **ad-hoc combinations** without understanding:
- When does Item2Vec preserve sequence information?
- What are the bounds on information loss in aggregation?
- When is NMF appropriate for embeddings?

### The Novel Contribution

**Formal framework** for analyzing sequential customer profiling:

```
Theorem 1 (Information Loss Bound):
  Let S be a customer sequence and f be the embedding function.
  The information loss in aggregation g is bounded by:
  I(S; g(f(S))) ≥ I(S; f(S)) - ε(g)
  where ε(g) depends on the aggregation function.

Theorem 2 (NMF Consistency):
  For embeddings with property P, NMF factorization preserves
  customer similarity iff [conditions].

Theorem 3 (Disentanglement in Sequences):
  A sequential encoder achieves disentanglement score D iff
  the latent dimensions satisfy [independence conditions].
```

### Key Innovations

1. **Formal definitions**: What does "interpretable" mean mathematically?
2. **Provable bounds**: Information-theoretic analysis
3. **Necessary conditions**: When do different approaches work?
4. **Unified view**: Connect Item2Vec, NMF, VAE, Transformers

### Research Questions

1. What information-theoretic framework captures interpretability?
2. Can we prove bounds on the quality of different pipelines?
3. What are necessary conditions for disentanglement in sequences?
4. How do different methods compare under this framework?

### Novelty Assessment

| Aspect | Score | Notes |
|--------|-------|-------|
| Technical novelty | Very High | New theoretical framework |
| Theoretical contribution | Very High | Formal analysis |
| Empirical contribution | Medium | Needs validation |
| Practical relevance | Medium | Guides method selection |

**Venue fit**: NeurIPS, ICML, JMLR

---

## Recommended Path Forward

### For a Master's Thesis

**Option A: Empirical Focus (Lower risk)**
1. Implement seqNMF for funnel data
2. Comprehensive experiments on 2-3 datasets
3. Ablation studies and pattern analysis
4. Industry collaboration for deployment

**Option B: Methodological Focus (Medium risk)**
1. Develop FunnelVAE (Disentangled Sequential VAE)
2. Experiments comparing to baselines
3. User study on interpretability
4. Ablation on β parameter

### For a PhD Thesis

**Full Research Program:**
1. Year 1: Theoretical framework (Direction 5)
2. Year 2: Novel method development (Direction 2 or 4)
3. Year 3: Large-scale empirical validation
4. Year 4: Production deployment and impact study

### For a Conference Paper (Quick Win)

**Causal Skip-gram + Attention Pooling:**
1. Implement causal Skip-gram (Direction 1)
2. Add attention aggregation (Direction 4 simplified)
3. Compare to Item2Vec + mean baseline
4. Submit to RecSys or CIKM

---

## Summary: Publication Potential

| Direction | Novelty | Difficulty | Timeline | Venue |
|-----------|---------|------------|----------|-------|
| Causal Skip-gram | High | Low | 3-6 months | RecSys, CIKM |
| FunnelVAE | High | High | 6-12 months | NeurIPS, KDD |
| BehaviorNMF (seqNMF) | Medium | Medium | 4-8 months | RecSys Industry |
| InterpAttn | High | Medium | 6-9 months | AAAI, FAccT |
| Theoretical Framework | Very High | Very High | 12-24 months | NeurIPS, JMLR |

**Recommended for immediate pursuit**: Direction 1 (Causal Skip-gram) as it has:
- Clear novelty
- Manageable scope
- Direct comparison to baseline (Item2Vec)
- Practical relevance
