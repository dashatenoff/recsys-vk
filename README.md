# VK RecSys HW-1 — Baselines and Item-based Collaborative Filtering

This repository contains implementations of baseline and item-based recommender systems
for the VK-LSVD dataset as part of VK RecSys HW-1.

The goal of this project is to build a personalized recommender system for short video clips
and evaluate it using the MAP@10 metric.

---

## Implemented Models

### 1. Top Popular (TopPop)
- Recommends the globally most popular items
- No personalization
- Used as a baseline model

### 2. Top Popular with Seen-Items Filtering
- Extends TopPop by removing items already seen by the user
- Provides a stronger baseline
- Improves MAP@10 compared to plain TopPop

### 3. Item-based Collaborative Filtering (Jaccard Similarity)
- Uses implicit feedback (views)
- Items are considered similar if they are watched by common users
- Recommendation score is aggregated over similarities to all items seen by a user
- Item–item similarities are precomputed for efficiency
- Implemented in a simple and interpretable form for educational purposes

---

## Evaluation

All models are evaluated using the **MAP@10** metric.

| Model                         | MAP@10 |
|------------------------------|--------|
| TopPop                       | 0.0073 |
| TopPop (filtered)            | 0.0149 |
| Item-based CF (Jaccard)      | 0.0170 |

The item-based collaborative filtering model outperforms the TopPop baseline
by more than **2×**, demonstrating the benefit of personalization.

---

The notebook contains the full pipeline:

data loading

similarity computation

recommendation generation

MAP@10 evaluation
