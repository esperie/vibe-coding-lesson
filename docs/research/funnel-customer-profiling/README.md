# Customer Profile Extraction from Funnel Data

## Research Documentation

This directory contains comprehensive research on dimension reduction techniques for extracting customer profiles from sequential funnel data (e.g., view → add-to-cart → remove → purchase sequences) for building a recommender system.

---

## Navigation

### Start Here (Beginner-Friendly)

| Document | Description |
|----------|-------------|
| [00-lesson-for-beginners.md](./00-lesson-for-beginners.md) | **START HERE** - Easy-to-understand lesson with analogies and visuals |

### Critical Analysis & Novel Directions

| Document | Description |
|----------|-------------|
| [critiques/README.md](./critiques/README.md) | **Critical review** of the recommended approach |
| [critiques/04-novel-research-directions.md](./critiques/04-novel-research-directions.md) | **Potential thesis/paper topics** |

### Technical Deep-Dives

| Document | Description |
|----------|-------------|
| [01-problem-statement.md](./01-problem-statement.md) | Problem definition and requirements |
| [02-why-traditional-methods-fail.md](./02-why-traditional-methods-fail.md) | Why NMF/SVD/PCA don't work for sequential data |
| [03-sequence-aware-techniques.md](./03-sequence-aware-techniques.md) | Modern techniques: Item2Vec, Transformers, VAEs |
| [04-technique-comparison.md](./04-technique-comparison.md) | Detailed comparison matrix and benchmarks |
| [05-recommended-approach.md](./05-recommended-approach.md) | The hybrid Item2Vec + NMF solution |
| [06-data-structure-requirements.md](./06-data-structure-requirements.md) | How to structure and preprocess funnel data |
| [07-implementation-considerations.md](./07-implementation-considerations.md) | Practical concerns: scale, latency, cold-start |
| [08-references.md](./08-references.md) | Academic papers and industry sources |

---

## Quick Summary

### The Problem
Traditional dimension reduction (NMF, SVD) **cannot** properly handle funnel data because they collapse sequences into flat matrices, losing:
- Temporal ordering
- Action type semantics (view vs cart vs remove)
- Repeated interaction patterns
- Negative signals (remove from cart)

### The Solution
A **hybrid approach** combining:
1. **Item2Vec** - learns sequence-aware embeddings from action-item pairs
2. **NMF** - decomposes customer embeddings into interpretable traits

### Output Format
Continuous trait vectors suitable for similarity-based recommendations:
```python
customer_A = [0.15, 0.72, 0.13, ...]  # k-dimensional trait scores
```

---

## User Requirements (Gathered)

| Requirement | Value |
|-------------|-------|
| Data Scale | Exploratory (flexible approach needed) |
| Interpretability | **High** (must explain components) |
| Action Weights | Learn automatically from data |
| Deployment | Near real-time (updates within hours) |
| Output Format | Continuous traits for similarity operations |

---

## Key Insight

```
Traditional NMF:
  view_a → view_b → cart_a → remove_a → cart_d
                    ↓ collapses to ↓
  {a: 1, b: 1, d: 1}  # Lost: order, action types, remove signal!

Recommended Hybrid:
  view_a → view_b → cart_a → remove_a → cart_d
                    ↓ becomes ↓
  ["view_a", "view_b", "cart_a", "remove_a", "cart_d"]
                    ↓ Item2Vec ↓
  [embedding vectors that capture sequence context]
                    ↓ NMF ↓
  [interpretable trait dimensions]
```

---

## Research Date
January 2025

## Status
Research complete. Awaiting user approval to proceed with implementation.
