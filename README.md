# VK RecSys — Recommendation Systems Project

This repository contains multiple recommendation system approaches built on the VK-LSVD dataset.  
The goal is to develop and compare different methods for personalized short video recommendation using the **MAP@10** metric.

---

## Implemented Approaches

### 1. Top Popular (TopPop)
- Recommends globally most popular items  
- No personalization  
- Used as a baseline

### 2. Top Popular (Filtered)
- Removes items already seen by the user  
- Stronger baseline than plain TopPop

### 3. Item-based Collaborative Filtering (Jaccard)
- Uses implicit feedback (views)
- Items are similar if watched by common users
- Recommendation score is aggregated over item–item similarities

---

## Content-Based (Unsupervised)

User profiles are built by averaging item embeddings.  
Recommendations are generated using **cosine similarity** between user profile and item embeddings.

### Results

| Split | MAP@10 |
|------|--------|
| Train (in-sample) | ~0.043 |
| Test (out-of-sample) | ~0.0033 |

### Insights

The large gap between in-sample and out-of-sample performance indicates that:

- Embeddings capture meaningful semantic information  
- Cosine similarity reflects content similarity well  
- However, the model lacks predictive power for future interactions  

### Limitations

- No popularity signal  
- No temporal dynamics  
- Optimizes semantic similarity rather than interaction probability  

This behavior is typical for unsupervised content-based models without collaborative or contextual signals.

---

## Supervised Model (LightGBM Baseline)

A supervised LightGBM classifier was trained to predict a binary target:
**watch time > 5 seconds**.

### Features
- User metadata (age, gender, geo)
- Item metadata
- Item embeddings

### Evaluation
Metric: **ROC-AUC**

**ROC-AUC ≈ 0.68**

This confirms the presence of a learnable signal and shows that supervised models can distinguish relevant from non-relevant interactions.  
The model is later used as a ranking component in the hybrid system.

---

## Implicit ALS

Matrix factorization for implicit feedback using user–item interaction matrix.

### Best configuration
- alpha = 1000  
- regularization = 10  

**MAP@10 ≈ 0.0164**

---

## Hybrid Recommendation System (Final Model)

A two-stage architecture:

### Stage 1 — Candidate Generation
- Implicit ALS  
- Top-100 items per user  

### Stage 2 — Re-Ranking
- LightGBM Ranker (LambdaRank)

### Features
- ALS score
- User metadata (age, gender, geo)
- Item metadata (author_id, duration)
- Item embeddings

---

## Final Results

| Model | MAP@10 |
|------|--------|
| TopPop | 0.0073 |
| TopPop (filtered) | 0.0149 |
| Item-based CF (Jaccard) | 0.0170 |
| ALS | 0.0164 |
| Content-based (test) | 0.0033 |
| **Hybrid (ALS + LightGBM)** | **0.162** |

The hybrid approach significantly improves recommendation quality by combining collaborative filtering for candidate retrieval with learning-to-rank for optimal item ordering.

---

## Key Insights

- Pure content similarity does not generalize to future interactions
- Collaborative filtering captures user behavior patterns
- Supervised learning effectively combines multiple signals
- Two-stage architectures outperform single-model approaches

---

## Future Improvements

- Time-based validation split
- Hyperparameter optimization
- Additional behavioral features
- User embeddings
- Online A/B testing

---

This project demonstrates practical implementation of modern recommender system techniques, including collaborative filtering, content-based methods, supervised learning, and hybrid learning-to-rank architectures.


