# 04 - Technique Comparison

## Detailed Capability Matrix

### Scoring Key
- 1 = Poor / Not supported
- 2 = Limited / Workaround needed
- 3 = Moderate / Basic support
- 4 = Good / Well supported
- 5 = Excellent / Native support

---

## Core Capabilities

| Technique | Temporal Order | Action Types | Repeated Items | Variable Length | Total |
|-----------|---------------|--------------|----------------|-----------------|-------|
| **NMF** | 1 | 2 | 2 | N/A | 5 |
| **SVD** | 1 | 2 | 2 | N/A | 5 |
| **PCA** | 1 | 1 | 1 | N/A | 3 |
| **Item2Vec** | 3 | 3* | 4 | 4 | 14 |
| **GRU4Rec** | 5 | 4 | 4 | 5 | 18 |
| **LSTM** | 5 | 4 | 4 | 5 | 18 |
| **SASRec** | 5 | 4 | 5 | 4 | 18 |
| **BERT4Rec** | 4 | 4 | 5 | 4 | 17 |
| **Seq-VAE** | 4 | 4 | 4 | 4 | 16 |
| **GNN** | 3 | 4 | 4 | 4 | 15 |

*Item2Vec action support requires action-item pair tokenization

---

## Operational Characteristics

| Technique | Interpretability | Training Speed | Inference Speed | Cold Start | Total |
|-----------|-----------------|----------------|-----------------|------------|-------|
| **NMF** | 5 | 5 | 5 | 2 | 17 |
| **SVD** | 4 | 5 | 5 | 2 | 16 |
| **PCA** | 4 | 5 | 5 | 3 | 17 |
| **Item2Vec** | 4 | 4 | 5 | 3 | 16 |
| **GRU4Rec** | 2 | 3 | 3 | 2 | 10 |
| **LSTM** | 2 | 3 | 3 | 2 | 10 |
| **SASRec** | 3 | 3 | 4 | 2 | 12 |
| **BERT4Rec** | 3 | 2 | 3 | 2 | 10 |
| **Seq-VAE** | 3 | 2 | 3 | 3 | 11 |
| **GNN** | 2 | 2 | 3 | 3 | 10 |

---

## Combined Score Analysis

| Technique | Core Capability | Operational | **Combined** | Notes |
|-----------|----------------|-------------|--------------|-------|
| NMF | 5 | 17 | 22 | Good ops, bad for sequences |
| SVD | 5 | 16 | 21 | Same as NMF |
| PCA | 3 | 17 | 20 | Worst for sequences |
| **Item2Vec** | 14 | 16 | **30** | Best balance |
| GRU4Rec | 18 | 10 | 28 | Good capability, slow |
| LSTM | 18 | 10 | 28 | Similar to GRU |
| **SASRec** | 18 | 12 | **30** | Best if compute available |
| BERT4Rec | 17 | 10 | 27 | Overkill for most cases |
| Seq-VAE | 16 | 11 | 27 | Good for generation |
| GNN | 15 | 10 | 25 | Complex setup |

---

## Performance Benchmarks (Industry Data)

### Next-Item Prediction (MovieLens 1M)

| Model | HR@10 | NDCG@10 | MRR |
|-------|-------|---------|-----|
| Pop | 0.0513 | 0.0265 | 0.0189 |
| Item-KNN | 0.1523 | 0.0823 | 0.0612 |
| NMF | 0.1198 | 0.0612 | 0.0445 |
| BPR-MF | 0.1356 | 0.0701 | 0.0521 |
| Item2Vec | 0.1812 | 0.0956 | 0.0723 |
| GRU4Rec | 0.2156 | 0.1145 | 0.0867 |
| **SASRec** | **0.2589** | **0.1423** | **0.1089** |
| BERT4Rec | 0.2512 | 0.1378 | 0.1045 |

### Session-Based Recommendation (Yoochoose)

| Model | Recall@20 | MRR@20 |
|-------|-----------|--------|
| Item-KNN | 0.5123 | 0.2156 |
| GRU4Rec | 0.6078 | 0.2512 |
| NARM | 0.6189 | 0.2623 |
| **SASRec** | **0.6456** | **0.2812** |
| SR-GNN | 0.6389 | 0.2756 |

### E-commerce Click Prediction (Taobao)

| Model | AUC | Log Loss |
|-------|-----|----------|
| DIN (attention) | 0.8012 | 0.4523 |
| DIEN (sequence) | 0.8156 | 0.4389 |
| **BST (transformer)** | **0.8234** | **0.4289** |

---

## Specific Use Case Analysis: Funnel Data

### Requirements Match

| Requirement | Best Techniques |
|-------------|-----------------|
| Preserve sequence order | SASRec, GRU4Rec, LSTM |
| Action type semantics | All (with proper embedding) |
| Handle remove_cart signal | Transformer (learned), Item2Vec (tokenized) |
| High interpretability | Item2Vec, NMF (as second stage) |
| Automatic weight learning | Transformer (attention), Item2Vec (embedding) |
| Near real-time updates | Item2Vec (fast), Transformer (batch) |

### Trade-off Analysis

```
                    Interpretability
                          ^
                          |
              NMF  *      |
                          |      * Item2Vec + NMF (Recommended)
                          |
                    * PCA |        * Item2Vec
                          |
                          |              * Seq-VAE
                          |
                          +---------------------> Sequence Modeling
                                    * GRU4Rec
                                         * SASRec
                                              * BERT4Rec
```

---

## Handling Specific Challenges

### Challenge 1: Different Action Types

| Technique | Approach | Effectiveness |
|-----------|----------|---------------|
| NMF | Weighted aggregation | Poor (loses semantics) |
| Item2Vec | Action-item tokens | Good (separate embeddings) |
| Transformer | Separate embedding + combination | Excellent (learned) |

```python
# Item2Vec approach
tokens = ["view_productA", "cart_productA", "remove_productA"]

# Transformer approach
event_emb = item_emb + action_emb + pos_emb
```

### Challenge 2: Remove from Cart (Negative Signal)

| Technique | Approach | Effectiveness |
|-----------|----------|---------------|
| NMF | Negative weight | Poor (arbitrary) |
| Item2Vec | "remove_X" token | Good (learned implicitly) |
| Transformer | Action embedding | Excellent (learned directly) |

### Challenge 3: Repeated Items

| Technique | Approach | Effectiveness |
|-----------|----------|---------------|
| NMF | Count aggregation | Poor (just count) |
| Item2Vec | Each occurrence as separate token | Good |
| Transformer | Attention accumulation | Excellent |

```python
# Sequence: view_a, view_b, view_a, cart_a
# Item2Vec: "view_a" appears twice, contributes twice to embedding
# Transformer: Second "view_a" attends to first, learns repetition pattern
```

### Challenge 4: Variable Sequence Length

| Technique | Approach | Max Length Support |
|-----------|----------|-------------------|
| NMF | N/A (matrix) | Unlimited (aggregated) |
| Item2Vec | Sliding window | Unlimited (windowed) |
| GRU/LSTM | Native | Unlimited (memory constrained) |
| Transformer | Truncation/padding | Fixed (typically 50-200) |

---

## Recommendation Summary

### For This Use Case (High Interpretability + Sequence Awareness)

**Primary: Hybrid Item2Vec + NMF**
- Item2Vec captures sequence patterns with action-item tokens
- NMF provides interpretable dimension reduction
- Best balance of interpretability and sequence modeling

**Alternative: SASRec (if interpretability can be relaxed)**
- Best raw performance
- Attention visualization provides some interpretability
- Higher compute and complexity

**Avoid: Pure NMF/SVD/PCA**
- Fundamentally cannot handle sequences
- Will lose critical information

→ See [05-recommended-approach.md](./05-recommended-approach.md) for implementation details.
