
# D2C Customer Churn Prediction Model Card

## 1. Model Overview

### Model Name
D2C Customer Churn Prediction Model

### Model Version
Version 1.0

### Business Objective

This machine learning model predicts the probability that a customer will churn within the next 60 days after the snapshot date.

The model supports the marketing, CRM, and retention teams in identifying customers who should receive proactive engagement campaigns such as personalized offers, loyalty benefits, product recommendations, or service improvements.

The model is designed to prioritize retention resources efficiently instead of sending expensive campaigns to every customer.

---

# 2. Intended Use

## Appropriate Use Cases

The model should be used for:

- Prioritizing customers for retention campaigns.
- Ranking customers according to their predicted churn risk.
- Supporting CRM teams in deciding where retention budgets should be allocated.
- Identifying customer segments requiring additional manual review.
- Monitoring changes in customer engagement and loyalty trends over time.

---

## Inappropriate Use Cases

This model must NOT be used for:

- Making final decisions without human business review.
- Determining customer eligibility for essential services.
- Discriminating against customers based on personal attributes.
- Making financial, legal, or employment-related decisions.
- Predicting customer behavior beyond the defined 60-day prediction window.
- Evaluating customers using data collected after the snapshot date.

---

# 3. Data Used

## Dataset Sources

The model uses historical customer information available on or before the snapshot date.

Primary data sources include:

- Customer demographic and acquisition attributes.
- Purchase recency, frequency, and monetary value (RFM) signals.
- Product category purchasing behavior.
- Historical return patterns.
- Customer support interaction history.
- Website and mobile application engagement metrics.
- Marketing campaign interaction signals.

---

## Leakage Prevention Strategy

To prevent data leakage:

- Only features available on or before the snapshot date were used.
- The target variable `churn_next_60d` was excluded from model inputs.
- Dataset identifiers such as `customer_id` and `snapshot_date` were excluded from training.
- The predefined train, validation, and test splits were respected during evaluation.
- Future customer behavior occurring inside the target window was never used as a predictive feature.

---

# 4. Modeling Approach

## Baseline Model

A Logistic Regression classifier was trained as a simple, interpretable benchmark model.

Purpose:

- Establish a minimum expected performance.
- Provide a transparent comparison against more complex algorithms.

---

## Final Production Model

A stronger ensemble model (Random Forest) was trained and compared against the baseline model.

Selection was based on validation performance using metrics suitable for imbalanced churn prediction, including:

- Precision
- Recall
- F1-score
- ROC-AUC

The final model selected the algorithm with the best balance between identifying churners and controlling unnecessary retention actions.

---

# 5. Performance Metrics

The model evaluation includes the following measurements:

| Metric | Business Meaning |
|---|---|
| Accuracy | Overall percentage of correct predictions. |
| Precision | Percentage of predicted churners who actually churn. |
| Recall | Percentage of actual churners successfully identified. |
| F1-score | Balance between precision and recall. |
| ROC-AUC | Ability of the model to distinguish churners from retained customers. |

The exact metric values are stored in the generated `metrics.json` file produced during model execution.

---

# 6. Decision Threshold Strategy

The default classification threshold is set to **0.40** instead of the traditional 0.50.

### Business Justification

The company considers missing a true churner more expensive than contacting a customer who may not actually churn.

A lower threshold increases recall, allowing the retention team to identify more at-risk customers while accepting a controlled number of false positive cases.

---

# 7. Model Limitations

The model has several important limitations:

- Customer preferences may change because of external market factors unavailable in historical data.
- Sudden competitor promotions or personal circumstances cannot be predicted.
- Prediction quality may decline if customer behavior patterns change significantly over time.
- The model does not understand the exact reasons behind churn; it only detects patterns associated with churn.
- Retention campaign effectiveness is not directly modeled.

---

# 8. Ethical Risks and Responsible AI Considerations

Potential risks include:

- Incorrectly classifying loyal customers as churn risks.
- Missing customers who are actually planning to leave.
- Creating unfair retention strategies if predictions are used without human oversight.

Mitigation strategies:

- Human review should be performed for high-value customers.
- Model performance should be monitored regularly across customer groups.
- Retention actions should focus on improving customer experience rather than manipulating customer behavior.
- The model should be retrained periodically using updated customer data.

---

# 9. Monitoring and Maintenance Plan

After deployment, the following indicators should be monitored:

## Data Monitoring

- Changes in feature distributions.
- Missing value increases.
- Unexpected customer behavior patterns.

## Model Monitoring

- Precision, recall, F1-score, and ROC-AUC trends.
- False Positive and False Negative rates.
- Prediction probability distribution changes.

## Business Monitoring

- Retention campaign conversion rates.
- Customer lifetime value improvement.
- Return on investment from retention spending.

Recommended retraining frequency:
Every 3 to 6 months, or earlier if significant data drift is detected.

---

# 10. Approval and Ownership

Model Owner:
Data Science Team

Primary Business Stakeholders:
Marketing Team, CRM Team, and Customer Experience Team

Deployment Status:
Internal Decision Support System

Approval Status:
Ready for controlled business evaluation after validation.
