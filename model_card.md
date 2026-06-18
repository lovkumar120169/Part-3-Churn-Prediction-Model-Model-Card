# D2C Customer Churn Prediction Model Card

## 1. Model Overview

### Model Name

D2C Customer Churn Prediction Model

### Model Version

Version 1.0

### Business Objective

This machine learning solution estimates the likelihood that a customer will churn within the 60-day period following the snapshot date.

The model assists marketing, CRM, and customer retention teams in identifying customers who may benefit from proactive engagement initiatives, including personalized offers, loyalty incentives, product recommendations, or service enhancement programs.

Its primary purpose is to optimize the allocation of retention resources rather than applying costly campaigns across the entire customer base.

---

# 2. Intended Use

## Appropriate Use Cases

The model is intended for:

* Prioritizing customers for retention initiatives.
* Ranking customers based on predicted churn likelihood.
* Assisting CRM teams in allocating retention budgets more effectively.
* Identifying customer groups that may require additional manual assessment.
* Tracking changes in customer loyalty and engagement patterns over time.

---

## Inappropriate Use Cases

This model should NOT be used for:

* Making final customer decisions without human review.
* Determining access to essential products or services.
* Discriminatory decision-making based on personal characteristics.
* Financial, legal, employment, or regulatory decision-making.
* Predicting customer behavior beyond the defined 60-day horizon.
* Evaluating customers using information collected after the snapshot date.

---

# 3. Data Used

## Dataset Sources

The model is trained using historical customer information available on or before the designated snapshot date.

Primary data sources include:

* Customer demographic and acquisition-related attributes.
* RFM indicators, including recency, frequency, and monetary value.
* Product category purchasing behavior.
* Historical return activity.
* Customer support interaction records.
* Website and mobile application engagement metrics.
* Marketing and campaign engagement signals.

---

## Leakage Prevention Strategy

Several safeguards were implemented to prevent data leakage:

* Only features available on or before the snapshot date were included.
* The target variable `churn_next_60d` was excluded from model inputs.
* Identifiers such as `customer_id` and `snapshot_date` were removed before training.
* Predefined training, validation, and testing splits were strictly maintained.
* Future customer activity occurring within the prediction window was never used as a predictive feature.

---

# 4. Modeling Approach

## Baseline Model

A Logistic Regression classifier was developed as a simple and interpretable benchmark model.

### Purpose:

* Establish a baseline performance benchmark.
* Enable transparent comparison with more advanced algorithms.

---

## Final Production Model

A more robust ensemble-based model (Random Forest) was trained and evaluated against the baseline model.

Model selection was based on validation performance using metrics appropriate for churn prediction and class imbalance, including:

* Precision
* Recall
* F1-score
* ROC-AUC

The final model was chosen based on its ability to balance churn detection effectiveness with minimizing unnecessary retention actions.

---

# 5. Performance Metrics

The model evaluation includes the following metrics:

| Metric    | Business Meaning                                                             |
| --------- | ---------------------------------------------------------------------------- |
| Accuracy  | Overall proportion of correctly classified customers.                        |
| Precision | Percentage of predicted churners who actually churned.                       |
| Recall    | Percentage of actual churners successfully identified by the model.          |
| F1-score  | Combined measure balancing precision and recall.                             |
| ROC-AUC   | Ability of the model to distinguish between churners and retained customers. |

Detailed metric values are stored in the generated `metrics.json` file produced during model execution.

---

# 6. Decision Threshold Strategy

The default classification threshold is configured at **0.40** rather than the conventional 0.50.

### Business Justification

From a business perspective, failing to identify a genuine churn-risk customer is more costly than contacting a customer who ultimately remains active.

Using a lower threshold improves recall, allowing the retention team to capture more at-risk customers while accepting a manageable number of false positive predictions.

---

# 7. Model Limitations

Several limitations should be considered when interpreting model outputs:

* Customer preferences may shift due to external market influences that are not reflected in historical data.
* Unexpected competitor actions or personal customer circumstances cannot be anticipated.
* Model performance may deteriorate if customer behavior evolves significantly over time.
* The model identifies churn-related patterns but does not determine the exact reasons behind churn.
* The effectiveness of retention campaigns is not directly incorporated into the model.

---

# 8. Ethical Risks and Responsible AI Considerations

Potential risks include:

* Incorrectly identifying loyal customers as churn risks.
* Failing to detect customers who are genuinely planning to leave.
* Creating unfair retention practices if predictions are used without appropriate human oversight.

### Mitigation Strategies

* High-value customer cases should undergo human review before action is taken.
* Model performance should be monitored regularly across different customer groups.
* Retention initiatives should focus on improving customer experience rather than influencing behavior unfairly.
* The model should be retrained periodically using updated customer information.

---

# 9. Monitoring and Maintenance Plan

Following deployment, the following indicators should be continuously monitored:

## Data Monitoring

* Shifts in feature distributions.
* Increases in missing data.
* Unusual or unexpected customer behavior trends.

## Model Monitoring

* Trends in precision, recall, F1-score, and ROC-AUC.
* False Positive and False Negative rates.
* Changes in prediction probability distributions.

## Business Monitoring

* Retention campaign conversion performance.
* Improvements in customer lifetime value.
* Return on investment from retention activities.

### Recommended Retraining Frequency

Every 3 to 6 months, or sooner if significant data drift or performance degradation is detected.

---

# 10. Approval and Ownership

### Model Owner

Data Science Team

### Primary Business Stakeholders

Marketing Team, CRM Team, and Customer Experience Team

### Deployment Status

Internal Decision Support System

### Approval Status

Approved for controlled business evaluation following validation and review.
