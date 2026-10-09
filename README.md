# ACTG175CD4Regression: Predicting Immune Response in HIV Patients (ACTG 175 Clinical Trial)

This project focuses on developing, evaluating, and interpreting machine learning regression models to predict the immune response of patients with HIV infection. The objective is to predict the CD4 cell count after 20 weeks of antiretroviral therapy, using `cd420` as the target variable.

## Dataset

The analysis uses data from the randomized ACTG 175 (AIDS Clinical Trials Group Study 175) clinical trial, which includes 2,139 adult patients.
The dataset contains 25 features, including demographic information, medical history, laboratory measurements, and treatment-related variables.

## Preprocessing and Methodology

To prevent data leakage and ensure reproducibility, a comprehensive preprocessing pipeline was developed.

*   **Standardization:** `StandardScaler` was applied to continuous variables, such as age, weight, and baseline cell counts.
*   **Encoding:** `OneHotEncoder` with `drop='first'` was used for categorical variables with more than two categories, such as treatment type (`trt`), to reduce multicollinearity.
*   **Feature Selection:** Recursive Feature Elimination (RFE) was applied to reduce dimensionality. The top 10 features were strategically selected, improving Mean Absolute Error (MAE) and model interpretability as measured by R².

## Modeling and Evaluation

Five baseline regression algorithms were evaluated using 5-fold cross-validation:

1. Linear Regression
2. Gradient Boosting Regressor
3. Random Forest Regressor
4. K-Nearest Neighbors (KNN)
5. Support Vector Regression (SVR)

Following the initial evaluation, Grid Search was performed to optimize the hyperparameters of the tree-based ensemble models.

## Best-Performing Model

Gradient Boosting emerged as the best-performing model, achieving an MAE of **84.19** with the following hyperparameters:

*   `learning_rate`: 0.05
*   `max_depth`: 3
*   `n_estimators`: 100
*   `subsample`: 0.8

The model successfully captured non-linear relationships and interactions within the data.

## Explainable AI (XAI) with SHAP

To improve the transparency and interpretability of the Gradient Boosting model, particularly in the context of potential clinical applications, SHAP (SHapley Additive exPlanations) was used to explain its predictions.

### Key Predictive Factors

*   **Most Important Predictor:** The baseline CD4 cell count (`cd40`) emerged as the most influential feature in predicting CD4 levels after 20 weeks.
*   **Positive Influence:** Initiation of a new treatment regimen (`bin_treat`, `cat_trt_1`) was associated with higher predicted CD4 counts.
*   **Negative Influence:** A history of previous treatments (`bin_str2`) and high baseline CD8 levels were associated with lower predicted values.

## Conclusion

This project demonstrates the potential of combining powerful predictive algorithms, such as Gradient Boosting, with modern Explainable AI techniques like SHAP to improve model transparency and support the interpretation of clinical data.

The findings highlight the importance of baseline CD4 counts and treatment-related factors in predicting immune response. However, these results should be interpreted as predictive associations rather than evidence of causation, and the model requires further clinical validation before being used to support clinical decisions.
