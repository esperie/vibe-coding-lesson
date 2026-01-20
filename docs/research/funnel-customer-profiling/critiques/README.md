# Critical Analysis: Item2Vec + NMF Hybrid Approach

## Overview

This directory contains a rigorous, transparent critique of the recommended hybrid approach (Item2Vec + NMF) for customer profiling from funnel data. The goal is to identify weaknesses, explore alternatives, and uncover **novel research directions** worthy of publication.

---

## Navigation

| Document | Description |
|----------|-------------|
| [01-theoretical-weaknesses.md](./01-theoretical-weaknesses.md) | Fundamental assumptions that may not hold |
| [02-methodological-gaps.md](./02-methodological-gaps.md) | Implementation and design flaws |
| [03-alternative-approaches.md](./03-alternative-approaches.md) | Better techniques from recent literature |
| [04-novel-research-directions.md](./04-novel-research-directions.md) | **Potential thesis/paper topics** |

---

## Executive Summary

### Current Approach Verdict

| Aspect | Rating | Notes |
|--------|--------|-------|
| Production readiness | Good | Pragmatic, deployable |
| Theoretical soundness | **Poor** | Several fundamental issues |
| Novelty | **None** | Straightforward combination of existing methods |
| Publication potential | **Low** | Without significant additions |

### Critical Issues Found

| Issue | Severity | Impact |
|-------|----------|--------|
| Symmetric context windows lose directionality | **Critical** | Claim of "sequence awareness" is overstated |
| NMF on shifted embeddings is mathematically unsound | **Critical** | Distorts geometry, invalidates interpretation |
| Mean aggregation loses journey shape | **Critical** | Decisive vs. exploratory shoppers look identical |
| Independence assumption in aggregation | Moderate | Cross-token interactions ignored |
| Cold-start not actually solved | Moderate | Falls back to zero vectors |

### Path to Publication

The current approach is **not publishable as-is**. However, we identified several novel research directions:

1. **Directional Skip-gram** for causal sequences (methodological novelty)
2. **Disentangled Sequential VAE** for interpretable customer factors (theoretical novelty)
3. **seqNMF** adaptation for behavioral sequences (application novelty)
4. **Learned attention aggregation** with interpretability constraints (practical novelty)

See [04-novel-research-directions.md](./04-novel-research-directions.md) for detailed proposals.

---

## Why This Critique Matters

The original documentation presents the hybrid approach as a well-reasoned solution. This critique reveals:

1. **Hidden assumptions** that the documentation glosses over
2. **Information loss** at each pipeline stage
3. **Better alternatives** from recent literature (2023-2025)
4. **Research gaps** that could become thesis topics

---

## Methodology

This critique was conducted through:

1. **Deep analysis** of the proposed pipeline's mathematical properties
2. **Literature review** of 30+ papers on sequential recommendation, disentangled learning, and NMF variants
3. **Web search** for recent advances (2024-2025) in customer journey modeling
4. **Cross-referencing** with the original documentation's claims

---

## Key Sources for Alternatives

- [MacridVAE: Disentangled Recommendations](https://proceedings.neurips.cc/paper/2019/file/a2186aa7c086b46ad4e8bf81e2a3a19b-Paper.pdf) (NeurIPS 2019)
- [seqNMF: Temporal Sequence Discovery](https://elifesciences.org/articles/38471) (eLife 2019)
- [AI for Customer Journeys: A Transformer Approach](https://journals.sagepub.com/doi/10.1177/00222437251347268) (JMR 2026)
- [Attention-Based Aggregation](https://arxiv.org/html/2511.12723) (2024)
- [Knowledge-Guided Disentanglement](https://dl.acm.org/doi/10.1145/3464304) (TOIS 2021)

---

## Recommendations

### For Production Use
The current approach is acceptable with these caveats:
- Acknowledge the directionality limitation
- Build robust cold-start fallbacks
- Monitor for concept drift

### For Research/Publication
Do NOT proceed with the current approach. Instead:
1. Choose a novel direction from [04-novel-research-directions.md](./04-novel-research-directions.md)
2. Conduct proper ablation studies
3. Compare against state-of-the-art baselines (SASRec, BERT4Rec)
4. Provide theoretical analysis or large-scale empirical evidence

---

*Critique conducted: January 2025*
