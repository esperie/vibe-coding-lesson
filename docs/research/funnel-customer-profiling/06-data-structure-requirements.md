# 06 - Data Structure Requirements

## Overview

This document specifies how raw funnel data should be structured and transformed for the recommended hybrid approach.

---

## Input Data Schema

### Raw Event Data

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           RAW EVENTS TABLE                                  │
├─────────────┬─────────────┬─────────────┬─────────────┬────────────────────┤
│ user_id     │ timestamp   │ action      │ product_id  │ session_id (opt)   │
│ (string)    │ (unix/iso)  │ (enum)      │ (string)    │ (string)           │
├─────────────┼─────────────┼─────────────┼─────────────┼────────────────────┤
│ user_001    │ 1704067200  │ view        │ prod_a      │ sess_001           │
│ user_001    │ 1704067205  │ view        │ prod_b      │ sess_001           │
│ user_001    │ 1704067210  │ view        │ prod_a      │ sess_001           │
│ user_001    │ 1704067215  │ add_cart    │ prod_a      │ sess_001           │
│ user_001    │ 1704067225  │ view        │ prod_c      │ sess_001           │
│ user_001    │ 1704067235  │ remove_cart │ prod_a      │ sess_001           │
│ user_001    │ 1704067240  │ add_cart    │ prod_d      │ sess_001           │
│ user_001    │ 1704069000  │ view        │ prod_e      │ sess_002           │
│ user_002    │ 1704067100  │ view        │ prod_x      │ sess_003           │
│ ...         │ ...         │ ...         │ ...         │ ...                │
└─────────────┴─────────────┴─────────────┴─────────────┴────────────────────┘
```

### Required Fields

| Field | Type | Description | Required |
|-------|------|-------------|----------|
| `user_id` | string | Unique customer identifier | Yes |
| `timestamp` | integer/string | Unix timestamp or ISO format | Yes |
| `action` | enum | Action type (view, add_cart, remove_cart, purchase) | Yes |
| `product_id` | string | Product identifier | Yes |
| `session_id` | string | Pre-computed session (if available) | No |

### Optional Fields (Enrichment)

| Field | Type | Description | Use |
|-------|------|-------------|-----|
| `product_category` | string | Product category | Fallback for cold products |
| `product_price` | float | Product price | Price-sensitivity analysis |
| `device_type` | string | mobile/desktop/tablet | Device-specific patterns |
| `referrer` | string | Traffic source | Channel analysis |

---

## Action Type Enumeration

```python
# Standard action types
ACTION_TYPES = {
    'view': 'view',           # Product page view
    'add_cart': 'cart',       # Added to cart
    'remove_cart': 'remove',  # Removed from cart
    'purchase': 'buy',        # Completed purchase
    'wishlist': 'wish',       # Added to wishlist
    'click': 'click',         # Generic click
    'search': 'search',       # Search action
}

# Mapping for tokenization
def normalize_action(raw_action):
    """Normalize action names for consistent tokenization."""
    return ACTION_TYPES.get(raw_action.lower(), raw_action.lower())
```

### Action Type Importance (Implicit)

The model learns action importance automatically, but expected hierarchy:
```
purchase > add_cart > wishlist > view > click
remove_cart: negative signal (learned separately)
```

---

## Data Transformations

### Step 1: Sort by User and Time

```python
# Input: Unsorted events
events = load_raw_events()

# Sort: Critical for sequence correctness
events_sorted = events.sort_values(['user_id', 'timestamp'])
```

### Step 2: Session Segmentation

```python
def segment_into_sessions(events_df, timeout_minutes=30):
    """
    Segment events into sessions based on inactivity.

    Args:
        events_df: DataFrame with user_id, timestamp columns
        timeout_minutes: Inactivity threshold for new session

    Returns:
        DataFrame with session_id column added
    """
    timeout_seconds = timeout_minutes * 60

    # Calculate time gap from previous event (per user)
    events_df = events_df.sort_values(['user_id', 'timestamp'])
    events_df['time_gap'] = events_df.groupby('user_id')['timestamp'].diff()

    # Mark session boundaries
    events_df['new_session'] = (
        events_df['time_gap'].isna() |  # First event for user
        (events_df['time_gap'] > timeout_seconds)
    )

    # Assign session IDs
    events_df['session_id'] = events_df.groupby('user_id')['new_session'].cumsum()
    events_df['session_id'] = (
        events_df['user_id'] + '_sess_' + events_df['session_id'].astype(str)
    )

    return events_df.drop(columns=['time_gap', 'new_session'])
```

### Step 3: Tokenization

```python
def tokenize_events(events_df):
    """
    Convert events to action-item tokens.

    Input:
        events_df with columns: user_id, session_id, action, product_id

    Output:
        events_df with 'token' column added
    """
    events_df['token'] = (
        events_df['action'].apply(normalize_action) +
        '_' +
        events_df['product_id']
    )
    return events_df
```

### Step 4: Create Sequences

```python
def create_sequences(events_df, min_length=2, max_length=100):
    """
    Group tokens into sequences per session.

    Args:
        events_df: DataFrame with session_id, token columns
        min_length: Minimum sequence length (filter short sessions)
        max_length: Maximum sequence length (truncate long sessions)

    Returns:
        List of token sequences (list of lists)
    """
    sequences = []

    for session_id, group in events_df.groupby('session_id'):
        tokens = group['token'].tolist()

        # Filter short sessions
        if len(tokens) < min_length:
            continue

        # Truncate long sessions (keep most recent)
        if len(tokens) > max_length:
            tokens = tokens[-max_length:]

        sequences.append(tokens)

    return sequences
```

---

## Intermediate Data Structures

### After Preprocessing

```python
# Token sequences for Item2Vec training
sequences = [
    ["view_prod_a", "view_prod_b", "view_prod_a", "cart_prod_a", "view_prod_c", "remove_prod_a", "cart_prod_d"],
    ["view_prod_e", "cart_prod_e", "buy_prod_e"],
    ["view_prod_x", "view_prod_y", "view_prod_x", "view_prod_z"],
    # ... more sessions
]

# Customer-to-tokens mapping
customer_tokens = {
    "user_001": ["view_prod_a", "view_prod_b", "view_prod_a", "cart_prod_a", "view_prod_c", "remove_prod_a", "cart_prod_d", "view_prod_e"],
    "user_002": ["view_prod_x", "view_prod_y", "view_prod_x", "view_prod_z"],
    # ...
}
```

### After Item2Vec

```python
# Token embeddings (from gensim model)
token_embeddings = {
    "view_prod_a": np.array([0.12, -0.34, 0.56, ...]),  # shape: (embedding_dim,)
    "cart_prod_a": np.array([0.45, -0.12, 0.78, ...]),
    "remove_prod_a": np.array([-0.23, 0.45, -0.11, ...]),
    # ...
}
```

### After Customer Aggregation

```python
# Customer embeddings
customer_embeddings = {
    "user_001": np.array([0.23, -0.15, 0.42, ...]),  # shape: (embedding_dim,)
    "user_002": np.array([0.11, 0.33, -0.28, ...]),
    # ...
}
```

### After NMF (Final Output)

```python
# Customer trait profiles
customer_profiles = {
    "user_001": [0.15, 0.72, 0.13, 0.45, 0.23, ...],  # shape: (n_components,)
    "user_002": [0.82, 0.11, 0.07, 0.33, 0.67, ...],
    # ...
}

# Trait-to-embedding mappings (for interpretation)
trait_embeddings = np.array([
    [...],  # Trait 0 embedding
    [...],  # Trait 1 embedding
    # ... n_components traits
])  # shape: (n_components, embedding_dim)
```

---

## Data Quality Requirements

### Minimum Thresholds

| Metric | Minimum | Recommended | Notes |
|--------|---------|-------------|-------|
| Total events | 10,000 | 100,000+ | For meaningful patterns |
| Unique users | 1,000 | 10,000+ | For NMF stability |
| Unique products | 100 | 1,000+ | Vocabulary diversity |
| Events per user (mean) | 5 | 20+ | Richer profiles |
| Session length (mean) | 3 | 10+ | Sequence context |

### Data Cleaning Rules

```python
def clean_events(events_df):
    """Apply data quality rules."""

    # Remove events with missing required fields
    events_df = events_df.dropna(subset=['user_id', 'timestamp', 'action', 'product_id'])

    # Remove invalid actions
    valid_actions = {'view', 'add_cart', 'remove_cart', 'purchase', 'wishlist', 'click'}
    events_df = events_df[events_df['action'].isin(valid_actions)]

    # Remove obvious bots (too many events in short time)
    user_event_counts = events_df.groupby('user_id').size()
    suspicious_users = user_event_counts[user_event_counts > 10000].index
    events_df = events_df[~events_df['user_id'].isin(suspicious_users)]

    # Remove test/internal users (if identifiable)
    events_df = events_df[~events_df['user_id'].str.contains('test|internal', case=False)]

    return events_df
```

---

## Storage Formats

### For Training Data

```python
# Option 1: Pickle (fastest for Python)
import pickle

with open('sequences.pkl', 'wb') as f:
    pickle.dump(sequences, f)

# Option 2: JSON Lines (portable)
import json

with open('sequences.jsonl', 'w') as f:
    for seq in sequences:
        f.write(json.dumps(seq) + '\n')

# Option 3: Parquet (for large datasets)
import pandas as pd

sequences_df = pd.DataFrame({
    'session_id': session_ids,
    'tokens': [','.join(seq) for seq in sequences]
})
sequences_df.to_parquet('sequences.parquet')
```

### For Model Artifacts

```python
# Item2Vec model
from gensim.models import Word2Vec
model.save('item2vec.model')

# Customer embeddings
import numpy as np
np.savez('customer_embeddings.npz',
         ids=list(customer_embeddings.keys()),
         embeddings=np.array(list(customer_embeddings.values())))

# Final profiles
import json
with open('customer_profiles.json', 'w') as f:
    json.dump(customer_profiles, f)
```

---

## Example Data Pipeline

```python
def prepare_training_data(raw_events_path, output_dir):
    """
    Complete data preparation pipeline.

    Args:
        raw_events_path: Path to raw events CSV/Parquet
        output_dir: Directory to save processed data

    Returns:
        sequences: List of token sequences for Item2Vec
        customer_tokens: Dict mapping customer_id to their tokens
    """
    import pandas as pd
    from pathlib import Path

    output_dir = Path(output_dir)
    output_dir.mkdir(parents=True, exist_ok=True)

    # Load raw data
    print("Loading raw events...")
    events_df = pd.read_csv(raw_events_path)  # or read_parquet

    # Clean
    print("Cleaning data...")
    events_df = clean_events(events_df)

    # Segment sessions
    print("Segmenting sessions...")
    events_df = segment_into_sessions(events_df, timeout_minutes=30)

    # Tokenize
    print("Tokenizing events...")
    events_df = tokenize_events(events_df)

    # Create sequences
    print("Creating sequences...")
    sequences = create_sequences(events_df, min_length=2, max_length=100)

    # Create customer-tokens mapping
    print("Mapping customers to tokens...")
    customer_tokens = (
        events_df
        .groupby('user_id')['token']
        .apply(list)
        .to_dict()
    )

    # Save
    print(f"Saving to {output_dir}...")
    with open(output_dir / 'sequences.pkl', 'wb') as f:
        pickle.dump(sequences, f)
    with open(output_dir / 'customer_tokens.pkl', 'wb') as f:
        pickle.dump(customer_tokens, f)

    # Statistics
    print(f"\nDataset Statistics:")
    print(f"  Total sequences: {len(sequences)}")
    print(f"  Total customers: {len(customer_tokens)}")
    print(f"  Unique tokens: {len(set(t for seq in sequences for t in seq))}")
    print(f"  Mean sequence length: {np.mean([len(s) for s in sequences]):.1f}")

    return sequences, customer_tokens
```

---

## Schema Summary

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              DATA FLOW                                       │
└─────────────────────────────────────────────────────────────────────────────┘

RAW EVENTS (CSV/Parquet/Database)
    │
    │  Fields: user_id, timestamp, action, product_id
    │
    ▼
CLEANED EVENTS (DataFrame)
    │
    │  Added: session_id
    │
    ▼
TOKENIZED EVENTS (DataFrame)
    │
    │  Added: token = "{action}_{product_id}"
    │
    ▼
┌───────────────────────┬─────────────────────────────┐
│                       │                             │
▼                       ▼                             │
SEQUENCES              CUSTOMER_TOKENS                │
(List[List[str]])      (Dict[str, List[str]])        │
    │                       │                         │
    │   Item2Vec            │                         │
    ▼                       │                         │
TOKEN_EMBEDDINGS           │                         │
(Dict[str, ndarray])       │                         │
    │                       │                         │
    └───────────────────────┘                         │
                │                                     │
                │  Aggregation                        │
                ▼                                     │
        CUSTOMER_EMBEDDINGS                           │
        (Dict[str, ndarray])                          │
                │                                     │
                │  NMF                                │
                ▼                                     │
        CUSTOMER_PROFILES ◄───────────────────────────┘
        (Dict[str, List[float]])
```
