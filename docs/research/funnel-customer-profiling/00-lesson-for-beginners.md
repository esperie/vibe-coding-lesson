# Understanding Customer Profiling from Shopping Data

## A Beginner's Guide for Aspiring Data Scientists

---

## Before We Start: What You'll Learn

By the end of this lesson, you'll understand:
1. What "funnel data" is and why it matters
2. Why traditional methods fail for this problem
3. How computers can "learn" what products mean
4. How to create understandable customer profiles

**No math required.** We'll use stories and pictures.

---

# Part 1: The Problem (Why This Matters)

## Imagine You Run an Online Store

You have **100,000 customers**. Every day, they:
- **Look at** products (view)
- **Add things** to their cart (add_cart)
- **Remove things** from their cart (remove_cart)
- **Buy things** (purchase)

Your boss asks: *"What types of customers do we have?"*

You can't read 100,000 shopping histories manually. You need a computer to create a **summary** of each customer automatically.

---

## The Shopping Journey Tells a Story

Look at these three customers:

```
Customer A: view_shoes → view_shoes → view_shoes → cart_shoes → BUY_shoes
Customer B: view_shoes → cart_shoes → REMOVE_shoes → view_jacket → cart_jacket → BUY_jacket
Customer C: view_shoes → view_laptop → view_book → view_camera → [leaves]
```

**What can we infer?**

| Customer | The Story |
|----------|-----------|
| A | Knew what they wanted, researched it, committed |
| B | Considered shoes, **rejected them**, chose jacket instead |
| C | Window shopping, not ready to buy |

**Key insight**: The ORDER of actions tells us what the customer is thinking.

---

## The Detective's Notebook Analogy

Think of customer data like a detective's notebook:

```
9:00 AM - Customer entered store
9:05 AM - Looked at expensive watches (3 minutes)
9:08 AM - Asked about refund policy      ← Hmm, hesitant?
9:10 AM - Picked up a watch
9:11 AM - Put it back                    ← Changed their mind
9:15 AM - Left without buying
```

If we just counted "1 store visit, 1 watch interaction", we'd miss that this person **considered buying but decided against it**.

The sequence of events contains the meaning.

---

# Part 2: Why Simple Solutions Fail

## Your Boss Says: "Just Use a Spreadsheet!"

So you try this:

| Customer | Shoes Views | Shoes Cart | Shoes Buy | Laptop Views | Laptop Cart | ... |
|----------|-------------|------------|-----------|--------------|-------------|-----|
| A | 3 | 1 | 1 | 0 | 0 | ... |
| B | 1 | 1 | 0 | 0 | 0 | ... |
| C | 1 | 0 | 0 | 1 | 0 | ... |

**Three Problems:**

### Problem 1: Too Many Columns
You have 10,000 products. That's **30,000+ columns** (views, carts, buys for each product).

This is called the **"curse of dimensionality"** - too many columns makes finding patterns nearly impossible.

### Problem 2: Mostly Empty
Most customers only see 50-100 products out of 10,000. Your spreadsheet is **99% empty cells**.

### Problem 3: Lost the Story
Look at Customer B's row. It shows "1 cart, 0 buy" for shoes.

But we **lost crucial information**: they REMOVED shoes from their cart. That's a **rejection signal**, not just "didn't buy."

---

## The Squishing Problem

Traditional methods "squish" your data:

**Before squishing (the full story):**
```
view_shoes → view_shoes → cart_shoes → REMOVE_shoes → view_jacket → cart_jacket
```

**After squishing (spreadsheet):**
```
shoes: 2 views + 1 cart + 1 remove = score of 2
jacket: 1 view + 1 cart = score of 2
```

Both products got the **same score**, but the customer **rejected shoes** and **wanted jacket**.

The squishing destroyed the story.

---

## Visualizing What Gets Lost

```
TIMELINE (what really happened):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  [view_shoes]  [view_jacket]  [cart_shoes]  [REMOVE_shoes]  [cart_jacket]  [BUY_jacket]
       ↓              ↓             ↓              ↓               ↓              ↓
   Browsing      Comparing      Deciding       REJECTED!       Decided        BOUGHT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SPREADSHEET (what we keep):
┌─────────┬───────┬──────┬────────┬─────┐
│ Product │ Views │ Cart │ Remove │ Buy │
├─────────┼───────┼──────┼────────┼─────┤
│ Shoes   │ 1     │ 1    │ 1      │ 0   │
│ Jacket  │ 1     │ 1    │ 0      │ 1   │
└─────────┴───────┴──────┴────────┴─────┘

❌ LOST: The fact that shoes were CONSIDERED THEN REJECTED
❌ LOST: The sequence showing jacket was the SECOND CHOICE after rejection
```

---

# Part 3: The Key Insight - Learning from Patterns

## You Are Who You Hang Out With

Imagine you're at a party and you observe:
- Alice talks to Bob, then Carol, then Dave
- Eve talks to Bob, then Carol, then Frank

**Who are similar?**
- Bob and Carol - they appear in similar conversation chains
- Alice and Eve - they talked to similar people

**This is the core insight of our solution.**

---

## The Word Prediction Game

Here's a simple game. Fill in the blank:

> "The cat sat on the ___"

You'd guess: **mat, floor, couch, chair**

You would NOT guess: elephant, algorithm, photosynthesis

**Why?** Because you've seen "cat sat on X" patterns thousands of times. You **learned** what words appear near "cat sat on."

---

## Now Play It with Shopping Data

Fill in the blank:

> "Customer viewed shoes, then viewed ___, then bought shoes"

Good guesses: **socks, belt, shoe polish, sandals**

Bad guesses: refrigerator, car tire, piano

**Why?** Because in shopping data, certain products appear near each other. People who look at shoes often also look at socks.

---

## The Computer Learns Product Meanings

Instead of a human telling the computer "shoes and socks are related," we let the computer **discover this from patterns**.

After seeing millions of shopping journeys:
- Products that appear near each other = probably related
- Actions that appear in similar contexts = probably mean similar things

The computer builds a **"meaning map"** where similar things are close together.

```
        THE MEANING MAP (simplified)

     [Electronics Zone]              [Fashion Zone]

         laptop •                        • dress
                  • phone           shoes •
         tablet •                        • shirt
                  • headphones     belt •


     [Household Zone]

         pan •
              • blender
         towels •
```

Products that get bought together, viewed together, or carted together end up **close on the map**.

---

## Learning Language by Immersion (Analogy)

Imagine you move to France knowing zero French.

```
Day 1: You hear "bonjour" when people meet in the morning
Day 2: You hear "bonjour" when entering a shop
Day 3: You hear "au revoir" when people leave

You NEVER read a dictionary.
But you LEARN:
  - "bonjour" = greeting (appears when meeting)
  - "au revoir" = goodbye (appears when leaving)
```

The computer learns product meanings the same way:
- "cart_shoes" appears near "cart_socks" often → they're related
- "remove_item" appears after "view_price" often → price sensitivity pattern
- "buy_luxury" appears after "view_many_options" → research-then-commit pattern

**It learns meanings from PATTERNS, not definitions.**

This technique is called **Item2Vec** (like Word2Vec, but for shopping items).

---

# Part 4: Creating Customer Profiles

## Step 1: Learn What Products Mean

First, we train the computer on ALL shopping journeys to learn the "meaning map."

After training:
- `view_laptop` → position [0.2, 0.8, ...] on the map (128 numbers)
- `cart_phone` → position [0.3, 0.7, ...] on the map
- `buy_dress` → position [0.9, 0.1, ...] on the map

Each product-action gets a **position** in the meaning space.

---

## Step 2: Trace a Customer's Journey on the Map

Now we can "trace" a customer's shopping journey on our meaning map:

```
Customer A's Journey:
  view_laptop → view_phone → cart_phone → buy_phone

On the meaning map:

  [0.2, 0.8] → [0.3, 0.7] → [0.4, 0.9] → [0.5, 0.95]
       ↑           ↑            ↑            ↑
   Started     Explored      Decided       Bought
   in tech     tech zone     on phone    (still tech)
```

The customer stayed in the **"tech zone"** the whole time.

---

## Step 3: Summarize the Journey

We take the **average position** of all their actions:

```
Customer A's average position = [0.35, 0.84]  → "Tech Enthusiast area"

Customer B's Journey:
  view_dress → view_shoes → cart_dress → buy_dress
  Average position = [0.86, 0.31]  → "Fashion area"
```

Now each customer has ONE summary position instead of a long list of actions.

---

## Step 4: Find the "Personality Types"

If we plot 100,000 customers on the meaning map, we see clusters:

```
                     •  •
                    • •• •                   •  •
                   •  • •                   • ••• •
                  • ••  •                    • ••
                    Tech                    Fashion
                  Cluster                   Cluster

                           •
                          • •
                         •  •• •
                           ••
                          Bargain
                          Cluster
```

The computer can automatically find these "personality types" using a technique called **NMF (Non-negative Matrix Factorization)**.

Don't worry about the name - it just means "find the main directions that explain where customers are."

---

## The Final Output: Customer Traits

After all steps, each customer gets a **trait profile**:

```
Customer A:
  - Tech Enthusiast:    0.82  ████████░░
  - Fashion Focused:    0.05  █░░░░░░░░░
  - Bargain Hunter:     0.08  █░░░░░░░░░
  - Impulse Buyer:      0.05  █░░░░░░░░░

Customer B:
  - Tech Enthusiast:    0.10  █░░░░░░░░░
  - Fashion Focused:    0.75  ████████░░
  - Bargain Hunter:     0.10  █░░░░░░░░░
  - Impulse Buyer:      0.05  █░░░░░░░░░
```

Now we can:
- **Find similar customers**: "Show me customers like Customer A"
- **Personalize recommendations**: "Tech enthusiasts also bought..."
- **Understand segments**: "15% of our customers are bargain hunters"

---

# Part 5: Why We Need Both Techniques

## Why Not Just Use Item2Vec?

Item2Vec gives each customer a position like `[0.35, 0.84, 0.12, 0.67, ...]` with **128 numbers**.

Problem: What does each number mean? We don't know. It's a "black box."

## Why Not Just Use NMF?

NMF can find personality types, but it needs input that **doesn't lose the sequence information**.

If we feed it the "squished" spreadsheet, it finds patterns in garbage.

## The Combination: Best of Both Worlds

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   Item2Vec                           NMF                            │
│   ─────────                          ───                            │
│   Understands sequences        →     Finds interpretable           │
│   Learns product meanings            personality types              │
│   Outputs 128 numbers                Outputs 10-20 named traits    │
│   (hard to interpret)                (easy to understand)           │
│                                                                     │
│                     TOGETHER                                        │
│                     ════════                                        │
│         Sequences → Meaningful positions → Named traits             │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**Item2Vec** captures the story (sequence).
**NMF** makes it understandable (named traits).

---

# Part 6: Putting It All Together

## The Complete Pipeline

```
┌─────────────────────────────────────────────────────────────────────┐
│ 1. COLLECT: Raw shopping events                                     │
│                                                                     │
│    user_001: view_shoes → view_socks → cart_shoes → buy_shoes      │
│    user_002: view_laptop → view_laptop → cart_laptop → remove...   │
│    ... (millions of events)                                         │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│ 2. LEARN: Train Item2Vec on all events                              │
│                                                                     │
│    Computer learns: "shoes and socks appear together often"         │
│    Computer learns: "remove often follows view_price"               │
│    Output: Meaning map (each product-action gets a position)        │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│ 3. SUMMARIZE: Average each customer's journey positions             │
│                                                                     │
│    user_001: stayed in "fashion zone" → position [0.1, 0.9, ...]   │
│    user_002: wandered "tech zone" → position [0.8, 0.2, ...]       │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│ 4. SIMPLIFY: NMF finds main "personality types"                     │
│                                                                     │
│    Type 1: Tech Enthusiast                                          │
│    Type 2: Fashion Focused                                          │
│    Type 3: Bargain Hunter                                           │
│    Type 4: Impulse Buyer                                            │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│ 5. OUTPUT: Each customer gets trait scores                          │
│                                                                     │
│    user_001: 10% Tech, 85% Fashion, 3% Bargain, 2% Impulse         │
│    user_002: 78% Tech, 5% Fashion, 12% Bargain, 5% Impulse         │
│                                                                     │
│    → Use for recommendations, segmentation, personalization         │
└─────────────────────────────────────────────────────────────────────┘
```

---

# Part 7: Common Misconceptions

## "Just count the actions"

**Wrong**: Customer interacted with Product A five times = interested

**Right**: The pattern `view → cart → REMOVE → view → leave` = rejection, not interest

The sequence contains the meaning.

---

## "We need to label customers first"

**Wrong**: We need to manually tag customers as "tech enthusiast" before training

**Right**: The algorithm discovers patterns automatically. We name them afterward.

It's **unsupervised learning** - no labels needed.

---

## "Remove from cart is just negative"

**Wrong**: `remove_cart = -2 points` (arbitrary penalty)

**Right**: `remove_cart` is a **signal** that tells us "customer considered and rejected"

This is valuable information! It tells us what they **don't** want.

---

## "The computer understands customer types"

**Wrong**: The computer knows what "bargain hunter" means

**Right**: The computer finds clusters. Humans look at what products those customers bought and **name** the cluster.

```
Computer: "Cluster 3 customers often: view_sale, cart_clearance, remove_fullprice"
Human:    "I'll call that 'Bargain Hunter'"
```

---

# Part 8: Try It Yourself

## Exercise 1: Read the Story

What can you infer about each customer?

```
Customer A: view_TV → view_TV → view_soundbar → cart_TV → cart_soundbar → buy_TV → buy_soundbar

Customer B: view_TV → cart_TV → remove_TV → view_cheaper_TV → cart_cheaper_TV → buy_cheaper_TV

Customer C: view_TV → view_laptop → view_headphones → view_camera → view_drone → [leaves]
```

<details>
<summary>Click to see answers</summary>

- **Customer A**: Home theater enthusiast. Researched, bought a bundle. High intent, planned purchase.
- **Customer B**: Price sensitive. Wanted a TV but chose a cheaper option. Bargain hunter.
- **Customer C**: Window shopping electronics. Browsing without intent. Might be researching for future.

</details>

---

## Exercise 2: Spot the Lost Information

These two journeys would look IDENTICAL in a spreadsheet. What information gets lost?

```
Journey 1: view_A → view_B → cart_A → buy_A
Journey 2: view_A → cart_A → remove_A → view_B → cart_B → buy_B
```

**Spreadsheet for both:**
| Product | Views | Cart | Buy |
|---------|-------|------|-----|
| A | 1 | 1 | varies |
| B | 1 | 1 | varies |

<details>
<summary>Click to see answer</summary>

- **Journey 1**: Customer chose A. B was just browsed.
- **Journey 2**: Customer REJECTED A and chose B instead.

The spreadsheet can't distinguish "chose A over B" from "rejected A, chose B."

The **remove_A** action and the **sequence** (A first, then B) are completely lost.

</details>

---

## Exercise 3: Predict the Neighbors

If `cart_laptop` is close to `cart_phone` and `buy_electronics` on the meaning map...

What products would you expect to be CLOSE to `view_dress`?

<details>
<summary>Click to see answer</summary>

Likely neighbors:
- `view_shoes`
- `view_jewelry`
- `cart_dress`
- `buy_fashion`
- `view_handbag`

Products in the same shopping context (fashion/clothing) will cluster together.

</details>

---

# Summary: The Key Takeaways

1. **Funnel data is sequential** - the order of actions tells a story
2. **Spreadsheets lose the story** - counting destroys sequence information
3. **Item2Vec learns from context** - like learning a language by immersion
4. **NMF finds personality types** - clusters customers into interpretable groups
5. **Together they work** - Item2Vec captures sequences, NMF makes them understandable

---

# Glossary

| Term | Simple Meaning |
|------|----------------|
| **Funnel data** | The sequence of customer actions (view → cart → buy) |
| **Dimension** | One column or aspect of data (like height, weight, age) |
| **Embedding** | A position on the "meaning map" (list of numbers) |
| **Item2Vec** | Technique to learn product meanings from shopping patterns |
| **NMF** | Technique to find main "personality types" from customer positions |
| **Unsupervised** | Learning patterns without human-provided labels |
| **Cold start** | New customers with no history (hard to profile) |

---

# What's Next?

Now that you understand the concepts, you can explore:

1. **[05-recommended-approach.md](./05-recommended-approach.md)** - The technical implementation details
2. **[06-data-structure-requirements.md](./06-data-structure-requirements.md)** - How to prepare your data
3. **[08-references.md](./08-references.md)** - Academic papers to dive deeper

Remember: You now understand the **why** and **what**. The other documents explain the **how**.

---

*This lesson is part of the Customer Profiling Research documentation.*
