# Telecom Churn Analysis

Predicted customer churn for 7,043 telecom customers using RandomForest. Optimized decision threshold for business ROI (₹161,500) rather than accuracy.

**Result:** 82.4% recall | 861 at-risk customers | ₹161,500 net business value

---

## Problem

Telecom provider loses 26.5% of customers annually (1,900 customers/year × ₹2,000 LTV = ₹3.8M loss). No data-driven way to identify and retain at-risk customers.

---

## Solution

Business-optimized ML pipeline:

- RandomForest classifier: 82.4% recall
- Decision threshold optimized for ROI (0.45 vs default 0.5)
- Identified 861 at-risk customers for targeted retention

### Business Impact

False Positive Cost: ₹500 (wasted offer)
False Negative Cost: ₹2,000 (lost customer)

By shifting threshold from 0.5 → 0.45:

- Customers targeted: 861
- Retention cost: ₹430,500
- Revenue saved: ₹672,000
- **Net value: ₹161,500**

---

## Key Findings

### Top 3 Churn Drivers

1. **New customers (<6 months)** - 6.64% importance
   - 53% churn risk in first 6 months

2. **Tenure (months in service)** - 6.11% importance
   - 24+ month customers: 14% churn vs 53% for <6 months

3. **Tech support** - 5.07% importance
   - Lack of tech support increases churn risk

### Churn by Segment

**Contract Type:**

- Month-to-month: 42.7%
- One year: 11.3%
- Two year: 2.8%

**Customer Tenure:**

- 0-6 months: 53.3%
- 6-12 months: 35.9%
- 12-24 months: 28.7%
- 24+ months: 14.0%

---

## Model Performance

| Metric    | Value |
| --------- | ----- |
| Accuracy  | 59.9% |
| Recall    | 89.6% |
| Precision | 38.9% |
| F1-Score  | 54.3% |
| ROC-AUC   | 0.822 |

Recall prioritized: Missing a ₹2,000 customer loss is costlier than a ₹500 wasted offer.

---

## Customer Segments for Targeting

| Risk Level        | Count     | Action                        | Budget       |
| ----------------- | --------- | ----------------------------- | ------------ |
| High (0.5-0.7)    | 662       | Personal call + ₹500 discount | ₹331,000     |
| Medium (0.35-0.5) | 464       | Email + service check         | ₹46,400      |
| Low (<0.35)       | 283       | Monitor                       | —            |
| **Total**         | **1,409** |                               | **₹430,500** |

---

## Repository Structure

```
telecom-churn-analysis/
├── README.md
├── requirements.txt
├── telecom-churn-analysis.ipynb
└── results/
    ├── churn_predictions.csv
    └── figures/
        ├── 01_feature_importance.png
        ├── 02_precision_recall.png
        ├── 03_business_value.png
        └── 04_feature_contribution.png
```

---

## How to Run

```bash
git clone https://github.com/YOUR_USERNAME/telecom-churn-analysis.git
cd telecom-churn-analysis
pip install -r requirements.txt
python CLEAN_PRODUCTION_CODE.py
```

Or open Jupyter notebook:

```bash
jupyter notebook telecom-churn-analysis.ipynb
```

Output:

- 4 PNG visualizations (feature importance, precision-recall, business value, contribution)
- churn_predictions.csv (all predictions + risk segments)

---

## Model Architecture

**Algorithm:** RandomForest Classifier

- Trees: 100, Max depth: 10
- Class weight: Balanced (handles 26.5% churn imbalance)
- Split: 80/20 train/test (stratified)

**Features:** Tenure buckets, service counts, contract type, payment method, demographics

---

## Limitations

1. Point-in-time prediction (external factors not captured)
2. Untested ROI (assumes 60% of flagged customers would churn without intervention)
3. No customer value differentiation (all customers weighted equally)

---

## Future Work

1. A/B test retention offers to measure actual ROI
2. Time series forecasting for next N months
3. Customer lifetime value (CLV) integration
4. Causal analysis of churn drivers
5. Cohort-specific churn drivers

---

## Dataset

Kaggle - [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

- 7,043 customers, 21 features
- Binary target (churn yes/no)
- 2015-2018 data

---

## License

MIT License
