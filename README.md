# Telco Customer Churn Prediction

A machine learning portfolio project covering customer churn analysis, model comparison, validation-based threshold selection, and browser-based deployment.

## Live Demo

🤗 [Try the Telco Churn Predictor](https://huggingface.co/spaces/amarakoon2001/telco-churn-predictor)

Enter customer details to estimate churn probability using the trained Logistic Regression pipeline. Predictions run entirely in your browser.

## Project Overview

The project explores customer churn patterns and evaluates classification models for identifying customers who may leave a telecom service.

The final implementation combines preprocessing and Logistic Regression in a scikit-learn Pipeline. The classification threshold is selected using a separate validation set.

## Dataset

- **Dataset:** Telco Customer Churn
- **Source:** IBM sample dataset, available on Kaggle
- **Customers:** 7,043
- **Input attributes:** 19, excluding customer ID and target

Attributes include demographics, tenure, contract type, payment method, subscribed services, monthly charges, and total charges.

Blank TotalCharges values for 11 zero-tenure customers are converted to zero.

## Final Workflow

1. Load, inspect, and clean the data.
2. Explore customer churn patterns.
3. Create stratified training, validation, and test splits.
4. Build a preprocessing and classification pipeline.
5. Evaluate the pipeline using cross-validation on training data.
6. Fit the pipeline on the training split.
7. Select a classification threshold using validation F1-score.
8. Evaluate the fixed model and threshold on the test split.
9. Export the pipeline and deploy browser-based inference.

## Earlier Model Experiments

The notebook initially compared:

| Model | Mean 5-Fold CV Accuracy |
| --- | ---: |
| Logistic Regression | 80.44% |
| Random Forest | 78.84% |
| KNN | 76.25% |
| Decision Tree | 72.67% |

These are historical exploratory results from the earlier workflow. Logistic Regression and KNN used scaling fitted before cross-validation, so these scores are not leakage-free estimates.

The final Logistic Regression pipeline was evaluated separately using the procedure below.

## Final Pipeline

- **Numeric features:** StandardScaler
- **Categorical features:** OneHotEncoder
- **Classifier:** Logistic Regression
- **Cross-validation:** 5-fold stratified CV with shuffling
- **Mean training CV ROC-AUC:** 0.848

Preprocessing is fitted within each cross-validation fold.

### Data Split

| Split | Customers | Proportion |
| --- | ---: | ---: |
| Training | 4,225 | 60% |
| Validation | 1,409 | 20% |
| Test | 1,409 | 20% |

### Threshold Selection

A threshold of **0.38** achieved the highest validation F1-score among thresholds from 0.05 to 0.95 in steps of 0.01.

The threshold was fixed before evaluating the updated pipeline on the test split. A real deployment should select its operating threshold using business costs and retention objectives.

## Updated Test Results

| Metric | Result |
| --- | ---: |
| Classification threshold | 0.38 |
| Accuracy | 77.64% |
| ROC-AUC | 0.843 |
| Churn precision | 56.5% |
| Churn recall | 68.7% |
| Churn F1-score | 0.620 |

### Confusion Matrix

| Actual / Predicted | Stay | Churn |
| --- | ---: | ---: |
| Stay | 837 | 198 |
| Churn | 117 | 257 |

The model identified **257 of 374 actual churn customers**, missed 117, and flagged 198 non-churn customers.

## Key EDA Findings

- Month-to-month customers had higher observed churn rates.
- Electronic check users had higher observed churn rates.
- Customers with shorter tenure were more likely to churn.
- Churned customers had higher average monthly charges.
- Fiber optic customers showed higher churn than DSL customers.
- Tenure and TotalCharges were strongly positively correlated.

These are associations in the sample dataset, not evidence of causation.

## Deployment

The demo is hosted as a Hugging Face Static Space.

It reproduces the fitted pipeline in JavaScript using the exported numeric scaling parameters, categorical encoding, model coefficients, and intercept.

- Predictions run locally in the browser.
- Customer inputs are not sent to a prediction server.
- JavaScript predictions were compared with the Python pipeline on 200 generated customer profiles and matched within floating-point precision.

## Repository Contents

| Path | Purpose |
| --- | --- |
| `telco-customer-churn-eda-ml.ipynb` | EDA, experiments, final pipeline, evaluation, and export |
| `demo/index.html` | Interactive demo with browser-based inference |
| `README.md` | Project documentation |

## Kaggle Notebook

[View the complete notebook](https://www.kaggle.com/code/anjulaprasad/telco-customer-churn-eda-ml)

## Tech Stack

Python, Pandas, NumPy, Matplotlib, Seaborn, scikit-learn, Joblib, Jupyter Notebook, Kaggle, HTML, CSS, JavaScript, and Hugging Face Spaces.

## Limitations

This is an educational portfolio project using a public sample dataset.

Preprocessing and threshold selection are now separated correctly. However, the test split had already been inspected during earlier experiments, so the reported results remain exploratory rather than an independent final evaluation.

Probabilities have not been separately calibrated. Production use would require independent data, business cost analysis, monitoring, and validation for the intended telecom provider.

## Author

**Anjula Prasad**

- [GitHub](https://github.com/Anjula2001)
- [Kaggle](https://www.kaggle.com/anjulaprasad)
