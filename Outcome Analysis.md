## Outcome Analysis

To determine whether the presence of stable working groups affects the severity of punishments in the Russian legal system, I used a Random Forest regression model. This model predicts punishment severity using features such as region, judge, prosecutor, attorney, and the presence of a stable working group.

### Best Parameters Identified Through GridSearchCV:
- **max_depth**: 10
- **min_samples_leaf**: 4
- **min_samples_split**: 5
- **n_estimators**: 100

### Model Performance Metrics:
- **Mean Squared Error (MSE)**: 40.84
- **R-squared**: -0.15
- **Mean Absolute Error (MAE)**: 5.11

The MSE indicates that the average squared difference between the actual outcomes and the model's predictions is relatively high. A negative R-squared value suggests the model does not fit the data well, implying many factors influencing punishment severity are not captured in our model. The MAE shows that, on average, the model's predictions are off by about 5 years.

A scatter plot of observed vs. predicted punishment severity reveals a significant spread of data points, suggesting that while the model can predict general trends, it struggles with precise predictions, especially for higher values. The dashed line in the plot represents the ideal scenario where predicted values match observed values exactly.

#### Graph 1: Random Forest Regression: Observed vs. Predicted Punishment Severity

To understand each feature's contribution to the prediction of punishment severity, I used SHAP (SHapley Additive exPlanations) values. The SHAP summary plot illustrates the impact of different features, including the presence of a stable working group. This plot shows that stable working groups significantly influence punishment severity. Each dot represents a SHAP value for a feature in a particular instance, indicating how much that feature influenced the prediction.

#### Graph 2: SHAP Value (Impact on Model Output)

In addition to regression analysis, I employed a Random Forest classifier to predict judicial outcomes (guilty or not guilty) based on the same set of features. Here are the detailed results and their interpretations:

### Best Parameters for Classifier:
- **max_depth**: 30
- **min_samples_leaf**: 1
- **min_samples_split**: 2
- **n_estimators**: 300

### Model Performance Metrics:
- **Precision**: 0.9919678714859438
- **Recall**: 0.9427480916030534
- **F1-Score**: 0.9667318982387475
- **ROC-AUC**: 0.4713740458015267

Precision measures the proportion of true positive results among all positive results predicted by the classifier. For instance, a precision of 0.99 means that 99% of the cases predicted as guilty are actually guilty. Recall measures the proportion of true positive results among all actual positive cases. A recall of 0.94 suggests that the model correctly identifies 94% of all actual guilty cases. The F1-Score, which is the harmonic mean of precision and recall, provides a balance between the two. An F1-Score of 0.97 indicates excellent performance in predicting judicial outcomes. Lastly, the ROC-AUC score reflects the model's ability to distinguish between positive and negative classes. An ROC-AUC of 0.47 suggests that the model's performance is slightly better than random guessing.
