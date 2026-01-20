# 08 - References

## Academic Papers

### Sequential Recommendation

1. **SASRec: Self-Attentive Sequential Recommendation**
   - Kang, W.C., & McAuley, J. (2018)
   - ICDM 2018
   - [Paper](https://arxiv.org/abs/1808.09781)
   - Key contribution: Causal self-attention for next-item prediction

2. **BERT4Rec: Sequential Recommendation with Bidirectional Encoder Representations from Transformer**
   - Sun, F., et al. (2019)
   - CIKM 2019
   - [Paper](https://arxiv.org/abs/1904.06690)
   - Key contribution: Masked item prediction with bidirectional attention

3. **Session-based Recommendations with Recurrent Neural Networks (GRU4Rec)**
   - Hidasi, B., et al. (2015)
   - ICLR 2016
   - [Paper](https://arxiv.org/abs/1511.06939)
   - Key contribution: First successful application of RNNs to session recommendation

4. **Item2Vec: Neural Item Embedding for Collaborative Filtering**
   - Barkan, O., & Koenigstein, N. (2016)
   - RecSys 2016 Workshop
   - [Paper](https://arxiv.org/abs/1603.04259)
   - Key contribution: Word2Vec adaptation for item embeddings

### Dimension Reduction for Recommender Systems

5. **Application of Dimensionality Reduction in Recommender System - A Case Study**
   - Sarwar, B., et al. (2000)
   - ACM WebKDD Workshop
   - [Paper](https://files.grouplens.org/papers/webKDD00.pdf)
   - Key contribution: SVD for collaborative filtering

6. **Matrix Factorization Techniques for Recommender Systems**
   - Koren, Y., Bell, R., & Volinsky, C. (2009)
   - IEEE Computer
   - Key contribution: Comprehensive overview of MF methods

### Customer Journey Analysis

7. **Speaking with Actions - Learning Customer Journey Behavior**
   - ResearchGate, 2019
   - [Paper](https://www.researchgate.net/publication/331747008_Speaking_with_Actions_-_Learning_Customer_Journey_Behavior)
   - Key contribution: Sequence modeling for customer journeys

8. **Explainable Model Fusion for Customer Journey Mapping**
   - Frontiers in AI, 2022
   - [Paper](https://www.frontiersin.org/articles/10.3389/frai.2022.824197/full)
   - Key contribution: Interpretable journey analysis

### Autoencoders for Recommendation

9. **Variational Autoencoders for Collaborative Filtering**
   - Liang, D., et al. (2018)
   - WWW 2018
   - [Paper](https://arxiv.org/abs/1802.05814)
   - Key contribution: VAE for implicit feedback

10. **AutoRec: Autoencoders Meet Collaborative Filtering**
    - Sedhain, S., et al. (2015)
    - WWW 2015
    - Key contribution: First autoencoder for CF

---

## Industry Resources

### Technical Blogs

11. **Customer Journey Clustering - Ekimetrics**
    - How to use sequential modeling techniques for customer journey data
    - [Blog Post](https://ekimetrics.github.io/blog/2021/12/22/cjc/)
    - Key contribution: Practical implementation of journey embedding

12. **Introducing Melange: A Customer Journey Embedding System (Wayfair)**
    - Self-supervised representation learning for customer journeys
    - [Blog Post](https://www.aboutwayfair.com/careers/tech-blog/introducing-melange-a-customer-journey-embedding-system-for-improving-fraud-and-scam-detection)
    - Key contribution: Production-scale embedding system

13. **Decoding the Customer Journey with Graph Node Embeddings (Microsoft)**
    - Graph-based approach to customer journey analysis
    - [Blog Post](https://medium.com/data-science-at-microsoft/decoding-the-customer-journey-with-graph-node-embeddings-74eb983e9847)
    - Key contribution: Graph embeddings for journeys

14. **Item2Vec: Representation Learning for Customer Analytics (Grid Dynamics)**
    - Item2Vec and customer2vec for analytics
    - [Blog Post](https://www.griddynamics.com/blog/customer2vec-representation-learning-and-automl-for-customer-analytics-and-personalization)
    - Key contribution: Practical embedding applications

15. **Data-Driven Journey Optimization Using Deep Learning**
    - Towards Data Science
    - [Article](https://towardsdatascience.com/data-driven-journey-optimization-using-deep-learning-to-design-customer-journeys-93a3f8e92956/)
    - Key contribution: LSTM for journey modeling

### Survey Papers

16. **A Survey on Sequential Recommendation**
    - Frontiers of Computer Science, 2025
    - [Paper](https://link.springer.com/article/10.1007/s11704-025-41329-w)
    - Key contribution: Comprehensive overview of sequential methods

17. **A Comprehensive Review of Recommender Systems: Transitioning from Theory to Practice**
    - arXiv, 2024
    - [Paper](https://arxiv.org/html/2407.13699v1)
    - Key contribution: Traditional to modern techniques

18. **In-depth Survey: Deep Learning in Recommender Systems**
    - Neural Computing and Applications, 2024
    - [Paper](https://link.springer.com/article/10.1007/s00521-024-10866-z)
    - Key contribution: Deep learning methods comparison

---

## Libraries and Frameworks

### Embedding Training

19. **Gensim** - Word2Vec/Item2Vec implementation
    - [Documentation](https://radimrehurek.com/gensim/)
    - Used for: Item2Vec training

20. **Transformers4Rec** - NVIDIA's sequential recommendation library
    - [GitHub](https://github.com/NVIDIA-Merlin/Transformers4Rec)
    - Used for: Transformer-based models

### Dimension Reduction

21. **scikit-learn NMF** - Non-negative Matrix Factorization
    - [Documentation](https://scikit-learn.org/stable/modules/decomposition.html#nmf)
    - Used for: Trait decomposition

22. **UMAP** - Uniform Manifold Approximation and Projection
    - [Documentation](https://umap-learn.readthedocs.io/)
    - Used for: Embedding visualization

### Recommendation Frameworks

23. **RecBole** - Unified recommendation framework
    - [GitHub](https://github.com/RUCAIBox/RecBole)
    - Used for: Benchmarking and evaluation

24. **PyTorch Geometric** - Graph neural networks
    - [Documentation](https://pytorch-geometric.readthedocs.io/)
    - Used for: Graph-based recommendations

---

## Benchmark Datasets

### E-commerce

25. **Amazon Product Reviews**
    - [Dataset](https://jmcauley.ucsd.edu/data/amazon/)
    - Sequential purchase data

26. **Taobao User Behavior**
    - Alibaba dataset
    - Click, cart, purchase sequences

### Session-based

27. **Yoochoose (RecSys Challenge 2015)**
    - [Dataset](https://www.kaggle.com/chadgostopp/recsys-challenge-2015)
    - E-commerce click sequences

28. **Diginetica (CIKM Cup 2016)**
    - Session-based e-commerce data

### Entertainment

29. **MovieLens**
    - [Dataset](https://grouplens.org/datasets/movielens/)
    - Movie ratings with timestamps

30. **Netflix Prize Dataset**
    - Movie ratings dataset

---

## Key Findings Summary

| Topic | Key Reference | Main Insight |
|-------|---------------|--------------|
| Traditional limitations | Sarwar et al. (2000) | SVD loses sequence information |
| Item embeddings | Barkan & Koenigstein (2016) | Skip-gram works for item sequences |
| Session modeling | Hidasi et al. (2015) | RNNs capture session dynamics |
| Attention mechanisms | Kang & McAuley (2018) | Self-attention outperforms RNNs |
| Customer journeys | Ekimetrics (2021) | 3D image embeddings + autoencoders |
| Production systems | Wayfair (2023) | Self-supervised journey embeddings |
| Graph approaches | Microsoft (2022) | Node embeddings for journeys |

---

## Recommended Reading Order

For practitioners implementing this system:

1. **Start with**: Item2Vec paper (#4) - foundational technique
2. **Then**: Ekimetrics blog (#11) - practical implementation
3. **For depth**: SASRec paper (#1) - state-of-the-art alternative
4. **For production**: Wayfair blog (#12) - scale considerations
5. **For evaluation**: RecBole framework (#23) - benchmarking

---

## Citation Format

If using this research in academic work:

```bibtex
@misc{funnel_profiling_research_2025,
  title={Customer Profile Extraction from Funnel Data: Research Documentation},
  author={[Your Organization]},
  year={2025},
  howpublished={Internal Research Document}
}
```
