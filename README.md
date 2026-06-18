# D2C Customer Churn Prediction System

## Project Overview

This repository provides a complete machine learning workflow designed to predict customer churn for a Direct-to-Consumer (D2C) personal care company.

The main goal is to identify customers who are at risk of ceasing purchases within the upcoming 60 days, enabling CRM and marketing teams to execute targeted retention initiatives proactively.

The project includes:

* Data preparation and preprocessing
* Explicit data leakage prevention
* Baseline and advanced machine learning models
* Model evaluation using business-relevant metrics
* Decision threshold selection
* Feature importance analysis
* Error analysis
* Model documentation
* Saved production-ready model artifacts

---

## Business Objective

Customer retention resources are limited. Offering incentives to every customer increases costs and lowers overall campaign effectiveness.

This churn prediction solution enables the business to:

* Detect customers with a high likelihood of churn.
* Prioritize retention efforts more effectively.
* Minimize potential future revenue loss.
* Strengthen customer engagement initiatives.
* Enable data-driven CRM decision-making.

---

## Dataset Used

The model is trained using the following file:

`rfm_modeling_snapshot.csv`

The dataset contains only features generated from information available before the customer snapshot date.

Included feature categories:

* Customer profile information
* Acquisition channel
* RFM behavior:

  * Recency
  * Frequency
  * Monetary value
* Return behavior
* Support interaction history
* Web and application activity
* Marketing engagement signals

The target variable is:

`churn_next_60d`

which identifies whether a customer stopped making purchases during the subsequent 60-day prediction window.

---

## Leakage Prevention Strategy

To maintain realistic and trustworthy model performance, the following safeguards were implemented:

* Customer ID was excluded from model features.
* Snapshot date was excluded from model features.
* The target variable was never included as an input feature.
* Dataset split indicators were never used for training.
* Only information available before the snapshot date was utilized.

These controls ensure that future information cannot influence churn predictions.

---

## Repository Structure

```text
D2C-Churn-Prediction/

├── churn_model.ipynb
├── model.pkl
├── metrics.json
├── error_analysis.md
├── model_card.md
├── requirements.txt
└── README.md
```

---

## Environment Setup

Install all required dependencies using:

```bash
pip install -r requirements.txt
```

---

## Running the Project

### Step 1: Upload Dataset

Upload the provided D2C churn dataset package to Google Drive.

### Step 2: Open Notebook

Open:

`churn_model.ipynb`

using Google Colab.

### Step 3: Verify Dataset Path

The notebook expects the dataset to be available at:

```text
/content/drive/MyDrive/d2c churn data package/
```

### Step 4: Execute All Cells

Running the notebook will automatically:

* Load the modeling dataset.
* Perform leakage checks.
* Create train, validation, and test datasets.
* Train the Logistic Regression baseline model.
* Train the Random Forest model.
* Compare model performance.
* Select the final model.
* Apply the business decision threshold.
* Evaluate final performance.
* Generate feature importance visualizations.
* Save model artifacts.

---

## Generated Output Files

After successful execution, the repository will contain the following outputs:

### model.pkl

Stores the complete trained machine learning pipeline, including preprocessing steps and the final classification model.

### metrics.json

Contains:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC Score
* Confusion Matrix values
* Selected threshold

---

## Loading the Saved Model

Example:

```python
import joblib

model = joblib.load("model.pkl")

probability = model.predict_proba(customer_data)[:, 1]

prediction = (probability >= 0.40).astype(int)
```

---

## Decision Threshold

The selected classification threshold is **0.40**.

A lower threshold was intentionally chosen because failing to identify a customer who is likely to churn has a greater business impact than sending a retention offer to a customer who would have remained active.

This approach improves churn detection recall while maintaining reasonable campaign costs.

---

## Evaluation Metrics

The model is assessed using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

Accuracy alone is not sufficient because churn prediction requires balancing multiple types of business-related prediction errors.

---

## Error Analysis

The `error_analysis.md` file includes:

* False Positive examples.
* False Negative examples.
* Business implications of prediction errors.
* Customer-level interpretation of model outcomes.

---

## Responsible Usage

This model is intended to function as a decision-support system.

Predictions should assist CRM and marketing teams, while important customer-related decisions should continue to involve human review and judgment.

The model should not be used for legal, employment, financial, or discriminatory purposes.

---

## Future Improvements

Potential future enhancements include:

* Hyperparameter optimization.
* XGBoost or LightGBM implementation.
* Customer lifetime value integration.
* Continuous monitoring for data drift.
* Automated model retraining.

---

## Project Information

### Project Name

D2C Customer Churn Intelligence - Part 3

### Objective

Production-ready customer churn prediction and documentation pipeline.
