# Investment Campaign Targeting with Machine Learning

Machine learning case study focused on predicting which bank clients are most likely to respond positively to an investment campaign.

## Project Overview

This project explored how a bank could improve the targeting of an investment campaign using historical client and campaign data.

The task was approached as a binary classification problem:
- prepare a modeling dataset from relational tables
- engineer customer-level features
- train and compare multiple classification models
- score unseen clients for the next campaign round

The project combined SQL-style data extraction from a SQLite database, feature engineering from client balance history, model comparison across several classifiers, and prioritization of clients for a second campaign round.

## Business Goal

The goal was to help a bank identify the clients most likely to invest, instead of selecting campaign targets randomly.

Using historical client information and the results of a previous campaign, the objective was to build a model that could rank customers by likelihood of positive response and support more effective campaign targeting.

## Dataset

The source data was stored in a SQLite database and included four main tables:

- `client` — demographic information such as age, job, marital status, education, and gender
- `client_products` — product ownership indicators such as deposits, loan, insurance, and mortgage
- `balances` — dated account balances by client and currency
- `inv_campaign_eval` — historical campaign outcome (`poutcome`)

The modeling dataset was built by joining these tables and aggregating balance history into customer-level features.

## Feature Engineering

The final modeling dataset used 8 selected features:

- `has_deposits_enc`
- `age`
- `last_balance`
- `min_balance`
- `has_mortgage_enc`
- `max_balance`
- `mean_balance`
- `job_enc`

Categorical variables were label-encoded, missing values were handled in the notebooks, and numeric features were scaled before model training.

## Models Compared

The project compared five classification models:

- Random Forest
- Logistic Regression
- K-Nearest Neighbors
- AdaBoost
- Neural Network

## Results

Model performance was evaluated on the test set using the following metrics:

- F1 Score
- AUC-ROC
- AUC-PR
- Accuracy

| Model | F1 | AUC-ROC | AUC-PR | Accuracy |
|---|---:|---:|---:|---:|
| Random Forest | 0.672 | 0.749 | 0.655 | 0.699 |
| Logistic Regression | 0.679 | 0.746 | 0.646 | 0.700 |
| KNN | 0.660 | 0.716 | 0.610 | 0.670 |
| AdaBoost | 0.681 | 0.760 | 0.681 | 0.699 |
| Neural Network | 0.693 | 0.751 | 0.642 | 0.696 |

The Neural Network achieved the highest F1 score, while AdaBoost showed the strongest AUC-ROC and AUC-PR values. Logistic Regression remained highly competitive and offered a strong balance of performance, simplicity, and interpretability.

## Technical Workflow

The main workflow included:

- extracting and joining relational data from SQLite
- cleaning and preprocessing client-level data
- engineering aggregated balance-based features
- encoding categorical variables
- scaling numeric features
- training and tuning multiple classification models
- generating scores for unseen clients for the next campaign round

