# Fraud Detection in Financial Transactions

## Setup

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

## How to Run

```bash
jupyter notebook fraud_detection.ipynb

```

## Project Structure

```
.
├── fraud_detection.ipynb   # Complete analysis notebook
├── Fraud.csv               # Dataset (6.3M transactions)
├── Data Dictionary.txt     # Column descriptions
├── fig1-fig7 (.png)        # Output charts
└── README.md
```

## Results Summary

| Model | Precision | Recall | F1 | ROC-AUC | PR-AUC |
|-------|-----------|--------|----|---------|--------|
| Logistic Regression | 0.99 | 1.00 | 0.99 | 0.999 | 0.997 |
| **Random Forest** | **1.00** | **1.00** | **1.00** | **0.999** | **0.997** |
| Gradient Boosting | 1.00 | 1.00 | 1.00 | 1.000 | 0.997 |

## Key Findings

- Fraud only occurs in TRANSFER and CASH_OUT transactions (0.13% of total)
- Top predictor: **account draining pattern** (98% of fraud transactions empty the origin account)
- Current `isFlaggedFraud` system catches only 16 of 8,213 frauds (0.2%) — effectively useless
- Engineered features (balance errors, drain flags) outperform raw features

## Questions Answered

1. **Data Cleaning**: No missing values; outliers retained as fraud signals; multicollinearity handled via feature engineering
2. **Model**: Compared Logistic Regression, Random Forest, and Gradient Boosting with class balancing
3. **Variable Selection**: Mutual information analysis + engineered features from domain knowledge
4. **Performance**: ROC-AUC > 0.999, PR-AUC > 0.997 across all models
5. **Key Factors**: Account draining, balance discrepancies, high transaction amounts
6. **Interpretation**: All factors align with known fraud patterns (account takeover + fund extraction)
7. **Prevention**: Real-time ML scoring, balance verification, velocity checks, two-phase processing
8. **Evaluation**: A/B testing, KPI monitoring (recall, false positive rate, $ saved), champion-challenger framework
