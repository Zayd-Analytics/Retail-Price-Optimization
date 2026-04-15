# Retail Price Optimization
### Machine Learning for Competitive Pricing Strategy

## Overview
A machine learning pipeline to determine optimal retail
product pricing based on historical sales data, competitor
pricing, and product attributes. Built to maximize
profitability while maintaining competitive market positioning.

Built as part of the BIA® Research Internship at
First Quadrant Labs. Project 4 of 6.

## Business Objective
- Predict optimal lag price for retail products
- Analyze competitor pricing impact on pricing decisions
- Provide interpretable, actionable pricing recommendations

## Dataset
- **Size:** 676 rows × 30 features
- **Target:** `lag_price` — previous period's price
- **Features:** Product attributes, sales metrics,
  3 competitor prices + scores + freight, temporal features

## Methodology
1. Data Loading & Inspection
2. Data Validation
   - Verified: total_price = unit_price × qty
   - Removed redundant derived columns
3. Feature Engineering
   - `diff_comp1/2/3` — price gap vs each competitor
   - `avg_comp_price` — average competitor price
   - `price_index` — relative competitive position
4. Leakage Prevention
   - Time-based split: train < 2018, test ≥ 2018
   - Dropped product_id, month_year, prev_unit_price
5. Preprocessing Pipeline
   - One-hot encoding for product_category_name
   - Standard scaling for numerical features
6. Model Training
   - Ridge Regression (L2 regularization)
   - Random Forest Regressor
7. Model Explainability
   - Permutation Importance
   - SHAP values (LinearExplainer)
8. Residual Analysis & Visualization

## Model Results
| Model | R² | MAE |
|---|---|---|
| **Ridge Regression** | **0.9868** | **4.92** |
| Random Forest | 0.9784 | 6.66 |

**Selected Model:** Ridge Regression
Simpler linear model outperformed ensemble —
confirms lag_price follows largely linear patterns
driven by price persistence and competitor dynamics.

## Feature Importance (SHAP)
| Rank | Feature | Insight |
|---|---|---|
| 1 | `unit_price` | Price persistence dominates |
| 2 | `diff_comp1/2/3` | Competitor gaps drive adjustments |
| 3 | `avg_comp_price` | Market pricing level matters |
| 4+ | Product attributes | Minimal influence on pricing |

## Key Findings
- Price persistence is the dominant pricing signal —
  products maintain stable prices month over month
- Competitor price differentials are the second
  strongest driver of optimal pricing decisions
- Product attributes (weight, photos, description)
  have minimal influence on lag price
- Ridge outperforms Random Forest — pricing follows
  linear patterns, not complex non-linear interactions
- SHAP confirms model decisions are interpretable
  and aligned with business intuition

## Tech Stack
Python • Scikit-learn • SHAP • Pandas • NumPy •
Matplotlib • Seaborn • Jupyter Notebooks

## Deliverables
- `Retail_Price_Optimization.ipynb` — Full pipeline
- `Retail_Price_Optimization.pptx` — Executive summary

## About
Part of a 6-month BIA® Research Internship at
First Quadrant Labs.
Project 4 of 6 — retail analytics & pricing domain.
