
# D2C Customer Churn Prediction System

## Project Overview

This repository contains a complete machine learning pipeline for predicting customer churn for a Direct-to-Consumer (D2C) personal care brand.

The objective is to identify customers who are likely to stop purchasing within the next 60 days so that the marketing and CRM teams can launch targeted retention campaigns.

The project includes:
- Data preparation and preprocessing
- Explicit data leakage prevention
- Baseline and advanced machine learning models
- Model evaluation using business-relevant metrics
- Decision threshold selection
- Feature importance analysis
- Error analysis
- Model documentation
- Saved production-ready model artifacts

---

## Business Objective

Retention budgets are limited. Sending incentives to every customer increases marketing costs and reduces campaign efficiency.

This churn prediction system helps the business:

- Identify customers with high churn probability.
- Prioritize retention campaigns.
- Reduce future revenue loss.
- Improve customer engagement strategy.
- Support data-driven CRM decisions.

---

## Dataset Used

The model uses the file:

rfm_modeling_snapshot.csv

The dataset contains only features created using information available before the customer snapshot date.

Included feature categories:

- Customer profile information
- Acquisition channel
- RFM behavior:
  - Recency
  - Frequency
  - Monetary value
- Return behavior
- Support interaction history
- Web and application activity
- Marketing engagement signals

The target variable is:

churn_next_60d

which indicates whether a customer stopped purchasing during the next 60-day prediction period.

---

## Leakage Prevention Strategy

To ensure realistic model performance, the following rules were applied:

- Customer ID was removed from model inputs.
- Snapshot date was removed from model inputs.
- Target variable was never used as a feature.
- Dataset split labels were never used as model features.
- Only information available before the snapshot date was considered.

This prevents future information from influencing churn predictions.

---

## Repository Structure

D2C-Churn-Prediction/

├── churn_model.ipynb  
├── model.pkl  
├── metrics.json  
├── error_analysis.md  
├── model_card.md  
├── requirements.txt  
└── README.md  

---

## Environment Setup

Install required libraries using:

pip install -r requirements.txt

---

## Running the Project

### Step 1: Upload Dataset

Upload the provided D2C churn dataset package to Google Drive.

### Step 2: Open Notebook

Open:

churn_model.ipynb

using Google Colab.

### Step 3: Verify Dataset Path

The notebook expects the following path:

/content/drive/MyDrive/d2c churn data package/

### Step 4: Execute All Cells

Running the notebook will automatically:

- Load the modeling dataset.
- Perform leakage checks.
- Create train, validation, and test datasets.
- Train Logistic Regression baseline model.
- Train Random Forest model.
- Compare model performance.
- Select the final model.
- Apply business decision threshold.
- Evaluate final performance.
- Generate feature importance charts.
- Save model artifacts.

---

## Generated Output Files

After successful execution, the repository will contain:

### model.pkl

Contains the complete trained machine learning pipeline including preprocessing and classification model.

### metrics.json

Contains:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC Score
- Confusion Matrix values
- Selected threshold

---

## Loading the Saved Model

Example:

import joblib

model = joblib.load("model.pkl")

probability = model.predict_proba(customer_data)[:, 1]

prediction = (probability >= 0.40).astype(int)

---

## Decision Threshold

The selected threshold is 0.40.

A lower threshold is chosen because missing a customer who is likely to churn has a higher business cost than sending a retention offer to a customer who would have stayed.

This strategy increases churn detection recall while keeping campaign costs manageable.

---

## Evaluation Metrics

The model is evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC

Accuracy alone is not considered sufficient because churn prediction requires balancing multiple types of business errors.

---

## Error Analysis

The file error_analysis.md includes:

- False Positive examples.
- False Negative examples.
- Business impact of prediction mistakes.
- Customer-level case interpretations.

---

## Responsible Usage

The model should be used as a decision-support tool.

Predictions should assist CRM and marketing teams, but important customer decisions should include human review.

The model should not be used for legal, employment, financial, or discriminatory decisions.

---

## Future Improvements

Potential future enhancements:

- Hyperparameter optimization.
- XGBoost or LightGBM implementation.
- Customer lifetime value integration.
- Continuous monitoring for data drift.
- Automated model retraining.

---

## Project Information

Project Name:
D2C Customer Churn Intelligence - Part 3

Objective:
Production-ready customer churn prediction and documentation pipeline.
