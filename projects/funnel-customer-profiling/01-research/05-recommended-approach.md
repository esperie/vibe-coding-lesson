# 05 - Recommended Approach: Hybrid Item2Vec + NMF

## Overview

Given the requirements for **high interpretability**, **automatic weight learning**, and **sequence awareness**, we recommend a **two-stage hybrid approach**:

1. **Stage 1: Item2Vec** - Learn sequence-aware embeddings from action-item pairs
2. **Stage 2: Customer Aggregation** - Combine embeddings per customer
3. **Stage 3: NMF** - Decompose into interpretable trait dimensions

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          RAW FUNNEL DATA                                │
│                                                                         │
│  user_id | timestamp | action      | product_id | session_id           │
│  --------|-----------|-------------|------------|----------            │
│  A       | 1000      | view        | prod_001   | sess_1               │
│  A       | 1005      | view        | prod_002   | sess_1               │
│  A       | 1010      | add_cart    | prod_001   | sess_1               │
│  A       | 1035      | remove_cart | prod_001   | sess_1               │
│  A       | 1040      | add_cart    | prod_003   | sess_1               │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     STAGE 0: PREPROCESSING                              │
│                                                                         │
│  1. Session segmentation (30-min inactivity rule)                       │
│  2. Action-item tokenization: "view_prod_001", "cart_prod_001", etc.    │
│  3. Filter: minimum session length, remove bots                         │
│                                                                         │
│  Output: List of token sequences per session                            │
│  [["view_prod_001", "view_prod_002", "cart_prod_001", ...], ...]       │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     STAGE 1: ITEM2VEC TRAINING                          │
│                                                                         │
│  Algorithm: Skip-gram with Negative Sampling (SGNS)                     │
│  Input: All token sequences (sessions as "sentences")                   │
│  Output: Embedding matrix E ∈ ℝ^(n_tokens × d)                          │
│                                                                         │
│  Parameters:                                                            │
│  - embedding_dim (d): 64-128                                            │
│  - context_window: 5                                                    │
│  - min_count: 5 (filter rare tokens)                                    │
│  - negative_samples: 5                                                  │
│  - epochs: 10-20                                                        │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     STAGE 2: CUSTOMER AGGREGATION                       │
│                                                                         │
│  For each customer, aggregate their token embeddings:                   │
│                                                                         │
│  Option A: Simple mean                                                  │
│    customer_emb = mean([E[token] for token in customer_tokens])         │
│                                                                         │
│  Option B: TF-IDF weighted mean (recommended)                           │
│    weights[token] = log(N / df[token])  # Inverse doc frequency         │
│    customer_emb = weighted_mean(embeddings, weights)                    │
│                                                                         │
│  Option C: Recency weighted                                             │
│    weights[i] = decay^(n - i)  # Recent tokens weighted higher          │
│                                                                         │
│  Output: Customer embedding matrix C ∈ ℝ^(n_customers × d)              │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     STAGE 3: NMF DECOMPOSITION                          │
│                                                                         │
│  Problem: Customer embeddings may have negative values (from Item2Vec)  │
│  Solution: Shift to non-negative before NMF                             │
│                                                                         │
│  C_shifted = C - min(C) + ε  # Make all values positive                 │
│                                                                         │
│  NMF: C_shifted ≈ W × H                                                 │
│  - W ∈ ℝ^(n_customers × k): Customer-to-trait weights                   │
│  - H ∈ ℝ^(k × d): Trait-to-embedding mappings                           │
│                                                                         │
│  Parameters:                                                            │
│  - n_components (k): 8-32 (start with 16)                               │
│  - max_iter: 200                                                        │
│  - init: 'nndsvd'                                                       │
│                                                                         │
│  Output: Customer trait matrix W ∈ ℝ^(n_customers × k)                  │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     FINAL OUTPUT: TRAIT VECTORS                         │
│                                                                         │
│  customer_profiles = {                                                  │
│      "customer_A": [0.15, 0.72, 0.13, 0.45, ...],  # k dimensions       │
│      "customer_B": [0.82, 0.11, 0.07, 0.33, ...],                       │
│      ...                                                                │
│  }                                                                      │
│                                                                         │
│  Trait interpretation (via H matrix analysis):                          │
│  - Trait 0: "Tech products affinity" (loads on tech product embeddings) │
│  - Trait 1: "Price sensitivity" (loads on sale/discount patterns)       │
│  - Trait 2: "Impulsive behavior" (loads on quick cart-purchase)         │
│  ...                                                                    │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Why This Combination?

| Requirement | How It's Met |
|-------------|--------------|
| **Sequence awareness** | Item2Vec captures local ordering via context window |
| **Action type semantics** | Action-item tokens preserve "view_X" ≠ "cart_X" |
| **Negative signals** | "remove_X" tokens learn appropriate relationships |
| **Automatic weight learning** | Skip-gram learns co-occurrence importance |
| **Interpretability** | NMF produces non-negative, interpretable factors |
| **Near real-time updates** | Embeddings fixed; only aggregation updates |
| **Scalability** | Both Item2Vec and NMF are efficient |

---

## Stage Details

### Stage 0: Preprocessing

#### Session Segmentation
```python
def segment_sessions(events, timeout_minutes=30):
    """Split events into sessions based on inactivity gaps."""
    sessions = []
    current_session = []

    for i, event in enumerate(events):
        if i == 0:
            current_session.append(event)
            continue

        time_gap = event['timestamp'] - events[i-1]['timestamp']
        if time_gap > timeout_minutes * 60:  # New session
            if len(current_session) >= 2:  # Minimum session length
                sessions.append(current_session)
            current_session = [event]
        else:
            current_session.append(event)

    if len(current_session) >= 2:
        sessions.append(current_session)

    return sessions
```

#### Tokenization
```python
def tokenize_event(event):
    """Convert event to action-item token."""
    action_map = {
        'view': 'view',
        'add_cart': 'cart',
        'remove_cart': 'remove',
        'purchase': 'buy',
    }
    action = action_map.get(event['action'], event['action'])
    return f"{action}_{event['product_id']}"

# Example
# {"action": "view", "product_id": "prod_001"} → "view_prod_001"
# {"action": "add_cart", "product_id": "prod_001"} → "cart_prod_001"
```

### Stage 1: Item2Vec Training

```python
from gensim.models import Word2Vec

# Prepare sequences (list of lists of tokens)
sequences = [
    ["view_prod_001", "view_prod_002", "cart_prod_001", "remove_prod_001", "cart_prod_003"],
    ["view_prod_005", "view_prod_006", "cart_prod_006", "buy_prod_006"],
    # ... more sessions
]

# Train Item2Vec (Word2Vec on item sequences)
model = Word2Vec(
    sentences=sequences,
    vector_size=64,      # Embedding dimension
    window=5,            # Context window
    min_count=5,         # Minimum token frequency
    sg=1,                # Skip-gram (1) vs CBOW (0)
    negative=5,          # Negative sampling
    epochs=15,
    workers=4,
)

# Access embeddings
embedding = model.wv["view_prod_001"]  # Shape: (64,)

# Find similar tokens
similar = model.wv.most_similar("cart_prod_001", topn=10)
# Returns: [("buy_prod_001", 0.85), ("cart_prod_002", 0.72), ...]
```

### Stage 2: Customer Aggregation

```python
import numpy as np

def aggregate_customer_embedding(customer_tokens, model, method='tfidf'):
    """Aggregate token embeddings into customer embedding."""

    # Get embeddings for known tokens
    embeddings = []
    weights = []

    for token in customer_tokens:
        if token in model.wv:
            embeddings.append(model.wv[token])

            if method == 'mean':
                weights.append(1.0)
            elif method == 'tfidf':
                # IDF weight: rare tokens are more informative
                df = model.wv.get_vecattr(token, 'count')
                idf = np.log(len(model.wv) / (df + 1))
                weights.append(idf)
            elif method == 'recency':
                # More recent tokens weighted higher
                position = customer_tokens.index(token)
                decay = 0.95 ** (len(customer_tokens) - position - 1)
                weights.append(decay)

    if not embeddings:
        return np.zeros(model.vector_size)

    embeddings = np.array(embeddings)
    weights = np.array(weights) / sum(weights)  # Normalize

    return np.average(embeddings, axis=0, weights=weights)
```

### Stage 3: NMF Decomposition

```python
from sklearn.decomposition import NMF
import numpy as np

def apply_nmf(customer_embeddings, n_components=16):
    """Apply NMF to customer embeddings for interpretable traits."""

    # Customer embeddings matrix: (n_customers, embedding_dim)
    C = np.array(list(customer_embeddings.values()))

    # Shift to non-negative (Item2Vec can produce negative values)
    C_min = C.min()
    if C_min < 0:
        C_shifted = C - C_min + 1e-6
    else:
        C_shifted = C

    # Apply NMF
    nmf = NMF(
        n_components=n_components,
        init='nndsvd',
        max_iter=200,
        random_state=42,
    )

    # W: Customer-to-trait weights (n_customers, k)
    # H: Trait-to-embedding mappings (k, embedding_dim)
    W = nmf.fit_transform(C_shifted)
    H = nmf.components_

    # Normalize W to [0, 1] range for each customer
    W_normalized = W / (W.sum(axis=1, keepdims=True) + 1e-6)

    # Map back to customer IDs
    customer_ids = list(customer_embeddings.keys())
    trait_profiles = {
        cid: W_normalized[i].tolist()
        for i, cid in enumerate(customer_ids)
    }

    return trait_profiles, H
```

---

## Trait Interpretation

After NMF, interpret each trait by analyzing the H matrix:

```python
def interpret_traits(H, model, top_k=10):
    """Interpret what each NMF trait represents."""

    interpretations = []

    for trait_idx in range(H.shape[0]):
        trait_vector = H[trait_idx]

        # Find tokens whose embeddings are most aligned with this trait
        similarities = []
        for token in model.wv.index_to_key:
            token_emb = model.wv[token]
            # Cosine similarity
            sim = np.dot(trait_vector, token_emb) / (
                np.linalg.norm(trait_vector) * np.linalg.norm(token_emb) + 1e-6
            )
            similarities.append((token, sim))

        # Top tokens for this trait
        top_tokens = sorted(similarities, key=lambda x: -x[1])[:top_k]

        interpretations.append({
            'trait_index': trait_idx,
            'top_tokens': top_tokens,
            'suggested_name': infer_trait_name(top_tokens),  # Manual or heuristic
        })

    return interpretations

# Example output:
# Trait 0: ["cart_electronics", "buy_electronics", "view_tech"] → "Tech Enthusiast"
# Trait 1: ["view_sale", "cart_clearance", "remove_fullprice"] → "Bargain Hunter"
```

---

## Usage for Recommendations

```python
def find_similar_customers(target_customer_id, trait_profiles, top_k=10):
    """Find customers with similar trait profiles."""
    from sklearn.metrics.pairwise import cosine_similarity

    target_traits = np.array(trait_profiles[target_customer_id]).reshape(1, -1)
    all_traits = np.array(list(trait_profiles.values()))
    all_ids = list(trait_profiles.keys())

    similarities = cosine_similarity(target_traits, all_traits)[0]

    # Sort by similarity (excluding self)
    ranked = sorted(
        [(cid, sim) for cid, sim in zip(all_ids, similarities) if cid != target_customer_id],
        key=lambda x: -x[1]
    )

    return ranked[:top_k]


def recommend_products(customer_id, trait_profiles, product_trait_affinity, top_k=10):
    """Recommend products based on customer traits."""

    customer_traits = np.array(trait_profiles[customer_id])

    # Product scores = trait profile × trait-product affinity
    product_scores = {}
    for product_id, product_traits in product_trait_affinity.items():
        score = np.dot(customer_traits, product_traits)
        product_scores[product_id] = score

    # Return top products
    return sorted(product_scores.items(), key=lambda x: -x[1])[:top_k]
```

---

## Advantages of This Approach

1. **Interpretable output**: Each trait dimension has meaning derived from token analysis
2. **Sequence-aware**: Item2Vec captures ordering through context windows
3. **Action semantics preserved**: "view_X" and "cart_X" are different tokens with different embeddings
4. **Automatic weight learning**: Skip-gram learns importance through co-occurrence
5. **Fast updates**: New customer profiles only need aggregation (embeddings fixed)
6. **Scalable**: Both Item2Vec and NMF are efficient algorithms
7. **Proven components**: Both techniques are well-understood and production-validated

---

## Limitations and Mitigations

| Limitation | Mitigation |
|------------|------------|
| Fixed context window in Item2Vec | Use larger window (10) or supplement with session-level features |
| NMF requires non-negative input | Shift embeddings before decomposition |
| New products have no embeddings | Use product category fallback or retrain periodically |
| Trait interpretation requires domain knowledge | Automated labeling heuristics or manual review |

---

## Alternative: Attention-Based Aggregation

For learned (vs fixed) aggregation weights:

```python
class AttentionAggregator(nn.Module):
    """Learn which tokens matter most for each customer."""

    def __init__(self, embedding_dim):
        super().__init__()
        self.attention = nn.Linear(embedding_dim, 1)

    def forward(self, token_embeddings):
        # token_embeddings: (seq_len, embedding_dim)
        scores = self.attention(token_embeddings)  # (seq_len, 1)
        weights = F.softmax(scores, dim=0)
        aggregated = (weights * token_embeddings).sum(dim=0)
        return aggregated
```

This adds complexity but learns optimal aggregation weights from data.
