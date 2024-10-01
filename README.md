# GPA Predictors in the Fragile Families Challenge

This repository contains the code and methodologies used in the research paper titled "Combining Machine Learning and Social Theory to Discern GPA Predictors in the Fragile Families Challenge." The study aims to identify predictors of GPA using machine learning techniques while integrating social theory.

## Table of Contents
- [Introduction](#introduction)
- [Data Description](#data-description)
- [Methodology](#methodology)
- [Results](#results)

## Introduction
The research investigates the relationship between various factors (cognitive ability, learning environment, and socioeconomic circumstances) and GPA outcomes. The study employs both theory-driven and data-driven approaches to feature selection and model building.

## Data Description
This study is a retroactive take on the Fragile Families Challenge, using data from the Fragile Families and Child Wellbeing Study (FFCWS) (Reichman, Teitler, Garfinkel, & McLanahan, 2001). After feature selection and cleaning, the dataset used consists of 4242 households with 670 features, including constructed variables and non-constructed features reflecting cognitive ability, learning environment, and socioeconomic circumstances.

## Methodology
The analysis follows a structured pipeline:
1. **Data Preprocessing**: Cleaning and preparing the dataset.
2. **Feature Selection**: Using LASSO regression with Least Angle Regression (LARS) for efficient high-dimensional data handling.
3. **Model Building**: Implementing various models including OLS, ElasticNet, Decision Trees, Random Forests, Gradient Boosting, and LGBM.
4. **Results Interpretation**: Evaluating model performance using Mean Squared Error (MSE) and Root Mean Squared Error (RMSE) through 5-fold cross-validation.

## Results
The baseline model results for GPA prediction are as follows:

| Model          | MSE       | RMSE     |
|----------------|-----------|----------|
| OLS            | 0.516309  | 0.717608 |
| ElasticNet     | 0.406696  | 0.637363 |
| DecisionTree    | 0.831760  | 0.911480 |
| RandomForest    | 0.405152  | 0.636131 |
| Gradient Boosting| 0.424787 | 0.651276 |
| LGBM           | 0.430200  | 0.655291 |

The RandomForest model achieved the lowest MSE and RMSE, which is why I chose it as the final model to hyper-parameter tune. After tuning the following hyper-parameters: `n_estimators`, `max_features`, `max_depth` `min_samples_split` and `min_samples_leaf`, a 10-fold cross validation using the new RF model produced a RMSE of 0.376 (MSE of 0.141) presenting a 65.2% decrease in MSE. The tuned RF model’s MSE is 68.2% lower than that of the baseline model predicting mean GPA (0.443). Given that the model ranked first for predicting GPA in the FFC had an MSE of 0.377 on the holdout set (Fragile Families Challenge Team, 2016), my model’s MSE of 0.206 (imputed holdout set) and 0.365 (unimputed holdout set) suggests that it is _relatively_ reliable in predicting GPA, performing at least as well as the top-ranked model in 2016.
