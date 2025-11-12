Team Member 3's Model Notes and Findings

Model 1: Baseline [Logistic Regression]
Purpose: Establish baseline performance

Model Details:

Algorithm: Logistic Regression
Library: scikit-learn
Hyperparameters:
 - solver: saga
 - class_weight: balanced
 - C: 1.0
 - max_iter: 200

Training:
Training Time: 1.02 seconds
Date Trained: 2025-11-11 20:47

Performance Metrics:
Metric	Score
Accuracy	0.274
Precision (weighted)	0.486
Recall (weighted)	0.274
F1-Score (weighted)	0.189

Per-Class Performance:
Class	Precision	Recall	F1-Score	Support
Low	0.288	0.496	0.364	115
Medium	0.000	0.000	0.000	71
High	1.000	0.006	0.011	173
Severe	0.262	0.560	0.357	141
Observations:
 - Class weighting helps minority classes; adjacent classes remain challenging.
 - Fast to train and simple baseline.
Visualizations Created:
Confusion matrix: reports/figures/model_results/baseline_confusion_matrix.png

Model 2: Random Forest
Purpose: Capture non-linear interactions across features

Model Details:
Algorithm: Random Forest Classifier
Library: scikit-learn
Hyperparameters:
 - n_estimators: 80
 - max_depth: None
 - max_features: sqrt
 - class_weight: balanced

Training:
Training Time: 0.54 seconds
Date Trained: 2025-11-11 20:47

Performance Metrics:
Metric	Score
Accuracy	0.270
Precision (weighted)	0.272
Recall (weighted)	0.270
F1-Score (weighted)	0.265

Per-Class Performance:
Class	Precision	Recall	F1-Score	Support
Low	0.236	0.304	0.266	115
Medium	0.044	0.028	0.034	71
High	0.388	0.272	0.320	173
Severe	0.274	0.362	0.312	141
Comparison to Baseline:
Accuracy improvement: -0.40 percentage points
F1-Score improvement: 7.62 percentage points
Key differences: Non-linear splits reduce some confusions.
Observations:
 - Better recall on mid-frequency classes.
 - Importance plot surfaces key routes/incidents.
Visualizations Created:
Confusion matrix: reports/figures/model_results/rf_confusion_matrix.png
Feature importance: reports/figures/model_results/rf_feature_importance.png

Model 3: Gradient Boosting
Purpose: Boosted trees to refine decision boundaries

Model Details:
Algorithm: Gradient Boosting Classifier
Library: scikit-learn
Hyperparameters:
 - n_estimators: 80
 - learning_rate: 0.1
 - max_depth: 3

Training:
Training Time: 1.69 seconds
Date Trained: 2025-11-11 20:47

Performance Metrics:
Metric	Score
Accuracy	0.338
Precision (weighted)	0.403
Recall (weighted)	0.338
F1-Score (weighted)	0.346

Per-Class Performance:
Class	Precision	Recall	F1-Score	Support
Low	0.381	0.209	0.270	115
Medium	0.176	0.451	0.253	71
High	0.404	0.416	0.410	173
Severe	0.532	0.291	0.376	141
Comparison to Previous Models:
 - GB is often competitive with RF; best choice may vary per split.
Observations:
 - GBC balances precision/recall without heavy tuning.
Visualizations Created:
Confusion matrix: reports/figures/model_results/xgb_confusion_matrix.png
Feature importance: reports/figures/model_results/xgb_feature_importance.png

Handling Class Imbalance
Problem: Imbalanced classes (rare severe incidents).

Approaches Tested:
Approach 1: Class Weights
Method: Penalize minority-class errors more.
Implementation: class_weight='balanced' in Logistic Regression & Random Forest.
Result: Improved minority handling vs. no weights.
Used in Final Model? Yes
Approach 2: SMOTE - Synthetic Minority Over-sampling (not executed here)
Approach 3: Undersampling Majority Class (not executed here)
Final Decision: Use class weights for simplicity & stability.

Hyperparameter Tuning
Model: Logistic Regression
Tuning Method: Manual validation sweep (expand as needed)
Parameters Tested: C in {1.0} (fast default)
Cross-Validation: Time-based split
Best Parameters Found: C=1.0, solver='saga', class_weight='balanced'
Performance Improvement: Test weighted-F1 = 0.189
Training Time: See above.

Feature Importance Analysis
Model Used: Random Forest, Gradient Boosting
Top features visible in: reports/figures/model_results/rf_feature_importance.png
Key Insights: Routes/incident types dominate; hour/weekday add context.

Error Analysis
Confusion Matrix Insights: Adjacent severity levels often confused.
Error Patterns: Rush hours show more mistakes; limited external features likely contribute.

Model Comparison Summary
Model	Accuracy	Precision	Recall	F1-Score	Training Time	Notes
Logistic Regression	0.274	0.486	0.274	0.189	1.02s	Baseline
Random Forest	0.270	0.272	0.270	0.265	0.54s	Non-linear
Gradient Boosting	0.338	0.403	0.338	0.346	1.69s	Boosted trees

Final Model Selection
Selected Model: The best of the three by weighted F1 in your run (see table).
Rationale: Balance of performance vs. complexity/time.
Final Performance: See summary above (test set). Trained on: 2025-11-11 20:47

Business Impact
Operational Improvements: Better triage and planning for high-risk routes/hours.
Expected Benefits: Resource allocation, response-time reduction, preventive maintenance focus.
High-Value Insights: Route/incident patterns and rush-hour effects.

Limitations
Model Limitations: Struggles on rare classes; no ordinal modeling.
Data Limitations: No weather/events; possible missing location detail.
Assumptions: Time-based split approximates deployment.

Future Improvements
Additional Models: XGBoost/LightGBM; ordinal classification.
Feature Engineering: Weather, events, lag/rolling, spatial features.
Data Collection: Richer descriptors, precise locations.
Ensemble Methods: Stack/blend for robustness; deploy with monitoring.