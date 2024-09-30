# ML Newsletter Campaign Predictions

Educational machine learning project aimed at optimizing newsletter marketing processes by predicting users who are likely to make a purchase in the near future


## Project Overview

This project aims to predict the **likelihood of a customer making a purchase within the next 90 days** in an online shop using machine learning techniques. By analyzing customer purchase history and interaction with marketing campaigns, the developed model allows targeted marketing efforts, optimized newsletter campaigns, and overall improved customer engagement.

## Change Log

- [2024.09.29 17:15](https://github.com/eugen-hoppe/ml_rebuy_prediction/tree/145f977a45b95af77b8673ceb7d0ac4a75eb5f4a) - v1.0: BETA
- [2024.09.30 10:30](https://github.com/eugen-hoppe/ml_rebuy_prediction/blob/main/v1.ipynb) - v1.1: FIX (Evaluation/Results) model 0 as production model

## Goals

- **Predict Customer Purchase Probability**: Determine the likelihood of a customer making a purchase in the next 90 days.
- **Enhance Marketing Efficiency**: Provide data-driven insights to personalize marketing and promotional campaigns.
- **Optimize Newsletter Campaigns**: Use prediction results to target customers more likely to make future purchases.

## Dataset

The project utilizes three main datasets:

1. **Purchase History (`apparel-purchases`)**:
   - Contains customer purchase information such as product categories, prices, purchase quantities, and the purchase dates.
   - **Key features**: 
     - `client_id`: Customer identifier.
     - `category_ids`: Nested product categories.
     - `quantity` and `price`: Purchase quantities and price details.
     - `date`: Purchase date.
  
2. **Newsletter Campaign Data (`apparel-messages`)**:
   - Contains data on newsletter campaigns sent to customers and their interactions (e.g., opened, purchased).
   - **Key features**: 
     - `bulk_campaign_id`: Campaign ID.
     - `event`: Interaction type (e.g., opened, purchased).
     - `channel`: Communication channel used.

3. **Target Variable Data (`apparel-target_binary`)**:
   - Contains the target variable indicating whether the customer made a purchase in the next 90 days (`target = 1`) or not (`target = 0`).

## Methodology

1. **Data Preparation**: 
   - Cleaned and formatted data, including date transformations and category standardization.
2. **Feature Engineering**:
   - Created and derived important features from customer purchase and newsletter interaction data.
   - Engineered new features, such as interaction frequency with newsletters, purchase recency, and average product price.
3. **Model Development**:
   - Trained several classification models including `CatBoostClassifier`, `RandomForestClassifier`, and `LogisticRegression` to predict the purchase probability.
4. **Model Evaluation**:
   - Validated the model using a custom multi-iteration stability process, which ensures that the primary model (`model_0`) is robust across different data splits.
   - Average ROC-AUC values were used to evaluate model stability and consistency.

## Implementation

### Model Training Strategy

- **Iteration-Based Validation**: 
  - Multiple iterations of training and evaluation are conducted using different train-test splits.
  - The primary model (`model_0`) is used for predictions, while additional models (`model_1`, `model_2`, `model_3`) help evaluate the stability of metrics.
  - Average ROC-AUC metrics are compared to ensure minimal variation between different iterations.

- **Hyperparameter Optimization**:
  - Utilized `RandomizedSearchCV` for hyperparameter tuning.
  - Separate configurations were used for each model to explore the best parameters within a given search space.

- **Feature Importance Analysis**:
  - Generated feature importance plots for both numerical and categorical features to understand which factors contribute most to purchase probability predictions.

### Key Features

1. **Purchase Recency (`days_max`)**: Represents the maximum number of days since a customer's last significant interaction or purchase.
2. **Mobile Push Campaign Engagement (`bulk_campaign_id_count_mobile_push`)**: Indicates how many mobile push campaigns were received by a customer, which shows significant influence on purchase likelihood.
3. **Customer Year Segment (`year_top`)**: Represents the year when the customer's interaction occurred, capturing temporal purchasing trends.

## Project Results

- The model `model_0` demonstrated stable and reliable ROC-AUC values across various splits, ensuring that the predictions are not biased due to specific data partitioning.
- Feature importance analysis revealed that recency, customer engagement with mobile push notifications, and purchase quantities are key predictors for future purchases.
- With a mean ROC-AUC of approximately `0.66`, the model provides a reasonable performance for targeting customers likely to purchase, enabling more effective marketing.
