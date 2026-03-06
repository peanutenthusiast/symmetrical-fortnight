# Comparing Classifiers  

This project compares the following classification algorithms using [UCI Bank Marketing dataset](https://archive.ics.uci.edu/ml/datasets/bank+marketing):

- logistic regression
- k-nearest neighbors
- decision trees
- SVF
to identify the best model for predicting whether a customer will subscribe to a term deposit based on a marketing campaign.

## Business Objective

A Portuguese bank conducted 17 marketing campaigns with the goal of increasing subscriptions to a term deposit investment product. With each observation equal to a client phone call, this project leverages the previously listed ML models to:

- optimize contract strategy via prioritization of high-probability prospects
- reduce campaign costs by minimizing outreach to unlikely converters
- improve conversion rates through targeted, data-driven customer selection

## Dataset

The dataset is significantly imbalanced with only 10% clients who proceeded with term deposit subscriptions. 

## Data Preparation

The nobebook includes:

- one-hot encoding for categorical variables
- removal of all "unknown" values, except for those in the default column
- train/test split of the dataset
- various visualizations, including correlation heatmaps, numerical distributions, categorical distributions

## Evaluation Metrics

The following metrics were employed to compare the models:

- Accuracy
- F1 Score
- ROC-AUC
- Recall
- Confusion Matrix

## Findings & Insight

When using all available features, a turned SVM with the params:
```
  model__gamma: scale
  model__class_weight: balanced
  model__C: 0.5
```

performed the best on a test set of 20% of the entire data with the following scores:

accuracy = 0.837364	
precision =	0.363128
recall = 0.610329	
f1 = 0.455342
f1_weighted = 0.854390
f1_macro = 0.837364
roc_auc = 0.770580