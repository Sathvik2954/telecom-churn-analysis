# Telecom Churn Analysis

Predicted customer churn for 7,043 telecom customers using RandomForest. Optimized decision threshold for business ROI (₹161,500) rather than accuracy.

**Result:** 82.4% recall | 861 at-risk customers identified | ₹161,500 projected net business value

---

## Problem Statement

A telecom provider loses 26.5% of customers annually. Without a data-driven retention strategy:

- Miss opportunities to save at-risk customers
- Waste retention budget on low-risk customers
- Lack visibility into which factors drive churn

Annual impact: ~1,900 churned customers × ₹2,000 customer lifetime value = ₹3.8M loss

---

## Solution

Built a business-optimized machine learning pipeline that:

1. Predicts churn with 82.4% recall (catch 9 out of 10 churners)
2. Optimizes decision threshold for maximum ROI, not accuracy (0.45 vs default 0.5)
3. Segments customers by risk level for targeted retention offers
4. Quantifies business impact: ₹161,500 net value from optimized targeting

### What Makes This Different

Most ML projects optimize for accuracy. This project optimizes for business value:

- False Positive Cost: ₹500 (wasted retention offer)
- False Negative Cost: ₹2,000 (lost customer)
- Result: Threshold shifted from 0.5 → 0.45 to maximize net ROI

---

## Key Findings

### Top 3 Churn Drivers

1. **New customers (<6 months)** - Importance: 6.64%
   - 53% churn risk in first 6 months
   - Onboarding is the critical period
   - Early intervention has highest ROI

2. **Tenure (months in service)** - Importance: 6.11%
   - Every additional month of tenure reduces churn risk
   - 24+ month customers have only 14% churn vs 53% for <6 months
   - Long-term customers are stable

3. **Missing tech support** - Importance: 5.07%
   - Customers without tech support churn at higher rates
   - Tech support is a strong protective factor
   - Should be bundled in base package

### Churn Distribution by Segment

**By Contract Type:**

- Month-to-month: 42.7% (HIGH RISK)
- One year: 11.3%
- Two year: 2.8% (STABLE)

**By Customer Tenure:**

- 0-6 months: 53.3% (CRITICAL)
- 6-12 months: 35.9%
- 12-24 months: 28.7%
- 24+ months: 14.0% (SAFE)

---

## Model Performance

| Metric    | Value | Interpretation                           |
| --------- | ----- | ---------------------------------------- |
| Accuracy  | 59.9% | Good; baseline is 73.5% (majority class) |
| Recall    | 89.6% | Catches 9 out of 10 churners             |
| Precision | 38.9% | 39% of targeted customers will churn     |
| F1-Score  | 54.3% | Balanced precision-recall tradeoff       |
| ROC-AUC   | 0.822 | Strong discriminatory power              |

### Why These Metrics Matter

High Recall (89.6%) is prioritized because missing a ₹2,000 customer loss is costlier than a ₹500 wasted retention offer. Precision of 38.9% means 2 out of 3 offers will be wasted, but the third one saves ₹2,000, making the offer economically justified.

---

## Business Optimization

### Threshold Decision

Default threshold (0.5) is too conservative and misses churners.

Optimal threshold (0.45) maximizes business value:

- Customers targeted: 861 (+23% vs default)
- Retention offer cost: ₹430,500
- Revenue saved: ₹672,000
- Net business value: ₹161,500

### Customer Segmentation for Targeting

| Risk Segment      | Count | Action                                 | Budget   |
| ----------------- | ----- | -------------------------------------- | -------- |
| High (0.5-0.7)    | 662   | Personal call + ₹500 loyalty discount  | ₹331,000 |
| Medium (0.35-0.5) | 464   | Email campaign + service quality check | ₹46,400  |
| Low (<0.35)       | 283   | Monitor; no action needed              | —        |
| Total             | 1,409 |                                        | ₹430,500 |

---

## Strategic Recommendations

### 1. Onboarding Excellence (Highest Priority)

Problem: 53% of customers churn in first 6 months

Actions:

- Assign dedicated customer success manager for first 90 days
- Proactive check-ins: week 1, week 4, week 12
- Tech support training during onboarding setup
- Goal: Reduce <6-month churn from 53% to 35%

Expected ROI: Prevent ~150 churns × ₹2,000 = ₹300,000 annual savings

### 2. Contract Upgrade Campaign (High Impact)

Problem: Month-to-month contracts have 42.7% churn vs 2.8% for 2-year

Actions:

- Quarterly upgrade offers: "Lock in annual plan, save 20%"
- Discount: ₹50-100 per month for annual commitment
- Target: Convert 30% of month-to-month customers to annual
- Goal: Reduce month-to-month churn by 15%

Expected ROI: 30% × 700 customers × ₹2,000 = ₹420,000 annual savings

### 3. Tech Support Bundling (Quick Win)

Problem: Customers without tech support churn at higher rates

Actions:

- Bundle tech support in base package (remove from optional add-ons)
- Proactive outreach: "We noticed you had support issues; here's your contact"
- Minimal cost: Support team infrastructure already exists
- Goal: 15% reduction in tech-support-related churn

Expected ROI: 100-150 additional saves × ₹2,000 = ₹200,000-300,000 annual savings

### 4. Fiber Optic Quality Investigation (Root Cause)

Problem: Fiber optic users churn more than other service types

Actions:

- Speed audit: Verify fiber customers get promised speeds
- Quality analysis: Connection stability, support response time
- Cohort analysis: Which fiber segments churn most
- Decision: Fix quality vs adjust pricing vs improve support

Expected ROI: Investigation cost (~₹50k) could unlock ₹500k+ savings

---

## Implementation Roadmap

### Month 1: Pilot (500 High-Risk Customers)

- Target top 500 at-risk customers with retention offers
- Test offer messaging and delivery channels
- Measure: Offer acceptance rate, 3-month retention impact
- Success criteria: >40% acceptance, >60% 3-month retention

### Month 2-3: Scale Decision

- If pilot ROI is positive: Expand to full 861 customers
- If pilot ROI is negative: Adjust offer strategy and retry
- A/B test different offer amounts by segment

### Month 4+: Continuous Improvement

- Retrain model monthly with new churn data
- Monitor model performance; recalibrate quarterly
- Track actual ROI vs projected ROI
- Expand to other customer segments (upsell, cross-sell opportunities)

---

## Repository Structure

```
telecom-churn-analysis/
├── README.md
├── requirements.txt
├── telecom-churn-analysis.ipynb
├── results/
│   ├── churn_predictions.csv
│   └── figures/
│       ├── 01_feature_importance.png
│       ├── 02_precision_recall.png
│       ├── 03_business_value.png
│       └── 04_feature_contribution.png

```

---

## How to Reproduce

### Requirements

- Python 3.8+
- See requirements.txt for all dependencies

### Setup

```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/telecom-churn-analysis.git
cd telecom-churn-analysis

# Install dependencies
pip install -r requirements.txt

# Run analysis
python CLEAN_PRODUCTION_CODE.py
```

Or open the Jupyter notebook:

```bash
jupyter notebook telecom-churn-analysis.ipynb
```

### Output

The analysis generates:

- 4 PNG visualizations (feature importance, precision-recall, business value, feature contribution)
- churn_predictions.csv (predictions + risk segments for all 1,409 test customers)

---

## Key Interview Talking Points

1. **Business-First Optimization**

"I optimized for business value, not accuracy. Default threshold was 0.5, but I calculated that false positives cost ₹500 and false negatives cost ₹2,000. So I found the threshold (0.45) that maximized net ROI: ₹161,500."

2. **Handling Class Imbalance**

"Only 26.5% of customers churn. I used class_weight='balanced' in RandomForest to prevent the model from predicting everyone stays. This pushed recall from 51% to 89.6%."

3. **Metric Selection**

"I didn't use accuracy as my success metric. High recall (89.6%) beats high precision because missing a ₹2,000 customer loss is costlier than a ₹500 wasted offer."

4. **Segment-Based Strategy**

"New customers churn at 53% vs 14% for 24+ month customers. So I'd allocate retention resources differently by segment, not uniformly across all customers."

5. **Real-World Validation**

"The model is a tool, but business validation is critical. I'd run a pilot on 500 customers to measure actual offer acceptance rates and ROI before scaling."

---

## Model Architecture

Algorithm: RandomForest Classifier

- Trees: 100
- Max depth: 10
- Class weight: Balanced (handles 26.5% churn imbalance)
- Train/Test split: 80/20 (stratified)

Feature engineering:

- Tenure buckets (new customer flag, years in service)
- Service counts (phone, internet, security, streaming, etc.)
- Contract type encoding
- Payment method features
- Demographic features (senior citizen, partner, dependents)

---

## Limitations and Future Work

### Current Limitations

1. Point-in-time prediction: External factors (competitor promos, economic conditions) not captured in historical data

2. Retention ROI untested: Projections assume 60% of flagged customers would churn without intervention; actual may differ

3. No revenue heterogeneity: All customers weighted equally; high-value customers might justify different strategies

### Future Improvements

1. A/B test retention offers by segment to measure actual acceptance rates

2. Time series forecasting: Predict churn risk over next N months (not point-in-time snapshot)

3. Customer lifetime value (CLV) integration: Prioritize retention spend on high-value customers

4. Causal analysis: Determine which factors are causal vs correlational

5. Cohort analysis: Identify if different customer groups have different churn drivers

---

## Dataset Information

Source: Telco Customer Churn (Kaggle)
URL: https://www.kaggle.com/datasets/blastchar/telco-customer-churn

Dataset details:

- 7,043 customers
- 21 features (demographics, services, contract, charges)
- Binary target (churn yes/no)
- Time period: 2015-2018
- License: Public domain

---

## License

This project is licensed under the MIT License.

---
