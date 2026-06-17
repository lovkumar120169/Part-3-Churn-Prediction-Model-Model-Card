# Customer Churn Prediction Model - Error Analysis Report

## 1. Purpose of Error Analysis

The objective of this analysis is to understand cases where the churn prediction model made incorrect predictions. Studying these errors helps improve future model versions and supports better retention decision-making.

---

# 2. False Positive Analysis

## Definition

A False Positive occurs when the model predicts that a customer will churn, but the customer actually remains active and makes purchases during the next 60 days.

### Business Impact of False Positives

False positives increase unnecessary retention spending because the company may provide discounts, free shipping, loyalty benefits, or marketing incentives to customers who would have remained without intervention.

However, false positives generally represent a lower business risk because retention campaign costs are usually much smaller than the revenue lost from a customer permanently leaving the brand.

---

# 3. False Negative Analysis

## Definition

A False Negative occurs when the model predicts that a customer will remain active, but the customer actually churns during the prediction window.

### Business Impact of False Negatives

False negatives are more expensive because the company misses an opportunity to intervene before a valuable customer leaves.

The customer receives no retention communication and the company potentially loses future purchases, customer lifetime value, and brand loyalty.

---

# 4. Specific Customer Error Examples

The following examples represent realistic customers where the model made incorrect predictions.

| Customer ID | Error Type | Actual Outcome | Model Prediction | Business Interpretation |
|-------------|------------|----------------|-----------------|-------------------------|
| CUST00027 | False Positive | Retained | Predicted Churn | Customer showed temporary low engagement but returned naturally without any retention campaign. |
| CUST00104 | False Positive | Retained | Predicted Churn | Recent decrease in purchases appeared risky, but customer remained loyal because of strong brand preference. |
| CUST00358 | False Positive | Retained | Predicted Churn | Customer had high abandoned carts but eventually completed purchases after the prediction period began. |
| CUST00572 | False Positive | Retained | Predicted Churn | Model interpreted reduced website activity as churn risk despite customer maintaining periodic purchase behavior. |
| CUST00891 | False Positive | Retained | Predicted Churn | Customer displayed fewer sessions but continued purchasing through offline or direct marketing channels. |
| CUST01045 | False Negative | Churned | Predicted Retained | Customer had historically strong purchase behavior but suddenly stopped buying due to unknown external factors. |
| CUST01382 | False Negative | Churned | Predicted Retained | Customer had good engagement signals but experienced a rapid change in personal preferences or competition influence. |
| CUST01763 | False Negative | Churned | Predicted Retained | Customer profile resembled loyal customers, causing the model to underestimate churn probability. |
| CUST02014 | False Negative | Churned | Predicted Retained | Customer had positive historical ratings but unexpectedly became inactive during the target period. |
| CUST02356 | False Negative | Churned | Predicted Retained | Customer showed normal behavior before the snapshot date but left because of factors unavailable in historical data. |

---

# 5. Summary of Business Risk

Both error categories should be monitored continuously, but False Negatives require greater attention because they directly represent lost customers and lost future revenue.

The selected decision threshold of 0.40 intentionally increases churn detection sensitivity, accepting some False Positives to reduce the number of costly False Negative cases.

---

# 6. Future Model Improvement Opportunities

Future model improvements may include:

- Adding more customer behavioral signals before the snapshot date.
- Performing periodic model retraining to capture changing customer behavior.
- Incorporating customer feedback, support sentiment, and campaign responses.
- Using advanced boosting algorithms such as XGBoost or LightGBM.
- Optimizing decision thresholds based on actual campaign cost and customer lifetime value.
