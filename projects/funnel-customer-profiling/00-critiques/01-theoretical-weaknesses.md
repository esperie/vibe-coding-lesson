# 01 - Theoretical Weaknesses

## Overview

This document examines the **fundamental assumptions** of the Item2Vec + NMF approach that may not hold for customer funnel data.

---

## 1. The Distributional Hypothesis Violation

### What the Approach Assumes

Item2Vec inherits Word2Vec's core assumption: **items appearing in similar contexts have similar meanings**.

In NLP: "dog" and "cat" appear in similar contexts ("The ___ sat on the mat") → they're semantically similar.

### Why This Fails for Funnel Data

**Severity: CRITICAL**

In e-commerce funnels, items in similar contexts often have **opposite meanings**:

```
Context: [view_expensive_item] → [view_???] → [cart_cheap_item]

Both scenarios produce identical context:
  Scenario A: view_expensive → view_similar_expensive → cart_cheap (comparison shopping)
  Scenario B: view_expensive → view_cheap_alternative → cart_cheap (price sensitivity)
```

The middle item could be:
- Another expensive item (customer comparing luxury options)
- A cheap alternative (customer seeking budget option)

These represent **opposite** purchase intents, but Item2Vec would learn similar embeddings.

### Real-World Example

```
Customer 1: view_iPhone → view_iPhone_case → cart_iPhone → buy_iPhone
Customer 2: view_iPhone → view_Android → cart_Android → buy_Android

In both cases, "view_iPhone" appears before a cart action.
Item2Vec learns: iPhone ≈ Android (similar contexts)
Reality: One customer is an Apple loyalist, one rejected Apple!
```

### The Core Problem

The distributional hypothesis works for language because word meanings are **relatively stable**.

Customer behavior is **contextual and dynamic**:
- The same action (view_product) means different things depending on what comes before/after
- Items are not words—their "meaning" depends on the customer's intent

---

## 2. Independence Assumption in Aggregation

### What the Approach Assumes

Mean/weighted aggregation assumes token embeddings are **independently combinable**:

```python
customer_embedding = mean([emb_1, emb_2, emb_3, ...])
```

This treats the customer journey as a **bag of actions** after the embedding step.

### Why This Fails

**Severity: CRITICAL**

Customer behavior is **compositional**, not additive:

```
Customer A: view_a → cart_a → buy_a
  Journey: Direct purchase (decisive)

Customer B: view_a → view_b → view_c → view_d → cart_a → buy_a
  Journey: Extensive comparison (careful researcher)
```

After mean aggregation:

```
Customer A: mean([emb_view_a, emb_cart_a, emb_buy_a])
Customer B: mean([emb_view_a, emb_view_b, emb_view_c, emb_view_d, emb_cart_a, emb_buy_a])
```

**Problems:**
1. Customer A's embedding is concentrated (3 actions)
2. Customer B's embedding is diluted across 6 actions
3. The **journey shape** (decisive vs. exploratory) is lost
4. The **proportion of intent** (80% browsing vs. 20% buying for Customer B) is lost

### What's Actually Lost

| Journey Feature | Captured? | Why Not |
|-----------------|-----------|---------|
| Which products were viewed | Partially | Through embeddings |
| Ratio of view/cart/buy | No | Mean treats all equally (or uses fixed weights) |
| Journey length | No | Normalized away |
| Journey "shape" (direct vs wandering) | No | Sequence structure lost |
| Hesitation patterns (cart → remove → cart) | No | Aggregated into single values |

---

## 3. NMF on Shifted Embeddings: Mathematical Unsoundness

### What the Approach Does

Item2Vec produces embeddings with **negative values**. NMF requires **non-negative** input.

The solution: shift all values by `min(C) + ε`:

```python
C_shifted = C - min(C) + epsilon  # Make all values positive
W, H = NMF(C_shifted)
```

### Why This is Problematic

**Severity: CRITICAL**

Negative values in embeddings **carry semantic information**. They indicate "away from" certain concepts.

**Example:**
```
Original embeddings (2D simplified):
  tech_product = [0.8, -0.3]  → "Strongly tech, weakly anti-fashion"
  fashion_product = [-0.2, 0.9]  → "Weakly anti-tech, strongly fashion"

Shifted embeddings (min = -0.3, shift by 0.31):
  tech_product = [1.11, 0.01]  → "Very something, barely something"
  fashion_product = [0.11, 1.21]  → "Barely something, very something"
```

**What changed:**
1. The **relative magnitudes** are distorted non-uniformly
2. The **semantic meaning** of dimensions is scrambled
3. NMF on shifted data finds different factors than it would on proper non-negative data

### The Geometry Problem

```
Before shift: Embeddings form meaningful clusters

              ↑ Dimension 2 (fashion)
              |     * fashion_a
              |   * fashion_b
    ──────────┼──────────→ Dimension 1 (tech)
     * tech_b |
       * tech_a

After uniform shift: Geometry preserved but...

              ↑ Dimension 2
              |     * fashion_a
              |   * fashion_b
              |
    ──────────┼──────────→ Dimension 1
              | * tech_b
              |   * tech_a

After NMF: Factors don't align with original semantics!
  - Factor 1 might mix tech + fashion
  - Interpretability is compromised
```

### Better Alternatives

1. **Non-negative embeddings from the start**: Use ReLU projections or non-negative Word2Vec variants
2. **Use SVD instead of NMF**: Accepts negative values, but loses non-negative interpretability
3. **Use VAE with non-negative decoder**: Learns proper non-negative representations

---

## 4. Loss of Temporal Decay Information

### What the Approach Does

Item2Vec treats all co-occurrences within the context window **equally**.

Recency weighting is applied **after** embedding learning:

```python
# Embeddings already learned without temporal info
weights[i] = decay^(n - i)  # Applied during aggregation
```

### Why This is Too Late

**Severity: MODERATE**

Temporal relationships should influence **what the embeddings learn**, not just how they're combined.

**Example:**
```
Sequence: view_A (t=0) → view_B (t=5sec) → view_A (t=10sec) → cart_A (t=15sec)

To Item2Vec (window=3):
  - view_A co-occurs with view_B and cart_A
  - view_B co-occurs with view_A and view_A
  - All co-occurrences weighted equally!

Reality:
  - view_A → cart_A (5 seconds apart) = strong purchase signal
  - view_A → view_B (5 seconds apart) = comparison browsing
  - These should have DIFFERENT co-occurrence strengths
```

### What's Actually Lost

| Temporal Feature | Captured? | Impact |
|------------------|-----------|--------|
| Time between actions | No | 5sec vs 5min have same weight |
| Session momentum | No | Rapid browsing vs slow consideration |
| Recency at embedding time | No | Only at aggregation time |
| Temporal patterns (morning vs evening) | No | Not modeled at all |

---

## 5. The "Sequence-Aware" Claim is Overstated

### What the Documentation Claims

> "Item2Vec captures sequence patterns via context window"
> "Sequence awareness: Item2Vec captures local order"

### The Reality

**Severity: CRITICAL**

Skip-gram's context window is **symmetric**:

```
Target word: cart_A
Context window (size 2):

Position: [view_A] [view_B] [cart_A] [view_C] [buy_A]
           ←─────────────→        ←──────────────→
           Left context           Right context

Skip-gram predicts BOTH directions equally!
  P(view_A | cart_A) ≈ P(buy_A | cart_A)
```

**What this means:**
- "view_A before cart_A" is learned the same as "view_A after cart_A"
- The model learns **co-occurrence**, not **precedence**
- Funnel sequences are inherently **causal/directed**, but Skip-gram ignores this

### Evidence from the Documentation Itself

From `03-sequence-aware-techniques.md`:

> "Symmetric context: Skip-gram doesn't distinguish 'before' vs 'after'"

This weakness is **acknowledged** but the recommended approach uses Skip-gram anyway!

### Better Alternatives

1. **Directional Skip-gram**: Only predict forward context
2. **Transformer with causal mask**: Explicitly models left-to-right
3. **LSTM/GRU**: Inherently directional

---

## Summary: Theoretical Foundation Rating

| Assumption | Validity | Severity |
|------------|----------|----------|
| Distributional hypothesis | Invalid for funnel data | Critical |
| Independence in aggregation | Invalid (behavior is compositional) | Critical |
| NMF on shifted embeddings | Mathematically problematic | Critical |
| Temporal information preserved | Lost during embedding | Moderate |
| "Sequence-aware" claim | Overstated (symmetric context) | Critical |

**Overall Theoretical Soundness: POOR**

The approach makes pragmatic engineering choices but lacks rigorous theoretical grounding. For a research publication, these issues would need to be addressed either through:
1. Formal analysis showing the approximations are acceptable
2. New methods that avoid these issues entirely
