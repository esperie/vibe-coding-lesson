# 02 - Methodological Gaps

## Overview

Beyond theoretical issues, the Item2Vec + NMF pipeline has several **implementation and design flaws** that limit its effectiveness.

---

## 1. Arbitrary Session Boundaries

### The Current Approach

```python
timeout_minutes = 30  # Hardcoded
if time_gap > timeout_minutes * 60:
    new_session = True
```

### The Problems

**Severity: MODERATE**

1. **No theoretical justification** for 30 minutes
2. **User-dependent patterns ignored**:
   - Mobile users: Short, fragmented sessions
   - Desktop users: Long, continuous sessions
   - Multi-device users: Sessions that span devices appear as separate
3. **Domain-dependent variation**:
   - Grocery shopping: Quick decisions (5-10 min sessions)
   - Furniture shopping: Long deliberation (hours/days)
4. **No learning**: The boundary is fixed, not adapted from data

### Impact

```
True customer journey:
  Day 1: view_sofa (research)
  Day 2: view_sofa, view_table (more research)
  Day 3: cart_sofa, buy_sofa (purchase)

With 30-min rule:
  Session 1: [view_sofa]
  Session 2: [view_sofa, view_table]
  Session 3: [cart_sofa, buy_sofa]

Lost: The connection between research sessions and purchase decision
```

### Better Approaches

1. **Learned session boundaries**: Use change-point detection
2. **Hierarchical modeling**: Session-level → User-level
3. **Sensitivity analysis**: Test multiple thresholds
4. **Domain-specific tuning**: Different thresholds for different product categories

---

## 2. Minimum Count Threshold Creates Silent Failures

### The Current Approach

```python
model = Word2Vec(
    sentences=sequences,
    min_count=5,  # Tokens appearing < 5 times are ignored
)
```

### The Problems

**Severity: MODERATE**

1. **Long-tail products excluded**: Niche products that appear 1-4 times have no embeddings
2. **New products invisible**: Products launched recently are filtered out
3. **Rare but informative actions lost**: `buy_luxury_item` might appear rarely but is highly informative
4. **Silent degradation**: No warning when a token is filtered

### Impact Analysis

In a typical e-commerce catalog:
- 80% of products may have < 5 interactions (long tail)
- These products return zero vectors or fallback embeddings
- Customer profiles become biased toward popular products

### Interaction with Cold-Start "Solution"

The documentation mentions "product category fallback":

```python
# Vague specification
def get_fallback_embedding(token):
    category = get_product_category(token)
    return category_embedding_map.get(category, zero_vector)
```

**Problems with this fallback:**
1. Category embeddings are not defined in the pipeline
2. How are category embeddings computed? Average of category products?
3. If most category products are also filtered, the fallback is also empty

---

## 3. TF-IDF Weighting is Borrowed Without Validation

### The Current Approach

```python
# Option B: TF-IDF weighted mean
idf = np.log(len(model.wv) / (df + 1))
weights.append(idf)
```

### The Problems

**Severity: MINOR**

TF-IDF was designed for **document retrieval** with specific assumptions:
- Rare terms are discriminative (true for documents)
- Term frequency indicates importance (true for documents)

**For funnel data, these assumptions may not hold:**

| TF-IDF Assumption | Document Retrieval | Funnel Data |
|-------------------|--------------------| ------------|
| Rare terms are important | Usually true | Not always (rare = niche, not discriminative) |
| Frequency = importance | Usually true | Not always (view_same_product × 10 = indecision?) |
| Terms are independent | Roughly true | False (action sequences have structure) |

### Missing Validation

The documentation does not:
1. Compare TF-IDF vs. uniform vs. recency weighting empirically
2. Provide theoretical justification for TF-IDF in this context
3. Consider learned weighting as the default

### Better Approaches

1. **Learned attention weights**: Let the model discover what matters
2. **Action-type weighting**: Weight by action type (cart > view) with learned coefficients
3. **Empirical comparison**: A/B test different weighting schemes

---

## 4. Fixed Aggregation vs. Learned Aggregation

### The Current Approach

Three options, all **fixed a priori**:
- Mean
- TF-IDF weighted mean
- Recency weighted mean

### The Critical Gap

**Severity: CRITICAL FOR NOVELTY**

The aggregation function is **not learned** from data. This is a major missed opportunity.

**What could be learned:**
1. Which actions matter more (view vs. cart vs. buy)
2. How position in sequence affects importance
3. How repeated interactions should be weighted
4. Cross-token interactions (patterns like view→cart→remove)

### State-of-the-Art: Attention-Based Aggregation

From recent literature ([Attention-Based Aggregation Module](https://www.emergentmind.com/topics/attention-based-aggregation-module)):

> "Attention-Pooling Connectors employ learnable weighting mechanisms to replace fixed pooling, thereby enhancing efficiency, adaptivity, and model interpretability."

```python
# Fixed aggregation (current approach)
customer_emb = mean(token_embeddings)

# Learned aggregation (better)
attention_weights = softmax(W @ token_embeddings.T)  # Learnable W
customer_emb = attention_weights @ token_embeddings
```

**Benefits of learned aggregation:**
1. Automatically discovers what matters
2. Can capture cross-token interactions
3. Attention weights provide interpretability ("this purchase was driven by...")

---

## 5. Two-Stage Pipeline Loses End-to-End Learning

### The Current Approach

```
Stage 1: Train Item2Vec (separate objective)
Stage 2: Aggregate embeddings (fixed function)
Stage 3: Apply NMF (separate objective)
```

Each stage is optimized **independently**.

### The Problems

**Severity: MODERATE**

1. **No joint optimization**: Item2Vec doesn't know embeddings will be aggregated and factorized
2. **Objective mismatch**: Item2Vec optimizes for co-occurrence prediction, not customer profiling
3. **Error propagation**: Errors in Stage 1 are not corrected by later stages
4. **Suboptimal embeddings**: Embeddings might be good for similarity search but bad for NMF

### End-to-End Alternative

```python
# Joint model (conceptual)
class CustomerProfiler(nn.Module):
    def __init__(self):
        self.item_embedding = nn.Embedding(n_tokens, d_model)
        self.attention_aggregator = AttentionPool(d_model)
        self.trait_decoder = nn.Linear(d_model, n_traits)  # Replaces NMF

    def forward(self, customer_tokens):
        token_embs = self.item_embedding(customer_tokens)
        customer_emb = self.attention_aggregator(token_embs)
        traits = F.softmax(self.trait_decoder(customer_emb), dim=-1)
        return traits

# Train end-to-end with reconstruction or contrastive loss
```

**Benefits:**
1. All components optimize for the same goal
2. Gradients flow through the entire pipeline
3. Embeddings adapt to downstream task

---

## 6. Cold-Start Handling is Inadequate

### The Documentation Claims

> "Fast updates: Embeddings fixed; only aggregation updates per customer"
> "Cold-start handling via product category fallback"

### The Reality

**Severity: MODERATE**

**For new customers (no history):**
```python
if len(customer_tokens) == 0:
    return get_average_profile()  # Generic, non-personalized
```

**For new products (no embedding):**
```python
if token not in model.wv:
    return category_fallback(token)  # Undefined category embeddings
```

### What's Actually Needed

| Cold-Start Scenario | Current Solution | Better Solution |
|---------------------|------------------|-----------------|
| New customer, no actions | Average profile | Use demographic features, or similar user collaborative filtering |
| New customer, few actions | Normal pipeline | Special small-sample model |
| New product | Category fallback (vague) | Product content features, or meta-learning |
| New action type | Not addressed | Graceful degradation |

### Comparison with Alternatives

Collaborative filtering can use **user-user similarity** for cold-start:
- "This new user looks like users X, Y, Z based on their first few actions"
- Provides personalization even with minimal history

The proposed approach **cannot do this** because it treats each customer independently.

---

## 7. No Handling of Negative Interactions

### The Current Approach

`remove_cart` is tokenized as a separate action:

```python
tokens = ["view_a", "cart_a", "remove_a", "cart_b"]
```

### The Problems

**Severity: MODERATE**

1. **No explicit negative modeling**: `remove_a` is just another token
2. **Learned implicitly**: Skip-gram might learn `remove_a` is different from `cart_a`, but not guaranteed
3. **Aggregation doesn't distinguish**: Mean of [emb_cart_a, emb_remove_a] might cancel out or not

### What Negative Signals Mean

```
cart_a → remove_a = "Considered A, rejected it"

This is DIFFERENT from:
- Never viewing A (no information)
- Viewing A once (mild interest)
- Viewing A and not carting (browsed but passed)
```

### Better Approaches

1. **Explicit negative sampling**: Train embeddings to push apart cart and remove
2. **Signed embeddings**: Positive for add, negative for remove
3. **Separate encoding**: Positive and negative interaction channels

---

## 8. Scalability Concerns for Power Users

### The Scenario

Power users may have thousands of interactions:

```
power_user_tokens = [token_1, token_2, ..., token_5000]
```

### The Problems

**Severity: MODERATE**

1. **Item2Vec context window is local**: Window of 5-10 misses global patterns
2. **Mean aggregation dilutes**: Mean of 5000 embeddings → generic central vector
3. **Central Limit Theorem effect**: Large averages converge to population mean
4. **Memory for aggregation**: Storing all tokens per user

### Evidence

```python
# Simulated effect
import numpy as np

# Short journey: 5 tokens
short_emb = np.random.randn(5, 128).mean(axis=0)
print(f"Short journey variance: {np.var(short_emb):.4f}")

# Long journey: 5000 tokens
long_emb = np.random.randn(5000, 128).mean(axis=0)
print(f"Long journey variance: {np.var(long_emb):.4f}")

# Long journeys converge to zero! (CLT)
```

### Better Approaches

1. **Hierarchical aggregation**: Session-level → User-level
2. **Attention with sparsity**: Focus on most important tokens
3. **Recency truncation**: Only use last N tokens
4. **Reservoir sampling**: Maintain representative sample

---

## Summary: Methodological Gap Severity

| Gap | Severity | Fix Difficulty |
|-----|----------|----------------|
| Arbitrary session boundaries | Moderate | Easy (sensitivity analysis) |
| Min-count threshold | Moderate | Medium (fallback design) |
| TF-IDF borrowed without validation | Minor | Easy (ablation study) |
| Fixed vs. learned aggregation | Critical | Medium (architectural change) |
| Two-stage pipeline | Moderate | Hard (full redesign) |
| Cold-start handling | Moderate | Medium (additional models) |
| Negative interaction handling | Moderate | Medium (encoding change) |
| Power user scalability | Moderate | Medium (hierarchical aggregation) |

**Overall Methodological Soundness: MODERATE**

The approach makes reasonable engineering choices but misses opportunities for improvement. For a research publication, at minimum the aggregation mechanism should be learned rather than fixed.
