# VK RecSys HW-1 — Baselines and Item-based CF

This repository contains baseline recommender system models
implemented for the VK-LSVD dataset.

## Implemented approaches

### 1. Top Popular (TopPop)
- Recommends globally most popular items
- No personalization
- Baseline model

### 2. TopPop with seen-items filtering
- Removes items already seen by the user
- Slightly improves MAP@10

### 3. Item-based Collaborative Filtering (Jaccard similarity)
- Uses implicit feedback (views)
- Items are similar if they are watched by common users
- Recommendation score is aggregated over all items seen by a user

The item-based CF model is implemented in a straightforward form
for educational purposes and clarity.
Due to computational complexity, this version is not optimized
for large-scale inference.

## Evaluation

All models are evaluated using MAP@10.

| Model | MAP@10 |
|------|--------|
| TopPop | X.XXX |
| TopPop filtered | X.XXX |
| Item-based CF (Jaccard) | X.XXX |

## Notes
- Datasets are not included in the repository
- Implementations focus on clarity and conceptual correctness
- Further optimization and ALS-based models are planned

