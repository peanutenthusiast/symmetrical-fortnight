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

![Final Model Comparison][/images/final_tuned_models_model_comparison.png]

When using all available features, a tuned SVM (RBF) Model provided the best scores, balancing efficiency and coverage.

- **Efficiency:** 36.3% conversion rate (> 1/3 contacted customers subscribes)
- **Coverage:** Captures 61% of all potential subscribers in the dataset
- **Real-world impact:** From 10,000 prospects, we can expect to contact ~1850 customers and gain ~670 new term deposit subscriptions.
- **Caveat:** ~6 minutes for train time, 21 seconds for train time could be a latency bottleneck

### Alternative Strategies

**1. Limited Budget / High-Cost Contacts → Use KNN**

When outreach costs are high (e.g. direct mail, dedicated advisors), minimizing
wasted contacts is the priority.

- **Efficiency:** 47.7% conversion rate — nearly 1 in 2 contacted customers subscribes
- **Coverage:** 32.4% of potential subscribers reached
- **Real-world impact:** From 10,000 prospects, contact a smaller, highly qualified
  pool with a near coin-flip conversion rate — maximizing ROI per contact
- **Latency:** Trains in 0.17 seconds, scores in 1.38 seconds, more ideal for real-time or large-scale scoring pipeliens

**2. Maximum Market Penetration → Use Decision Tree**

When the goal is to capture as many subscribers as possible regardless of contact volume:

- **Efficiency:** 30% conversion rate — 3 in 10 contacts convert
- **Coverage:** 64% of all potential subscribers reached — the highest recall of
  any model
- **Real-world impact:** Ideal for low-cost outreach channels (e.g. email, SMS)
  where volume is affordable and missing a subscriber is the greater risk

**3. Explainability & Regulatory Compliance → Use Logistic Regression**

When decisions must be justified to stakeholders or auditors:

- **Efficiency:** 33% conversion rate, on par with SVM
- **Coverage:** 61% recall, matching SVM's reach
- **Probability calibration:** Highest ROC-AUC at 0.787 — best model for
  generating reliable subscription probability scores for lead ranking
- **Speed advantage:** Trains in 0.17 seconds and scores in 0.03 seconds —
  over **2,000× faster** than SVM, making it ideal for real-time or
  large-scale scoring pipelines

### Key Insights from Feature Analysis

![Feature Importances and Coefficients][/images/feature_importance_and_coefficients.png]

1. **Macroeconomic economic conditions dominate** `euribor3m` adn `cons.conf.idx` are strongest numerical predictors. Campaigns launched during periods of higher interest rates and consumer confidence yield better conversion rates.
2. **Prior campaign success is strongest client-level signal.** Clients who subscribed in a previous campaign are highest-value re-engagement targets in any scenario.
3. **Contact fatigue lowers probability.** The more a client has been contacted, the less likely they are to subscribe. Consider a contact cap policy.
4. **Timing matters.** March and October outperform all other months. August, September, and November underperform. High-signal months can lift conversion without changing target audience.
5. **Segment by life stage.** Retirees, students, and university-educated clients show the highest subscription likelihood. Blue-collor, unemployed, basic-education segments show lowest.