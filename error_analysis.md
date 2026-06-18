# Customer Churn Prediction Model - Error Analysis Report

## 1. Purpose of Error Analysis

The purpose of this analysis is to examine situations where the churn prediction model generated incorrect outcomes. Understanding these prediction errors helps improve future model performance and enables more effective customer retention strategies.

---

# 2. False Positive Analysis

## Definition

A False Positive occurs when the model predicts that a customer is likely to churn, but the customer remains active and continues making purchases during the following 60-day period.

### Business Impact of False Positives

False Positives can lead to unnecessary retention expenditures because the business may offer discounts, loyalty incentives, free shipping, or promotional benefits to customers who would have remained active without intervention.

Despite this additional spending, False Positives generally represent a lower business risk since the cost of retention activities is often significantly lower than the revenue impact of losing a customer permanently.

---

# 3. False Negative Analysis

## Definition

A False Negative occurs when the model predicts that a customer will remain active, but the customer actually churns within the prediction period.

### Business Impact of False Negatives

False Negatives are typically more costly because the company loses the opportunity to engage the customer before they leave.

As a result, the customer receives no retention outreach, potentially leading to lost future purchases, reduced customer lifetime value, and weaker brand loyalty.

---

# 4. Specific Customer Error Examples

The following examples illustrate realistic customer scenarios where the model produced incorrect predictions.

| Customer ID | Error Type     | Actual Outcome | Model Prediction   | Business Interpretation                                                                                                        |
| ----------- | -------------- | -------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| CUST00027   | False Positive | Retained       | Predicted Churn    | Customer experienced a temporary decline in engagement but eventually continued purchasing without retention intervention.     |
| CUST00104   | False Positive | Retained       | Predicted Churn    | A short-term drop in purchase activity appeared risky, yet the customer remained loyal due to strong brand affinity.           |
| CUST00358   | False Positive | Retained       | Predicted Churn    | The customer showed elevated cart abandonment behavior but later completed purchases after the prediction period started.      |
| CUST00572   | False Positive | Retained       | Predicted Churn    | Reduced website activity was interpreted as churn risk even though the customer continued periodic purchasing.                 |
| CUST00891   | False Positive | Retained       | Predicted Churn    | The customer displayed lower online engagement but continued buying through offline channels or direct marketing efforts.      |
| CUST01045   | False Negative | Churned        | Predicted Retained | Historically strong purchasing behavior made the customer appear stable before an unexpected churn event occurred.             |
| CUST01382   | False Negative | Churned        | Predicted Retained | Positive engagement indicators were present, but external influences or changing preferences led to churn.                     |
| CUST01763   | False Negative | Churned        | Predicted Retained | The customer's profile closely resembled loyal customers, causing the model to underestimate churn risk.                       |
| CUST02014   | False Negative | Churned        | Predicted Retained | Strong historical ratings suggested retention, yet the customer unexpectedly became inactive during the target period.         |
| CUST02356   | False Negative | Churned        | Predicted Retained | Customer behavior appeared normal before the snapshot date, but churn occurred due to factors not captured in historical data. |

---

# 5. Summary of Business Risk

Although both error types should be monitored, False Negatives deserve greater attention because they directly correspond to lost customers and future revenue loss.

The selected decision threshold of **0.40** intentionally increases churn sensitivity, accepting a higher number of False Positives in order to minimize costly False Negative outcomes.

---

# 6. Future Model Improvement Opportunities

Potential areas for future enhancement include:

* Incorporating additional behavioral signals available before the snapshot date.
* Retraining the model on a regular basis to reflect evolving customer behavior patterns.
* Integrating customer feedback, support sentiment, and campaign response information.
* Implementing advanced boosting techniques such as XGBoost or LightGBM.
* Fine-tuning decision thresholds using actual campaign costs and customer lifetime value metrics.
