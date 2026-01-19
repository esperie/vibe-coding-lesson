# 07 - Implementation Considerations

## Overview

This document covers practical concerns for implementing the hybrid Item2Vec + NMF approach in a production environment.

---

## Scale Considerations

### Data Volume Tiers

| Tier | Events | Users | Products | Approach |
|------|--------|-------|----------|----------|
| **Small** | <100K | <10K | <1K | Single machine, in-memory |
| **Medium** | 100K-10M | 10K-1M | 1K-100K | Single machine, batch processing |
| **Large** | 10M-1B | 1M-100M | 100K+ | Distributed, incremental |

### Resource Requirements (Medium Tier)

| Component | Memory | CPU | Time |
|-----------|--------|-----|------|
| Data preprocessing | 4-8 GB | 4 cores | 10-30 min |
| Item2Vec training | 8-16 GB | 8 cores | 1-4 hours |
| Customer aggregation | 8-16 GB | 4 cores | 30-60 min |
| NMF decomposition | 4-8 GB | 4 cores | 10-30 min |

---

## Computational Complexity

### Item2Vec (Word2Vec)

```
Training: O(V × D × W × N × E)
  V = vocabulary size (action-item pairs)
  D = embedding dimension
  W = context window size
  N = total tokens in corpus
  E = epochs

Inference (lookup): O(1)
```

### Customer Aggregation

```
Per customer: O(T × D)
  T = tokens per customer
  D = embedding dimension

Total: O(C × T_avg × D)
  C = number of customers
  T_avg = average tokens per customer
```

### NMF

```
Training: O(C × D × K × I)
  C = number of customers
  D = embedding dimension
  K = number of components
  I = iterations

Per iteration: O(C × D × K)
```

---

## Cold Start Handling

### New Customers (No History)

```python
def handle_cold_start_customer(customer_id, default_profile=None):
    """Handle customers with no or insufficient history."""

    customer_tokens = get_customer_tokens(customer_id)

    if len(customer_tokens) == 0:
        # No history: use population average
        return get_average_profile()

    if len(customer_tokens) < 3:
        # Very short history: use category-based fallback
        return get_category_based_profile(customer_tokens)

    # Sufficient history: normal processing
    return compute_profile(customer_tokens)


def get_category_based_profile(tokens):
    """Fallback using product categories instead of specific products."""

    category_embeddings = []
    for token in tokens:
        product_id = extract_product_id(token)
        category = get_product_category(product_id)
        if category in category_embedding_map:
            category_embeddings.append(category_embedding_map[category])

    if category_embeddings:
        return aggregate_embeddings(category_embeddings)

    return get_average_profile()
```

### New Products (No Embedding)

```python
def get_product_embedding(token, model, fallback_strategy='category'):
    """Get embedding for token, with fallback for unseen products."""

    if token in model.wv:
        return model.wv[token]

    if fallback_strategy == 'category':
        # Use category average
        product_id = extract_product_id(token)
        category = get_product_category(product_id)
        category_tokens = [t for t in model.wv.key_to_index if category in t]
        if category_tokens:
            return np.mean([model.wv[t] for t in category_tokens], axis=0)

    if fallback_strategy == 'action':
        # Use action average
        action = extract_action(token)
        action_tokens = [t for t in model.wv.key_to_index if t.startswith(action)]
        if action_tokens:
            return np.mean([model.wv[t] for t in action_tokens], axis=0)

    # Ultimate fallback: zero vector
    return np.zeros(model.vector_size)
```

---

## Update Strategies

### Near Real-Time Profile Updates

For updates within hours (as required):

```python
class CustomerProfileUpdater:
    """Efficient profile updates without retraining."""

    def __init__(self, item2vec_model, nmf_model, trait_embeddings):
        self.item2vec = item2vec_model
        self.nmf = nmf_model
        self.H = trait_embeddings  # (k, d) from NMF

    def update_profile(self, customer_id, new_events):
        """Update a single customer's profile with new events."""

        # Get existing tokens
        existing_tokens = get_customer_tokens(customer_id)

        # Add new tokens
        new_tokens = [tokenize_event(e) for e in new_events]
        all_tokens = existing_tokens + new_tokens

        # Recompute embedding (fast: just lookup and aggregate)
        embedding = self.aggregate_tokens(all_tokens)

        # Project to trait space using pre-computed NMF components
        # W_new = argmin ||C_new - W_new × H||
        # Closed form: W_new = C_new × H^T × (H × H^T)^{-1}
        profile = self.project_to_traits(embedding)

        # Save updated profile
        save_customer_profile(customer_id, profile)

        return profile

    def aggregate_tokens(self, tokens):
        """Aggregate token embeddings."""
        embeddings = [
            get_product_embedding(t, self.item2vec)
            for t in tokens
        ]
        return np.mean(embeddings, axis=0)

    def project_to_traits(self, embedding):
        """Project embedding to trait space using NMF components."""
        # Shift to non-negative
        embedding_shifted = embedding - embedding.min() + 1e-6

        # Solve: embedding ≈ profile × H
        # Using non-negative least squares
        from scipy.optimize import nnls
        profile, _ = nnls(self.H.T, embedding_shifted)

        # Normalize
        profile = profile / (profile.sum() + 1e-6)

        return profile.tolist()
```

### Batch Retraining Schedule

| Component | Frequency | Trigger | Duration |
|-----------|-----------|---------|----------|
| Item2Vec | Weekly | New products > 5% | 2-4 hours |
| Customer aggregation | Daily | Any new events | 30-60 min |
| NMF | Weekly | After Item2Vec retrain | 30 min |

```python
def should_retrain_item2vec(current_vocab, new_tokens, threshold=0.05):
    """Determine if Item2Vec needs retraining."""
    new_unique = set(new_tokens) - set(current_vocab)
    new_ratio = len(new_unique) / len(current_vocab)
    return new_ratio > threshold
```

---

## Latency Optimization

### Embedding Lookup Optimization

```python
import numpy as np
from functools import lru_cache

class EmbeddingCache:
    """Optimized embedding lookup with caching."""

    def __init__(self, model):
        # Pre-convert to numpy array for faster lookup
        self.vocab = list(model.wv.key_to_index.keys())
        self.embeddings = np.array([model.wv[t] for t in self.vocab])
        self.token_to_idx = {t: i for i, t in enumerate(self.vocab)}

    def get(self, token):
        idx = self.token_to_idx.get(token)
        if idx is not None:
            return self.embeddings[idx]
        return None

    def batch_get(self, tokens):
        """Get embeddings for multiple tokens at once."""
        indices = [self.token_to_idx.get(t) for t in tokens]
        valid_indices = [i for i in indices if i is not None]
        if valid_indices:
            return self.embeddings[valid_indices]
        return np.array([])
```

### Profile Caching

```python
import redis
import json

class ProfileCache:
    """Redis-based profile caching."""

    def __init__(self, redis_url, ttl_hours=24):
        self.redis = redis.from_url(redis_url)
        self.ttl = ttl_hours * 3600

    def get_profile(self, customer_id):
        cached = self.redis.get(f"profile:{customer_id}")
        if cached:
            return json.loads(cached)
        return None

    def set_profile(self, customer_id, profile):
        self.redis.setex(
            f"profile:{customer_id}",
            self.ttl,
            json.dumps(profile)
        )

    def get_or_compute(self, customer_id, compute_fn):
        profile = self.get_profile(customer_id)
        if profile is None:
            profile = compute_fn(customer_id)
            self.set_profile(customer_id, profile)
        return profile
```

---

## Monitoring and Validation

### Embedding Quality Metrics

```python
def evaluate_embedding_quality(model, test_pairs):
    """
    Evaluate Item2Vec embedding quality.

    test_pairs: List of (token_a, token_b, expected_similarity)
    """
    from scipy.stats import spearmanr

    predicted_sims = []
    expected_sims = []

    for token_a, token_b, expected in test_pairs:
        if token_a in model.wv and token_b in model.wv:
            predicted = model.wv.similarity(token_a, token_b)
            predicted_sims.append(predicted)
            expected_sims.append(expected)

    correlation, p_value = spearmanr(predicted_sims, expected_sims)

    return {
        'spearman_correlation': correlation,
        'p_value': p_value,
        'n_pairs': len(predicted_sims),
    }
```

### Profile Coherence Metrics

```python
def evaluate_profile_coherence(profiles, customer_segments):
    """
    Check if customers in same segment have similar profiles.

    customer_segments: Dict mapping customer_id to known segment
    """
    from sklearn.metrics import silhouette_score
    from collections import defaultdict

    # Group profiles by segment
    segment_profiles = defaultdict(list)
    for customer_id, profile in profiles.items():
        segment = customer_segments.get(customer_id)
        if segment:
            segment_profiles[segment].append(profile)

    # Compute within-segment vs between-segment similarity
    profile_matrix = np.array(list(profiles.values()))
    labels = [customer_segments.get(cid, 'unknown') for cid in profiles.keys()]

    # Filter to known segments
    mask = [l != 'unknown' for l in labels]
    if sum(mask) > 10:
        filtered_profiles = profile_matrix[mask]
        filtered_labels = [l for l, m in zip(labels, mask) if m]

        silhouette = silhouette_score(filtered_profiles, filtered_labels)
    else:
        silhouette = None

    return {
        'silhouette_score': silhouette,
        'n_customers_with_segments': sum(mask),
    }
```

### Drift Detection

```python
def detect_embedding_drift(old_model, new_model, sample_tokens, threshold=0.1):
    """
    Detect if embeddings have drifted significantly.
    """
    from scipy.spatial.distance import cosine

    drifts = []
    for token in sample_tokens:
        if token in old_model.wv and token in new_model.wv:
            old_emb = old_model.wv[token]
            new_emb = new_model.wv[token]
            drift = cosine(old_emb, new_emb)
            drifts.append(drift)

    mean_drift = np.mean(drifts) if drifts else 0

    return {
        'mean_drift': mean_drift,
        'max_drift': max(drifts) if drifts else 0,
        'drift_detected': mean_drift > threshold,
        'n_tokens_compared': len(drifts),
    }
```

---

## Error Handling

### Graceful Degradation

```python
class RobustProfiler:
    """Profile computation with graceful degradation."""

    def __init__(self, item2vec_model, fallback_profiles):
        self.model = item2vec_model
        self.fallback = fallback_profiles  # Category-based defaults

    def get_profile(self, customer_id):
        try:
            tokens = get_customer_tokens(customer_id)

            if not tokens:
                return self.fallback['no_history']

            # Attempt full computation
            embedding = self.compute_embedding(tokens)
            profile = self.compute_profile(embedding)

            return profile

        except KeyError as e:
            # Unknown token
            logger.warning(f"Unknown token for {customer_id}: {e}")
            return self.get_fallback_profile(customer_id)

        except Exception as e:
            # Unexpected error
            logger.error(f"Profile computation failed for {customer_id}: {e}")
            return self.fallback['default']

    def get_fallback_profile(self, customer_id):
        """Get fallback based on available information."""
        # Try category-based
        categories = get_customer_categories(customer_id)
        if categories:
            return self.fallback.get(categories[0], self.fallback['default'])
        return self.fallback['default']
```

---

## Testing Strategy

### Unit Tests

```python
def test_tokenization():
    """Test event tokenization."""
    event = {"action": "view", "product_id": "prod_001"}
    token = tokenize_event(event)
    assert token == "view_prod_001"

def test_session_segmentation():
    """Test session boundary detection."""
    events = [
        {"timestamp": 1000, "user_id": "u1"},
        {"timestamp": 1005, "user_id": "u1"},  # Same session
        {"timestamp": 3000, "user_id": "u1"},  # New session (>30 min)
    ]
    segmented = segment_into_sessions(events, timeout_minutes=30)
    assert segmented[0]['session_id'] == segmented[1]['session_id']
    assert segmented[0]['session_id'] != segmented[2]['session_id']
```

### Integration Tests

```python
def test_end_to_end_pipeline():
    """Test complete pipeline with sample data."""
    # Generate sample data
    events = generate_sample_events(n_users=100, n_events=1000)

    # Run pipeline
    sequences, customer_tokens = preprocess(events)
    model = train_item2vec(sequences)
    embeddings = aggregate_customers(customer_tokens, model)
    profiles = apply_nmf(embeddings)

    # Validate outputs
    assert len(profiles) == 100  # All customers have profiles
    assert all(len(p) == 16 for p in profiles.values())  # k=16 dimensions
    assert all(sum(p) > 0 for p in profiles.values())  # Non-zero profiles
```

### Quality Tests

```python
def test_similar_customers_are_similar():
    """Test that behaviorally similar customers have similar profiles."""
    # Create two customers with similar behavior
    customer_a_tokens = ["view_electronics", "cart_electronics", "buy_electronics"]
    customer_b_tokens = ["view_electronics", "view_tech", "cart_tech", "buy_tech"]
    customer_c_tokens = ["view_clothing", "view_fashion", "cart_fashion"]

    profile_a = compute_profile(customer_a_tokens)
    profile_b = compute_profile(customer_b_tokens)
    profile_c = compute_profile(customer_c_tokens)

    sim_ab = cosine_similarity(profile_a, profile_b)
    sim_ac = cosine_similarity(profile_a, profile_c)

    # A and B should be more similar than A and C
    assert sim_ab > sim_ac
```

---

## Dependencies

### Required Libraries

```
# Core
gensim>=4.3.0          # Item2Vec (Word2Vec implementation)
scikit-learn>=1.3.0    # NMF, metrics
numpy>=1.24.0          # Array operations
pandas>=2.0.0          # Data manipulation

# Optional (visualization)
umap-learn>=0.5.0      # Dimensionality reduction for viz
matplotlib>=3.7.0      # Plotting
seaborn>=0.12.0        # Statistical visualization

# Optional (caching)
redis>=4.5.0           # Profile caching

# Optional (monitoring)
prometheus-client>=0.17.0  # Metrics export
```

### Installation

```bash
pip install gensim scikit-learn numpy pandas
pip install umap-learn matplotlib seaborn  # For visualization
pip install redis  # For caching
```
