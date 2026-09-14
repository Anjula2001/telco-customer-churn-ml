# Telco Customer Churn Prediction

An end-to-end machine learning project for predicting customer churn using the Telco Customer Churn dataset.

The project focuses on understanding customer churn patterns, comparing multiple classification algorithms, evaluating model performance, and selecting an appropriate operating threshold for a customer retention use case.

## Project Overview

Customer churn is an important business problem for telecom companies. Identifying customers who are likely to leave can help businesses take proactive retention actions.

In this project, customer data is analyzed and several machine learning classification models are trained and evaluated to predict whether a customer is likely to churn.

### Objective

Build and evaluate a machine learning model that can identify customers who are at higher risk of churn.

## Dataset

**Dataset:** Telco Customer Churn
**Source:** IBM Sample Dataset / Kaggle

The dataset contains information about 7,043 telecom customers, including:

* Customer demographics
* Tenure
* Contract information
* Payment method
* Internet services
* Monthly charges
* Total charges
* Churn status

## Machine Learning Workflow

```text
Data Loading
     ↓
Data Cleaning
     ↓
Exploratory Data Analysis
     ↓
Feature Engineering & Encoding
     ↓
Train / Test Split
     ↓
Feature Scaling
     ↓
Model Training
     ↓
Cross-Validation
     ↓
Hyperparameter Tuning
     ↓
Model Evaluation
     ↓
Threshold Tuning
     ↓
Final Model Selection
```

## Models Evaluated

The following classification algorithms were evaluated:

* Logistic Regression
* Decision Tree
* Random Forest
* K-Nearest Neighbors (KNN)

### Cross-Validation Results

| Model               | Mean 5-Fold CV Accuracy |
| ------------------- | ----------------------: |
| Logistic Regression |                  80.44% |
| Random Forest       |                  78.84% |
| KNN                 |                  76.25% |
| Decision Tree       |                  72.67% |

Logistic Regression achieved the strongest baseline performance among the tested models.

## Final Model

The selected model is **Logistic Regression**.

A classification threshold of **0.3** was selected instead of the default 0.5 because the primary business objective is to identify customers who are likely to churn.

### Final Results

| Metric          | Result |
| --------------- | -----: |
| Accuracy        | 75.00% |
| Churn Precision |    52% |
| Churn Recall    |    75% |
| Churn F1-score  |   0.62 |
| ROC-AUC         |  0.842 |

At the selected threshold of 0.3, the model identified **282 of 374 actual churn customers** in the test set.

The lower threshold increases churn recall while also increasing false positives. In a real business environment, the final threshold should be determined using the actual costs of false positives and false negatives.

## Key EDA Findings

The exploratory analysis revealed several important patterns:

* Month-to-month contract customers had substantially higher churn rates.
* Electronic check users showed a high churn rate.
* Customers with shorter tenure were more likely to churn.
* Churned customers had higher average monthly charges.
* Fiber optic customers showed higher churn compared with DSL customers.
* Tenure and TotalCharges had a strong positive correlation.

## Repository Structure

```text
telco-customer-churn-ml/
│
├── Telco Customer Churn — EDA & ML.ipynb
└── README.md
```

> The machine learning model is currently developed and evaluated in the Kaggle notebook. Model packaging, inference, API development, and deployment are planned as the next stage of the project.

## Current Status

### Completed

* [x] Data cleaning
* [x] Exploratory data analysis
* [x] Feature encoding
* [x] Train/test split
* [x] Feature scaling
* [x] Multiple classification models
* [x] Cross-validation
* [x] Hyperparameter tuning
* [x] Confusion matrix analysis
* [x] ROC-AUC evaluation
* [x] Threshold tuning
* [x] Class imbalance analysis
* [x] Final model selection
* [x] Kaggle notebook publication

## Kaggle Notebook

The complete exploratory analysis and machine learning workflow is available on Kaggle:

https://www.kaggle.com/code/anjulaprasad/telco-customer-churn-eda-ml

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook
* Kaggle

## Disclaimer

This project is an educational and portfolio machine learning project based on a publicly available sample dataset.

The reported model performance should not be interpreted as production performance for an actual telecom company. A production system would require additional validation, business cost analysis, monitoring, and testing on real-world data.

## Author

**Anjula Prasad**

Software Engineer | AI/ML Engineer

* GitHub: [Anjula2001](https://github.com/Anjula2001)
* Kaggle: [Anjula Prasad](https://www.kaggle.com/anjulaprasad)
