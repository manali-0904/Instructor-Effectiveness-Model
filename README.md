# Instructor-Effectiveness-Model
An ML model related to Instructor effectiveness for an ed-tech company
# Instructor Effectiveness Modeling

## 1. Problem Understanding

The objective of this analysis is to estimate instructor effectiveness using learner outcomes, engagement metrics, and learner feedback.

The dataset contains batch-level records, where each row represents a course batch. Since an instructor can teach multiple batches and courses, the batch-level information is first aggregated to the instructor level.

An Instructor Effectiveness Score is then constructed using learning outcomes, engagement, and feedback indicators. Instructors are divided into Low, Medium, and High effectiveness tiers, and classical machine learning models are trained to predict these tiers.

The analysis focuses not only on model performance but also on feature engineering, assumptions, interpretation, limitations, and potential real-world use.
EDA Observations
-The dataset contains 2,000 batch-level records with no missing values or duplicate rows.
-Completion rate and dropout rate show a strong negative relationship, which is expected because higher learner completion generally corresponds to lower dropout.
-Score improvement, quiz performance, engagement metrics, and feedback metrics show meaningful variation across batches.
-Most variables have relatively well-behaved distributions, with only a small number of potential IQR-based outliers.
-Potential outliers were retained because they may represent genuine differences between course batches rather than data-entry errors.
-The strong relationship between completion and dropout should be considered when constructing the instructor effectiveness score to avoid giving excessive weight to closely related measures.

## Model Results and Interpretation

Two classification models were evaluated: Logistic Regression as a baseline model and Random Forest as the primary model.

Random Forest achieved an accuracy of **95.8%**, compared with **87.5%** for Logistic Regression. Random Forest also achieved higher weighted precision (96.3%), recall (95.8%), and F1 score (95.8%). This indicates that Random Forest provided better overall classification performance for the three instructor effectiveness tiers.

The confusion matrix shows that the Random Forest correctly classified all 8 Low-effectiveness and all 8 Medium-effectiveness instructors in the test set. For the High-effectiveness class, 7 out of 8 instructors were correctly classified, while one High instructor was classified as Medium. There were no Low-to-High or High-to-Low classification errors.

The stronger performance of Random Forest compared with Logistic Regression suggests that the relationship between the instructor-level metrics and effectiveness tiers may include nonlinear patterns that are better captured by a tree-based model.

### Feature Importance

The most influential feature was **average score improvement**, followed by **completion rate**, **feedback response rate**, and **dropout rate**. Average score improvement is particularly meaningful because it directly measures learner progress between assessments. Completion rate also provides an important indicator of learner success and persistence.

Feedback response rate was also relatively influential. However, this should not be interpreted as evidence that higher feedback participation directly causes better instructor performance. Feedback response may be influenced by learner engagement or other factors.

The `num_batches` feature had very low importance, suggesting that the number of batches taught contributed relatively little to the model's predictions compared with learner outcome and engagement measures.

Feature importance indicates predictive usefulness rather than causation. Therefore, these results should be interpreted as associations within this dataset rather than causal relationships.
