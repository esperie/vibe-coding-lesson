# 02 - Why Traditional Dimension Reduction Methods Fail

## Overview

Traditional dimension reduction techniques (NMF, SVD, PCA) were designed for **static, tabular data**. When applied to sequential funnel data, they fundamentally **cannot capture** the temporal and semantic richness of customer journeys.

---

## The Core Problem: Matrix Collapse

All traditional methods require converting sequential data into a **user-item matrix**:

```python
# Original sequence (rich information)
customer_A_sequence = [
    {"action": "view", "product": "a", "time": 1000},
    {"action": "view", "product": "b", "time": 1005},
    {"action": "view", "product": "a", "time": 1010},
    {"action": "add_cart", "product": "a", "time": 1015},
    {"action": "view", "product": "c", "time": 1025},
    {"action": "view", "product": "d", "time": 1030},
    {"action": "remove_cart", "product": "a", "time": 1035},
    {"action": "add_cart", "product": "d", "time": 1040},
]

# Collapsed to matrix (information lost)
user_item_matrix = {
    "customer_A": {"a": 2, "b": 1, "c": 1, "d": 1}
}
# Or with action weights:
user_item_matrix = {
    "customer_A": {"a": 2*1 + 1*3 - 1*2, "b": 1, "c": 1, "d": 1 + 3}
    # view=1, cart=3, remove=-2
}
```

---

## Method-by-Method Analysis

### 1. Non-negative Matrix Factorization (NMF)

**How it works:**
```
R ≈ W × H
where:
  R = user-item matrix (n_users × n_items)
  W = user-factor matrix (n_users × k)
  H = factor-item matrix (k × n_items)
```

**What NMF can capture:**
- Latent "topics" or "archetypes" across users and items
- Non-negative factors (interpretable as "amount of interest")
- Co-occurrence patterns (users who like A also like B)

**What NMF CANNOT capture:**

| Lost Information | Why It Matters |
|------------------|----------------|
| **Temporal order** | `view_a → cart_a` is different from `cart_a → view_a` |
| **Action sequences** | The progression view → cart → purchase indicates intent |
| **Repeated interactions** | `view_a` twice = stronger interest, but NMF just sees count=2 |
| **Negative signals** | `remove_cart` gets aggregated away or becomes negative weight |
| **Session context** | Morning browse vs evening purchase have different meanings |

**Example of information loss:**
```python
# These two customers have IDENTICAL NMF representations:
customer_1: view_a → view_b → view_c → cart_c → purchase_c
customer_2: view_c → cart_c → view_b → view_a → purchase_c

# Both collapse to: {a: 1, b: 1, c: 3}  (with action weights)
# But customer_1 browsed then decided; customer_2 knew what they wanted
```

---

### 2. Singular Value Decomposition (SVD)

**How it works:**
```
R ≈ U × Σ × V^T
where:
  U = user latent factors
  Σ = singular values (importance weights)
  V = item latent factors
```

**Additional limitations beyond NMF:**
- Allows negative values (less interpretable)
- Requires complete matrix or imputation
- Assumes linear relationships

**Same fundamental problem:** Requires matrix form, loses sequence.

---

### 3. Principal Component Analysis (PCA)

**How it works:**
- Finds orthogonal directions of maximum variance
- Projects data onto lower-dimensional subspace

**Why it's even worse for funnel data:**
- Designed for continuous features, not discrete sequences
- Assumes Gaussian distribution
- Captures variance, not semantic similarity
- No notion of co-occurrence or context

---

## The Weighted Aggregation Workaround (Still Inadequate)

A common attempt to "save" traditional methods:

```python
def aggregate_sequence(sequence, weights):
    """Convert sequence to weighted item counts"""
    weights = {"view": 1, "add_cart": 3, "remove_cart": -2, "purchase": 5}
    item_scores = defaultdict(float)
    for event in sequence:
        item_scores[event["product"]] += weights[event["action"]]
    return item_scores
```

**Why this still fails:**

1. **Order is still lost**
   ```python
   # Same aggregated score, different intent:
   view_a → cart_a = cart_a → view_a = {a: 4}
   ```

2. **Negative weights are problematic**
   ```python
   # Remove after cart: {a: 3 + (-2) = 1}
   # But is this the same as just one view? No!
   view_a → cart_a → remove_a ≠ view_a
   ```

3. **Temporal decay is ad-hoc**
   ```python
   # Recent actions should matter more, but how much?
   # Any decay function is arbitrary without learning
   ```

4. **Action combinations have meaning**
   ```python
   # The PATTERN "view → cart → remove" is meaningful
   # But aggregation destroys the pattern
   ```

---

## Empirical Evidence

### Industry Benchmarks (Sequential vs Matrix Methods)

| Method | HR@10 | NDCG@10 | Notes |
|--------|-------|---------|-------|
| Popularity baseline | 0.05 | 0.03 | No personalization |
| **NMF** | 0.12 | 0.06 | Matrix method |
| **SVD** | 0.13 | 0.07 | Matrix method |
| Item-KNN | 0.15 | 0.08 | Uses co-occurrence |
| **Item2Vec** | 0.18 | 0.10 | Sequence-aware |
| **GRU4Rec** | 0.22 | 0.12 | Full sequence model |
| **SASRec** | 0.26 | 0.15 | Transformer |

*Source: Academic benchmarks on MovieLens, Amazon, Taobao datasets*

**Key insight:** Sequence-aware methods consistently outperform matrix methods by 50-100% on sequential recommendation tasks.

---

## Summary: When Traditional Methods Are Appropriate

| Scenario | Use Traditional? | Reason |
|----------|------------------|--------|
| Static user features (age, location) | Yes | No sequence to preserve |
| One-time ratings (5-star reviews) | Yes | Order doesn't matter |
| Aggregate statistics (total purchases) | Yes | Already aggregated |
| **Sequential interactions** | **No** | Order and actions matter |
| **Funnel data** | **No** | Action types have semantics |
| **Session-based behavior** | **No** | Context matters |

---

## Conclusion

For funnel data with:
- Temporal ordering
- Multiple action types
- Repeated interactions
- Negative signals (remove from cart)

**Traditional dimension reduction (NMF, SVD, PCA) is fundamentally inadequate.**

We need techniques designed for **sequential data** that can:
1. Capture local and global ordering
2. Learn action type semantics
3. Handle variable-length sequences
4. Produce interpretable representations

→ See [03-sequence-aware-techniques.md](./03-sequence-aware-techniques.md) for solutions.
