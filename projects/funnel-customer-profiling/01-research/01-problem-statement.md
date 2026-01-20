# 01 - Problem Statement

## Objective

Extract customer profiles from **sequential funnel data** to create a recommender system. Unlike static measurements (demographics, one-time surveys), the input data captures the dynamic journey of customer interactions.

---

## The Data: Funnel Sequences

Customer behavior is captured as ordered sequences of actions:

```
Customer A: view_a → view_b → view_a → add_cart_a → view_c → view_d → remove_a → add_cart_d
Customer B: view_x → add_cart_x → purchase_x
Customer C: view_a → view_a → view_a → view_b → add_cart_b → purchase_b
```

### Key Characteristics

| Characteristic | Description | Example |
|----------------|-------------|---------|
| **Sequential** | Order matters | `view_a → cart_a` ≠ `cart_a → view_a` |
| **Variable length** | Different customers have different journey lengths | 3 events vs 500 events |
| **Multiple action types** | Different semantics per action | view, add_cart, remove_cart, purchase |
| **Repeated items** | Same product can appear multiple times | `view_a` appears twice |
| **Negative signals** | Some actions indicate disinterest | `remove_cart` is important! |
| **Session boundaries** | Natural breaks in customer journeys | 30-min inactivity gaps |

---

## The Goal: Interpretable Customer Components

Transform funnel sequences into **low-dimensional, interpretable customer profiles** that can be used for:

1. **Similarity-based recommendations** - find similar customers
2. **Customer segmentation** - cluster customers into archetypes
3. **Personalization** - tailor experiences based on traits
4. **Explainability** - understand WHY a recommendation was made

### Desired Output Format

```python
# Continuous trait vectors (k dimensions)
customer_profiles = {
    "customer_A": [0.15, 0.72, 0.13, 0.45, 0.88, ...],  # k scores
    "customer_B": [0.82, 0.11, 0.07, 0.33, 0.21, ...],
}

# Each dimension should have interpretable meaning:
# Dimension 0: "Tech enthusiasm"
# Dimension 1: "Price sensitivity"
# Dimension 2: "Impulse buying tendency"
# ...
```

---

## Requirements Summary

| Requirement | Priority | Notes |
|-------------|----------|-------|
| Preserve sequence information | **Critical** | Order of actions matters |
| Distinguish action types | **Critical** | view ≠ cart ≠ purchase |
| Handle negative signals | High | remove_cart indicates disinterest |
| Interpretable output | **High** | Each component should be explainable |
| Automatic weight learning | High | Don't hardcode action importance |
| Near real-time updates | Medium | Profile refresh within hours |
| Cold-start handling | Medium | New customers with few events |
| Scalable | Medium | Exploratory now, may scale later |

---

## Why This Matters

Traditional approaches that aggregate interactions into a user-item matrix lose critical information:

```
# What we have (rich sequential data):
Customer A: view_a(t=0) → view_b(t=5) → view_a(t=10) → cart_a(t=15) → remove_a(t=35) → cart_d(t=40)

# What traditional methods see (flattened):
Customer A × Products = {a: 2, b: 1, d: 1}

# What's lost:
- The fact that 'a' was viewed TWICE (strong interest signal)
- The add-to-cart then REMOVE pattern (reconsideration/rejection)
- The temporal proximity of events (browsing session vs return visit)
- The final choice of 'd' over 'a' (preference revelation)
```

The goal is to find a technique that preserves this richness while still producing interpretable, low-dimensional customer representations.

---

## Success Criteria

1. **Embedding quality**: Similar products should cluster together in embedding space
2. **Profile coherence**: Similar customers (by domain knowledge) should have similar profiles
3. **Interpretability**: Each component dimension should have a meaningful interpretation
4. **Recommendation quality**: Improved HR@10, NDCG@10 over baseline methods
5. **Actionability**: Profiles can be used for downstream tasks (segmentation, personalization)
