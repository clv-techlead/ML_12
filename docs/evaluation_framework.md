# Evaluation Metrics Framework for Classification Models
**Purpose:** To assess the performance of a classification model, understand its strengths and weaknesses, and determine its suitability for addressing the business problem of transforming reactive streetcar incident management into proactive, data-driven operations for TTC. 

## I. Foundation: Defining the Problem & Goals
    1. Objective: predicting TTC streetcar incident types (e.g., 'Mechanical', 'MTPU', 'General Delay', 'Held By', etc.) before they occur.
    2. Business Impact: Understand the real-world consequences of correct predictions versus different types of errors:
        ◦ Value of Correct Prediction: Enables anticipation of incident types, optimization of resource allocation (maintenance crews, vehicles, personnel), improved scheduling, enhanced coordination, and ultimately, better service reliability and passenger satisfaction.
        ◦ Cost of False Positives (FP): Misclassifying an incident type (e.g., predicting 'Mechanical' when it's 'Traffic') could lead to misallocation of specialized resources or unnecessary intervention. This results in wasted resources (money, time, personnel).
        ◦ Cost of False Negatives (FN): Failing to predict an actual incident type (e.g., missing a 'Severe' delay or a critical 'Mechanical' issue) means the TTC remains reactive, leading to service disruption, prolonged delays, and negative passenger experience. This impact is critical for service reliability.
     3.  Critical Scenarios: Identify specific scenarios where model performance is paramount:
        ◦ High-Impact Incident Types: Particularly accurate prediction of major delay causes like 'Mechanical' failures, 'General Delay', 'MTPU' (presumed mechanical), and 'Held By' (external factors).
        ◦ Peak Rush Hours: Model performance during 7-9 AM and 4-6 PM on weekdays, where incidents have the highest impact on ridership and traffic.
        ◦ High-Incident Routes & Stations: Accuracy for Routes 501 Queen, 504 King, and stations like Dundas Street West and Queen Street West, which are historically prone to incidents.
        ◦ Anticipation for Proactive Response: The model's ability to provide predictions early enough to allow for proactive measures rather than reactive ones.
        
## II. Core Evaluation Metrics (Member 3)
These metrics are calculated per class and then aggregated: 
    1. Confusion Matrix: The foundational table showing True Positives (TP), True Negatives (TN), False Positives (FP), and False Negatives (FN) for each class.
        ◦ Value: Provides a raw count of correct and incorrect predictions, offering the most granular view of model errors. 
    2. Accuracy: (TP + TN) / (TP + TN + FP + FN)
        ◦ Value: Easy to understand. Measures overall correctness.
        ◦ Caveat: Misleading with class imbalance. A model predicting the majority class can have high accuracy but be useless.
    3. Precision (Positive Predictive Value): TP / (TP + FP)
        ◦ Value: Measures how many of the positive predictions were actually correct. Important when minimizing false alarms is critical (e.g., if a false 'Severe' delay prediction triggers expensive interventions).
    4. Recall (Sensitivity, True Positive Rate): TP / (TP + FN)
        ◦ Value: Measures how many of the actual positive cases were correctly identified. Important when minimizing missed positive cases is critical (e.g., failing to predict an actual 'Severe' delay).
    5. F1-Score: 2 * (Precision * Recall) / (Precision + Recall)
        ◦ Value: The harmonic mean of precision and recall. Useful for balancing both concerns, especially with imbalanced classes.
    6. Specificity (True Negative Rate): TN / (TN + FP)
        ◦ Value: Measures how many of the actual negative cases were correctly identified.
    7. Log-Loss (Cross-Entropy Loss): Measures the performance of a classification model where the prediction is a probability. It penalizes confident incorrect predictions more heavily.
        ◦ Value: Excellent for models that output probabilities, as it assesses the calibration of those probabilities. A lower score is better.
        
    ### Visual Representation of Metrics 
      - **Confusion Matrix Heatmap** - Shows misclassification patterns at a glance 
      - **Per-Class Metrics Bar Chart** - Compare precision/recall/F1 across incident types 
      - **ROC Curves** (if applicable) - For models outputting probabilities 
      - **Precision-Recall Curves** - Especially valuable with class imbalance 
      
## III. Multi-Class Aggregation Strategies (Member 3)
For delay_bin with 'Low', 'Medium', 'High', 'Severe' categories, you need to aggregate per-class metrics:
    1. Macro Average: Calculate the metric independently for each class, then take the unweighted average. Treats all classes equally, regardless of their support.
    2. Weighted Average: Calculate the metric independently for each class, then take the average weighted by the support (number of true instances) for each class. Reflects the contribution of each class.
    3. Micro Average: Calculate metrics globally by counting the total true positives, false negatives, and false positives. More influenced by majority classes.
        ◦ Recommendation: Start with per-class metrics to see performance on each delay type, then use weighted average for an overall summary that reflects class distribution, and macro average to ensure minority classes aren't completely ignored.

### Special Consideration: Class Imbalance

Given the expected class imbalance in incident types:

**Metrics to prioritize:**
- **Macro Average F1-Score** - Ensures minority classes aren't ignored
- **Per-Class Recall** - Especially for rare but critical incident types
- **Balanced Accuracy** - Alternative to standard accuracy for imbalanced data

**Metrics to de-emphasize:**
- **Overall Accuracy** - Can be misleading with severe imbalance
- **Micro Average** - Dominated by majority class

## IV. Contextual Evaluation & Interpretation (Member 3)
    1. Threshold-Specific Analysis: For models outputting probabilities (e.g., probability of a 'Severe' delay), evaluate metrics at different classification thresholds. This is particularly relevant for balancing precision and recall based on the business costs associated with false positives (e.g., unnecessary resource dispatch) versus false negatives (e.g., missed opportunity for proactive intervention).
    2. Performance in Critical Scenarios: Evaluate all core metrics specifically on subsets of your data, as identified in your problem statement and EDA:
        ◦ High-Impact Incident Types: Focus on metrics for 'Mechanical' failures, 'General Delay', 'MTPU', and 'Held By'. How well does the model predict these categories, which are critical for resource allocation and service reliability?
        ◦ Peak Rush Hours: Filter data for 7-9 AM and 4-6 PM on weekdays. Assess model performance during these periods where incidents have the highest impact on ridership and traffic.
        ◦ High-Incident Routes & Stations: Evaluate accuracy and other metrics for specific routes (501 Queen, 504 King) and stations (Dundas Street West, Queen Street West), which are historically prone to incidents.
        ◦ Proactive Response Time: Consider if the model's predictions are available early enough to allow for proactive measures. While not a direct metric, the timing of predictions influences the utility of the accuracy.
    3. Error Analysis: Beyond quantitative metrics, perform a qualitative analysis of misclassified instances:
        ◦ What common characteristics do False Positives or False Negatives for critical incident types (e.g., 'Mechanical', 'Severe' delays) share?
        ◦ Are there specific times, locations, or external factors (e.g., extreme weather) where the model consistently struggles, indicating areas for future feature engineering or data collection? 
    4. Feature Importance: Analyze which features the model relies on most for its predictions. This helps validate the insights from your EDA (e.g., if 'hour' and 'route' features are highly important) and can provide further actionable insights.
    
## V. Framework for Reporting & Decision Making (Member 4)
    1. Dashboards/Visualizations: Create clear visualizations of the confusion matrix, ROC curves, and per-class metrics. Specifically highlight performance in critical scenarios (e.g., peak rush hours, high-incident routes).
    2. Comparison to Baselines: Always compare your model's performance against a simple baseline (e.g., predicting the most frequent incident type, or a rule-based system) to demonstrate the value added by the ML model.
    3. Trade-off Discussion: Present the trade-offs between precision and recall for different incident types. Discuss how these trade-offs align with the TTC's operational priorities (e.g., is it more critical to detect all mechanical failures even with some false alarms, or to have very few false alarms for 'Held By' incidents?).
    4. Actionable Recommendations: Translate evaluation findings into concrete, actionable suggestions for operational improvements. For instance:
        ◦ "Model predicts increased 'Mechanical' incidents on Route 501 during 7-9 AM, suggesting targeted pre-rush hour vehicle checks on this line."
        ◦ "High recall for 'Held By' incidents during evening rush hour indicates model's utility for proactive traffic management coordination."
    5. Long-Term Monitoring: Establish a plan for continuous monitoring of the model's performance in real-world deployment to detect drift and ensure sustained utility.
    6. Quick Reference: Translating Metrics to Business Language

| Technical Metric | Business Translation |
|------------------|---------------------|
| **80% Accuracy** | "Model correctly identifies 4 out of 5 incidents" |
| **High Precision (0.85) for 'Mechanical'** | "When model predicts mechanical issue, it's right 85% of the time - reduces unnecessary mechanic dispatches" |
| **High Recall (0.90) for 'General Delay'** | "Model catches 90% of general delays - allows proactive passenger communication" |
| **Low Recall (0.50) for 'Security'** | "Model misses half of security incidents - still need manual monitoring for these" |
| **F1-Score improved from 0.62 to 0.81** | "Model performance improved by 30%, translating to ~20% reduction in incident response time" |
| **Confusion: 'Mechanical' vs 'MTPU'** | "Model sometimes confuses mechanical failures with mechanical-related delays - both require maintenance crews, so impact is minimal" |
 
## VI. Implementation Checklist

**Phase 1: Basic Evaluation**
- [ ] Create confusion matrix for each model
- [ ] Calculate accuracy, precision, recall, F1 for each model
- [ ] Calculate both macro and weighted averages
- [ ] Create per-class performance table
- [ ] Save results to `reports/model_comparison.csv`
- [ ] Create confusion matrix visualizations (save to `reports/figures/model_results/`)

**Phase 2: Contextual Evaluation**
- [ ] Evaluate performance on peak rush hours subset
- [ ] Evaluate performance on high-incident routes subset
- [ ] Compare critical scenario performance to overall performance
- [ ] Document performance gaps in `docs/member3_model_notes.md`

**Phase 3: Deep Analysis**
- [ ] Analyze feature importance for final model
- [ ] Create feature importance visualization
- [ ] Perform error analysis (what's being misclassified?)
- [ ] Identify patterns in misclassifications
- [ ] Document findings for Member 4


**Phase 4: Business Translation**
- [ ] Write business impact summary in plain language
- [ ] Provide actionable recommendations based on findings
- [ ] Highlight model strengths for README
- [ ] Document limitations transparently
- [ ] Suggest future improvements

**Phase 5: Deliverables for Member 4**
- [ ] Complete `docs/member3_model_notes.md` with all findings
- [ ] Provide 3-5 key visualizations for README/presentation
- [ ] Write 1-paragraph performance summary in business language
- [ ] List top 3 actionable recommendations
- [ ] Flag any critical limitations

This framework ensures a holistic and purpose-driven approach to evaluating your classification model, moving beyond just raw numbers to derive meaningful insights.
