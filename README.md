# Investment Campaign Case Study

Machine learning case study focused on predicting which bank clients are most likely to respond positively to an investment campaign.

This project was built as part of a bootcamp team assignment. The workflow combines SQL-style data extraction from a SQLite database, feature engineering from client balance history, model comparison across multiple classifiers, and prioritization of clients for a second campaign round.

## Problem

The goal is to help a bank target the right customers for an investment campaign.

Given historical client information and the outcome of a previous campaign, the task is to:

- prepare a modeling dataset from relational tables
- engineer useful customer-level features
- train and compare classification models
- score unseen clients for the next campaign round

## Dataset

The source data lives in `case_study/data.db` and contains four tables:

- `client`: demographic information such as age, job, marital status, education, and gender
- `client_products`: product ownership indicators such as deposits, loan, insurance, and mortgage
- `balances`: dated account balances by client and currency
- `inv_campaign_eval`: historical campaign outcome (`poutcome`)

The modeling dataset was built by joining these tables and aggregating balance history into customer-level features.

## Feature Engineering

The final exported training and test sets contain 8 model features:

- `has_deposits_enc`
- `age`
- `last_balance`
- `min_balance`
- `has_mortgage_enc`
- `max_balance`
- `mean_balance`
- `job_enc`

Categorical fields were label-encoded, missing values were handled in the notebooks, and numeric inputs were scaled before training several models.

## Models Compared

The project compares five classifiers:

- Random Forest
- Logistic Regression
- K-Nearest Neighbors
- AdaBoost
- Neural Network

Saved trained artifacts are included in `case_study/` as `.joblib`, `.h5`, and `.npy` files.

## Results

Test-set metrics were saved in `case_study/results_on_test_metrics.csv`.

Metric order in the file:

1. F1 Score
2. AUC-ROC
3. AUC-PR
4. Accuracy

| Model | F1 | AUC-ROC | AUC-PR | Accuracy |
| --- | ---: | ---: | ---: | ---: |
| Random Forest | 0.672 | 0.749 | 0.655 | 0.699 |
| Logistic Regression | 0.679 | 0.746 | 0.646 | 0.700 |
| KNN | 0.660 | 0.716 | 0.610 | 0.670 |
| AdaBoost | 0.681 | 0.760 | 0.681 | 0.699 |
| Neural Network | 0.693 | 0.751 | 0.642 | 0.696 |

Based on the exported test metrics, the neural network produced the best F1 score, while AdaBoost achieved the strongest AUC-ROC and AUC-PR values. The project therefore shows the tradeoff between ranking quality and threshold-based classification performance.

## Repository Structure

```text
.
├── README.md
├── Investment_Campaign_Case_study.pptx
├── app.ipynb
└── case_study/
    ├── Master_notebook.ipynb
    ├── Zuzana.ipynb
    ├── Vojta_data.ipynb
    ├── Vojta_day_3.ipynb
    ├── Daniela.ipynb
    ├── data.db
    ├── X_train.csv / X_test.csv / y_train.csv / y_test.csv
    ├── results_on_train_metrics.csv
    ├── results_on_test_metrics.csv
    ├── second_phase_target.csv
    ├── second_phase_target_labeled.csv
    ├── id_results.csv
    └── saved model artifacts
```

## How To Explore The Project

The main end-to-end workflow is in:

- `case_study/Master_notebook.ipynb`

Supporting notebooks from individual team members:

- `case_study/Zuzana.ipynb`
- `case_study/Vojta_data.ipynb`
- `case_study/Vojta_day_3.ipynb`
- `case_study/Daniela.ipynb`

## Tech Stack

- Python
- pandas
- NumPy
- scikit-learn
- TensorFlow / Keras
- SQLite
- matplotlib
- seaborn
- plotly
- joblib

## Running The Project

This repository currently ships as a notebook-based analysis rather than a packaged application.

To run it locally:

1. Create a Python environment with the libraries listed above.
2. Open `case_study/Master_notebook.ipynb` in Jupyter Notebook or VS Code.
3. Run the notebook cells in order.
4. Review the exported CSV and model files in `case_study/`.

## Portfolio Summary

This project demonstrates:

- relational data extraction from SQLite
- feature engineering from transactional history
- preprocessing and scaling for ML workflows
- comparison of classical ML models against a neural network
- conversion of model scores into a campaign target list

## Notes

- The included Dash files are starter experiments and are not the main deliverable.
- This repository is strongest as a data science / machine learning case study, not as a deployed web app.
- Before publishing widely, review the included data and prediction outputs to make sure they are safe to share publicly.
