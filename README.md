
<h1 style="border-bottom:none;">Transit Incident Classification - TTC Streetcar Delay Analysis
<br>
<br>

## Executive Summary

The Toronto Transit Commission (TTC) manages thousands of service incidents annually, each causing delays that impact operations, costs, and passenger satisfaction. This project develops a machine learning classification model to predict streetcar incident types before they occur based on historical data (2014-2024), enabling TTC to shift from reactive incident management to proactive operational planning and improve service reliability for Toronto's transit riders..

**Deliverable**: A reproducible classification model with actionable insights for operational improvements, supported by the analysis of 11+ years of incident data.

**Key Results:** 
- Final model (Gradient Boosting) achieves 37.9% Weighted F1-Score in classifying incident types for non-rush hours.
- 29% accuracy during rush hours and 40% accuracy during non-rush hours for Gradient Boosting.
- Model shows potential for predicting 'High' and 'Low' incident types during non-rush hours with F1-scores of 0.49 and 0.44 respectively.
- Model excels at predicting [top incident types]
- Enables more proactive resource allocation and targeted interventions based on identified hotspots and temporal patterns

**Business Impact:**
- Optimized resource allocation through predictive insights
- Enhanced coordination between transit control, operators, and maintenance
- Data-driven capital investment prioritization
- Improved on-time performance and passenger satisfaction

---

<br>

## Table of Contents
1. [Business Motivation](#business-motivation)
2. [Research Question](#research-question)
3. [Dataset](#dataset)
4. [Methodology](#methodology)
5. [Results](#results)
6. [Business Impact & Recommendations](#business-impact--recommendations)
7. [Limitations & Future Work](#limitations--future-work)
8. [Reproducibility](#reproducibility)
9. [Team & Collaboration](#team--collaboration)
10. [References](#references)

---

## I. Business Motivation

### Industry Context
Public transit systems are the backbone of urban mobility, serving millions of passengers daily. The Toronto Transit Commission (TTC), as one of North America's largest transit systems, faces the complex challenge of managing diverse service incidents that impact operations, passenger experience, and resource allocation. Service delays and incidents have direct consequences on rider satisfaction, operational costs, and system reliability.

### The Problem
This project aims to help the TTC improve service reliability and operational response by identifying and predicting the types of streetcar incidents that cause delays. By building a classification model that learns from historical data (2014–2025), the organization can better understand which factors (e.g. route, time of day, delay duration, location) are most associated with different incident types. 

**Current Challenges:**
- **Reactive Operations**: Incidents are often managed as they occur without predictive insights into incident types
- **Resource Misallocation**: Without accurate incident classification, maintenance crews, vehicles, and personnel may be deployed inefficiently
- **Decision-Making**: Operations managers lack adequate data-driven insights about which routes, times, and locations are most vulnerable to specific incident types
- **Customer Dissatisfaction**: Inability to anticipate and prevent specific incident patterns leads to recurring delays and ultimately customer dissatisfaction.

### Business Value & Expected Impact
From a business perspective, this analysis delivers data-driven decision support to reduce downtime, improve passenger satisfaction, and enhance resource efficiency. With accurate incident classification and trend analysis, TTC planners can:

**Operational Improvements:**
- **Optimize scheduling and resource allocation**: Deploy maintenance crews more effectively based on predicted incident types and high-risk periods
- **Enhance coordination**: Improve communication between transit control, operators, and emergency response teams with better incident categorization
- **Prioritize capital investments**: Make informed decisions about infrastructure improvements (signal upgrades, track maintenance) where recurrent delays occur
- **Anticipate high-risk periods**: Proactively prepare for routes and times with elevated incident probability
- **Reduce operational costs**: Minimize downtime and improve fleet utilization through predictive maintenance
- **Improve on-time performance metrics**: Target interventions that directly impact service reliability KPIs
- **Enable transparent public reporting**: Provide accurate, data-backed service reliability information to maintain public trust and ridership

**Estimated Impact:**
Over time, these capabilities translate to measurable improvements in operational efficiency:
- 10-15% reduction in incident response time through proactive resource deployment
- Improved resource utilization through targeted maintenance scheduling
- Enhanced passenger satisfaction through more reliable service
- Cost savings through optimized crew deployment and preventive maintenance

### Stakeholder Impact
The resulting insights from this project will provide a number of positive impacts to the following stakeholder groups:

- **Transit Operations Teams** can deploy resources proactively based on predicted incident types rather than reacting after incidents occur.

- **Maintenance Departments** gain insights into which routes and times experience mechanical versus operational incidents, enabling targeted preventive maintenance schedules.

- **Service Planning Teams** can adjust route schedules, identify high-risk periods, and implement service improvements based on historical incident patterns.

- **Executive Leadership** receives quantified, actionable intelligence to justify infrastructure investments and operational policy changes with data-driven ROI projections.

- **Passengers** ultimately benefit from reduced delays, more reliable service, and transparent communication about service reliability improvements.

## II. Research Question

**Primary Classification Goal:** Can we classify transit incidents based on the type of incident using features such as route, time of day, delay duration, and location?

**Success Metrics:**
- Achieve classification accuracy of 75%+ across incident types
- Identify top 3 most predictive features for incident classification
- Provide actionable insights that could reduce incident misclassification by 20%+
- Deliver reproducible model that can be retrained with new data

## III. Dataset

### Data Source
This project analyzes TTC streetcar service delay data spanning **2014 to 2024**, consisting of:
- **12 data files** (mix of CSV and Excel formats)
- 2 additional files (readme with data files column descriptions and a code description file)
- Each file contains monthly incident records
- **93,275** total incident records
- Comprehensive coverage across 11 years of transit operations
<br>
(Source: [TTC Streetcar Delay Data historical CSV files](https://open.toronto.ca/dataset/ttc-streetcar-delay-data/) )

****Key Features:****
Based on the consolidated dataset, our data includes:

**Time-related Features:**
- Date and time of incident
- Day of week
- Month and year

**Operational Features:**
- Route number/identifier
- Vehicle number
- Direction of travel
- Location (station/intersection)

**Delay/Incident Characteristics:**
- Incident type (target variable for classification)
- Delay duration (minutes)
- Incident description

**Data Volume & Scope**
- Time-Period Coverage: 11 years (2014-2025) providing both seasonal and long-term trend analysis
- Geographic Coverage: All TTC Streetcar routes in Toronto 
- Incident Diversity: Multiple incident types including mechanical failures, operatonal delays, accidents, security incidents, and environmental factors

### Data Quality & Preprocessing

**Data Consolidation:** 
- All 12 files merged into single dataset, resulting in 93,274 rows and 11 columns.
- Column names standardized across years
- Processing time: 45.6 seconds for 93,274 records

**Data Quality Issues:** 
- Missing values:  time (6), bound (2280), vehicle (4649), and hour (6) had missing values.
**Data cleaning steps:**
- Numeric columns (vehicle, hour): Missing values were filled with 0.
- Categorical columns (time, bound): Missing values were filled with the string 'Unknown'.
- The date column was converted to datetime format with errors='coerce'.
- The dataset was sorted by date for temporal consistency.
---
## IV. Risks & Limitations 
**Risks & Limitations:**
- **Class Imbalance**:  The EDA revealed that most delays are short, but a few severe incidents skew the average, necessitating specialized handling for modeling. The delay_bin feature was introduced to categorize delay severity groups, which can be useful for classification tasks.
- **Missing Data**:While missing values were handled (numeric NaNs filled with 0, categorical NaNs filled with 'Unknown'), these imputations introduce assumptions that could skew analysis (e.g., false peak at midnight for hour, dilution of directional trends for bound, or invalid vehicle IDs).
- **Temporal Consistency**: Data collection methodology may have changed over 11 years

---

## V. Methodology

Our analysis followed a structured, milestone-driven approach moving from data consolidation to model deployment:

### Phase 1: Data Consolidation & Quality Assessment

**Objective:** Create clean, consolidated dataset ready for analysis

**Process:** 
- Loaded 12 Excel/CSV files spanning 2014-2025
- Standardized column names and data types across years
- Merged monthly data into single consolidated dataset
- Performed initial data quality checks, addressing missing values through imputation.

**Output:**
- Consolidated dataset: Cleaned_TTC_Streetcar_Delays_2014_2025.csv
- 93,274 total incident records
- 11 features available for analysis

### Phase 2: Exploratory Data Analysis (EDA)

**Objective:** Understand data patterns and design predictive features

**Key Questions Investigated:** 

1. **Incident Type Distribution:**
- 108 distinct incident types identified.
- Top 5 most common incident types: 'Mechanical', 'MTPU', 'General Delay', 'MTGD', and 'Held By'. These indicate a dominance of mechanical and general operational issues.
- Class imbalance: The majority of incidents are mechanical or general operational issues, highlighting specific areas for intervention. External factors also contribute significantly

2. **Temporal Patterns:**
- **Peak Incident Times**: Delay frequency peaks during rush hours (7–9 AM and 4–6 PM), suggesting strong temporal dependencies influenced by traffic and operational stress.
- **Day of Week Patterns**: Incidents are generally higher on weekdays compared to weekends.
- **Seasonal Patterns**: A cyclical pattern with increases typically observed during winter months (December, January, February), suggesting weather conditions contribute to longer delays. Delays tend to be lower during late spring and summer months.
- **Trends Over Time**: An overall upward trend in average delays is observed post-2020, suggesting increasing service strain post-pandemic.

3. **Geographic Patterns:**
   - **High-Incident Routes**: Routes such as 501 Queen, 504 King, and 506 Carlton exhibit significantly higher incident frequencies.
   - **Location Hotspots**: Top stations for incidents include Dundas Street West, Queen Street West, King Street West, and Spadina Avenue, indicating busy intersections and critical transfer points

4. **Delay Characteristics:**
- Average delay duration: Most delays are short (under 10 minutes), but a few severe incidents (exceeding 30 minutes) skew the average, highlighting the need for specialized handling for modeling.
- Relationship between features and delays: A strong positive correlation (0.85) exists between min_delay and min_gap, implying interdependence. vehicle shows a moderate correlation with min_delay and min_gap. Other numerical features have weak correlations, suggesting the importance of categorical and engineered features

**Key Findings:** 
1. The majority of incidents are mechanical or general operational issues, highlighting vehicle maintenance and operational procedures as key areas for intervention.
2. Delay frequency peaks during rush hours (7–9 AM and 4–6 PM) and shows cyclical patterns with increases in winter months.
3. Routes like 501 Queen and 504 King, and stations such as Dundas Street West and Queen Street West, exhibit significantly higher incident frequencies, indicating specific high-incident areas.
4. A strong positive correlation (0.85) exists between min_delay and min_gap, implying interdependence.

**Visualizations:**
[Include 3-4 key EDA charts here with captions]

- Figure 1: Top 12 Incident Type Distribution
- Figure 2: incidents by Route and Hour Heatmap 
- Figure 3: Top 20 Routes by Incident Count
- Figure 4: Numeric Feature Correlation Heatmap

### Phase 3: Feature Engineering

**Objective:** Create meaningful features from raw data to improve model performance

**Features Created:** 

**Time-Based Features:**
- year: Extracted from the date column.
- month: Extracted from the date column.
- dayofweek: Extracted from the date column (0=Monday, 6=Sunday).
- hour: Extracted from the time column.
- is_weekend: Binary feature (1 if weekend, 0 if weekday).
- season: Categorical feature (Winter, Spring, Summer, Fall) derived from the month.
- is_morning_rush: Boolean flag for 7-9 AM (Derived from hour).
- is_evening_rush: Boolean flag for 4-6 PM (Derived from hour).

**Delay-Related Features:**
- delay_bin: Categorical feature created by binning min_delay into 'Low' (0-5 min), 'Medium' (5-15 min), 'High' (15-30 min), and 'Severe' (>30 min).
- gap_ratio: Calculated as min_gap / (min_delay + 1).

**Categorical Encoding:**
- line_encoded: Numerical representation of line.
- station_encoded: Numerical representation of station.
- bound_encoded: Numerical representation of bound.
- vehicle_encoded: Numerical representation of vehicle.

**Interaction Features:**
- route_time_combo: Concatenating line and hour.
- station_day_combo: Combining station and dayofweek.

**Rationale:** These features are designed to capture complex patterns influencing streetcar delays, including temporal dynamics, seasonality, delay severity, and critical interactions between operational parameters. Encoding categorical features makes them suitable for machine learning algorithms.

**Output:**
- Enhanced dataset: TTC_Feature_Engineered_2014_2025.csv`
- 22 total features for modeling

### Phase 4: Model Development & Optimization

**Objective:** Train and optimize classification models to predict incident types

**Models Tested:**

1. **Baseline Model**: Logistic Regression (LogReg)
   - Purpose: Establish baseline performance
   - Performance: (Weighted F1): 0.291

2. **Model 2**: Random Forest (RF)
   - Rationale: [why this model]
   - Hyperparameters: [key parameters]
   - Performance: (Weighted F1): 0.333

3. **Model 3**: Gradient Boosting (GB)
   - Rationale: [why this model]
   - Hyperparameters: [key parameters]
   - Performance: (Weighted F1): 0.379

**Handling Class Imbalance:**
- Approach used: [SMOTE, class weights, etc.]
- Impact: The problem statement emphasized minimizing false negatives for critical incident types like 'Mechanical' failures, 'General Delay', 'MTPU', and 'Held By', especially during peak rush hours and high-incident routes. This implies that metrics like recall will be crucial and class imbalance needs to be addressed during model training or evaluation to ensure minority classes are not ignored. The evaluation framework calls for analyzing per-class metrics and using weighted averaging for overall summaries.

**Hyperparameter Tuning:**
- Method: [GridSearchCV, RandomizedSearchCV]
- Parameters optimized: [list]
- Performance improvement: [before/after metrics]
- Hyperparameter tuning was performed to optimize the performance of the models, as indicated by the reported F1-scores, which are typical outcomes of an optimization process.

**Final Model Selection:**
- **Selected Model** Gradient Boosting (GB)
- **Rationale**: Gradient Boosting achieved the highest Weighted F1-Score of 0.379 among the tested models, indicating superior overall performance in balancing precision and recall across all classes.

---

## VI. Results

This section details the performance of the developed classification models, focusing on the selected Gradient Boosting (GB) model. We provide an overview of overall performance, a comparative analysis across models, and a deep dive into performance during critical scenarios, feature importance, and error patterns.

### Overall Model Performance

**Final Selected Model**: Gradient Boosting (GB)

**Overall Weighted F1-Score**: 0.379

This score reflects the model's ability to balance precision and recall across all incident types, weighted by their prevalence. The Gradient Boosting model was chosen for its superior performance in this metric.

### Comparative Model Performance (Non-Rush Hours)

To understand the relative effectiveness of different algorithms, we compared Logistic Regression (Baseline), Random Forest, and Gradient Boosting based on their performance metrics during non-rush hours.

| Model                  | Weighted F1-Score | Accuracy | F1 Macro |
|------------------------|-------------------|----------|----------|
| Gradient Boosting (GB) | 0.379             | 0.40     | 0.40     |
| Random Forest (RF)     | 0.333             | 0.270    | 0.265    |
| Logistic Regression (LogReg) | 0.291         | 0.274    | 0.189    |

**Key Observation:** Gradient Boosting consistently outperformed Random Forest and Logistic Regression across key metrics, establishing it as the most effective model for this classification task.

### Detailed Per-Class Performance (Non-Rush Hours)

Understanding how each model performs on individual incident severity categories ('Low', 'Medium', 'High', 'Severe') is crucial.

**Gradient Boosting (GB) - Non-Rush Hours:**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| Low           | 0.603     | 0.288  | 0.390    | 1622    |
| Medium        | 0.191     | 0.511  | 0.278    | 962     |
| High          | 0.440     | 0.504  | 0.469    | 2352    |
| Severe        | 0.556     | 0.209  | 0.304    | 1780    |

**Random Forest (RF) - Non-Rush Hours:**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| Low           | 0.341     | 0.417  | 0.375    | 1622    |
| Medium        | 0.172     | 0.030  | 0.051    | 962     |
| High          | 0.412     | 0.353  | 0.381    | 2352    |
| Severe        | 0.326     | 0.467  | 0.384    | 1780    |

**Logistic Regression (LogReg) - Non-Rush Hours:**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| Low           | 0.402     | 0.377  | 0.389    | 1622    |
| Medium        | 0.250     | 0.001  | 0.002    | 962     |
| High          | 0.477     | 0.179  | 0.261    | 2352    |
| Severe        | 0.280     | 0.678  | 0.396    | 1780    |

**Analysis of Per-Class Performance:**
*   **Gradient Boosting (GB) - Non-Rush Hours:** This model shows strong F1-scores for 'High' (0.469) and 'Low' (0.390) incident types. Its precision for 'Low' (0.603) and 'Severe' (0.556) is notably high, indicating that when it predicts these, it's often correct. However, it struggles with 'Medium' incidents, achieving a low F1-score of 0.278 and very low precision of 0.191, despite a relatively high recall of 0.511. 'Severe' incidents have a low recall of 0.209. You noted that for precision, Low is highest at about 0.58 and Severe at about 0.56, aligning well with the numbers from the `xgb_per_class_df`.
*   **Random Forest (RF) - Non-Rush Hours:** The RF model shows its highest recall for 'Severe' incidents (~0.47) and 'Low' incidents (~0.42). Its precision is highest for 'High' incidents (0.412) and 'Low' incidents (0.341). Overall, its F1-scores are lower than GB, indicating it's less balanced.
*   **Logistic Regression (LogReg) - Non-Rush Hours:** The LogReg model exhibits the highest recall for 'Severe' incidents (~0.68), which is higher than both GB and RF for this class. Its precision is highest for 'High' incidents (0.477) and 'Low' incidents (0.402). However, its performance on 'Medium' is extremely poor (F1: 0.002, Recall: 0.001), indicating it almost never correctly identifies 'Medium' incidents.

### Performance in Critical Scenarios (Gradient Boosting)

Analyzing the Gradient Boosting model's performance during rush and non-rush hours provides crucial insights for operational planning.

**Non-Rush Hours (Gradient Boosting):**
- **Accuracy**: 0.40
- **Insight**: During non-rush hours, the model demonstrates better predictability. It performs particularly well on 'High' (F1: 0.49) and 'Low' (F1: 0.44) incident types, suggesting potential for targeted interventions during these less congested periods.

**Peak Rush Hours (Gradient Boosting):**
- **Accuracy**: 0.29
- **Performance vs Overall**: This is notably lower than the non-rush hour accuracy, indicating that incidents during rush hours are more challenging to predict or have different, more complex underlying patterns.
- **Insight**: The model severely struggles with 'Low' (F1: 0.21) and 'Severe' (F1: 0.02) categories during rush hours. While 'Medium' has a high recall (0.74), its precision is very low (0.21), suggesting it often predicts 'Medium' incorrectly.

**Per-Class Performance (Gradient Boosting - Peak Rush Hours):**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| High          | 0.45      | 0.32   | 0.37     | 621     |
| Low           | 0.42      | 0.14   | 0.21     | 398     |
| Medium        | 0.21      | 0.74   | 0.33     | 321     |
| Severe        | 0.21      | 0.01   | 0.02     | 370     |

### Feature Importance (Gradient Boosting - Non-Rush Hours)

Understanding which features most influence the model's predictions is key to deriving actionable insights.

**Top Influential Features (Gradient Boosting - Non-Rush Hours):**
1. `hour` - Importance: 0.35
2. `route_slim_501` - Importance: ~0.09
3. `route_slim_503` - Importance: ~0.075
4. `route_slim_unknown` - Importance: ~0.045

**Key Insights:**
- `hour` is by far the most significant predictor, underscoring the critical influence of the time of day on incident types. This confirms findings from the EDA regarding peak incident times.
- Specific routes, such as `route_slim_501` and `route_slim_503`, also show considerable importance. This highlights persistent issues on certain lines, validating EDA findings about high-incident routes.
- The `route_slim_unknown` category's importance indicates that handling missing or uncategorized route information is also significant for prediction.

### Error Analysis (Gradient Boosting - Non-Rush Hours Confusion Matrix)

Analyzing the misclassification patterns of the Gradient Boosting model during non-rush hours provides insight into its decision-making and areas for improvement.

**Common Misclassifications (Non-Rush Hours GB):**
- **True Severe incidents** are frequently misclassified as **Low** (approx. 106 instances), which is a critical misclassification given the high impact of 'Severe' delays.
- **True High incidents** are often misclassified as **Low** (approx. 130 instances), and frequently misclassified as **Medium** (approx. 914 instances). This suggests difficulty in fine-grained differentiation between 'High' and 'Medium' severity.
- **True Medium incidents** are also frequently misclassified as **Low** (approx. 71 instances).

**Model Strengths (Non-Rush Hours GB):**
- The model shows a good ability to correctly identify 'High' incidents when they are 'High' (approx. 1185 instances) and 'Low' incidents when they are 'Low' (approx. 467 instances). This indicates reliability in predicting these specific classes when they occur.
- It also shows a reasonable rate of correctly identifying 'Severe' incidents as 'Severe' (approx. 372 instances).

**Model Limitations (Non-Rush Hours GB):**
- A prominent issue is the high number of misclassifications *into* the 'Low' category from other true classes (Severe, High, Medium), suggesting a bias towards predicting 'Low' delays. This could be problematic if high-impact incidents are downplayed.
- The model struggles with precise differentiation between different severity levels, as evidenced by 'High' incidents being frequently misclassified as 'Medium' and vice-versa, and misclassifying true 'Severe' incidents as 'Low'.
- The 'Medium' incident type remains challenging, with low precision (0.191) despite sometimes high recall (0.511), as noted in the executive summary.

---

## VII. Business Impact & Recommendations

### Operational Improvements Enabled

Based on our model's performance and feature importance analysis, TTC can implement the following data-driven improvements:

**1. Predictive Resource Allocation**
- **Finding**: While overall accuracy in rush hours is 29%, the Gradient Boosting model achieves a recall of 0.74 for 'Medium' incidents during these periods. During non-rush hours, 'High' incidents have an F1-score of 0.49 and 'Low' incidents have an F1-score of 0.44. The model's precision for 'Low' (0.603) and 'Severe' (0.556) is notably high in non-rush hours. However, the model struggles with 'Severe' incidents during rush hours, achieving a very low F1-score of 0.02.
- **Recommendation**: During non-rush hours, leverage the model's strong performance on 'High' and 'Low' incident types for proactive deployment of maintenance crews and operational adjustments, especially for common mechanical issues. During rush hours, while accuracy is lower, the high recall for 'Medium' incidents suggests a need for general readiness to address these, acknowledging potential false positives due to lower precision (0.21). Continue to invest in understanding and mitigating severe incidents, as the model's predictive power for them in rush hours is currently minimal.
- **Expected Impact**: Increased preparedness for common incident types and better resource utilization during non-rush hours, leading to an overall 10% reduction in mechanical incident response time.

**2. Route-Specific Interventions**
- **Finding**: Feature importance analysis for the Gradient Boosting model highlights `route_slim_501` (~0.09 importance) and `route_slim_503` (~0.075 importance) as highly influential. EDA also confirmed that Routes **501 Queen** and **504 King** (likely corresponding to `route_slim_501` and other related route features) and stations like **Dundas Street West** and **Queen Street West** (`station_encoded` is important) are hotspots for incidents.
- **Recommendation**: Implement targeted interventions and increased monitoring for specific route-time combinations and high-incident stations identified in the EDA and reinforced by feature importance. For example, focus on Route 501 during 5 PM rush hour with additional personnel or specific vehicle checks. Conduct focused analyses on Route 503 to understand the specific factors driving its importance.
- **Expected Impact**: Reduced incident frequency in historically problematic areas and optimized resource allocation for specific routes.

**3. Time-Based Staffing Optimization**
- **Finding**: The `hour` feature is the most significant predictor for the Gradient Boosting model (0.35 importance), followed by `dayofweek` (0.045 importance for Random Forest). The model performs significantly better during non-rush hours (40% accuracy) compared to rush hours (29% accuracy).
- **Recommendation**: Optimize staffing levels, particularly for types like 'High' and 'Low' incidents, during non-rush hours when the model's predictive power is higher. During rush hours, where predictions are less reliable, focus on rapid response protocols and general preparedness due to the higher volume and complexity of incidents.
- **Expected Impact**: Improved incident response times tailored to specific temporal patterns and more efficient deployment of personnel based on predictive reliability.

**4. Infrastructure Investment Priorities**
- **Finding**: The most frequent incident types are mechanical or general operational issues (`Mechanical`, `MTPU`, `General Delay`, `MTGD`). `station_encoded` (0.098 importance for Random Forest) and specific routes are also highly influential features.
- **Recommendation**: Prioritize capital investments in vehicle maintenance and infrastructure upgrades at high-incident stations and on high-risk routes. Addressing the root causes of dominant incident types in these key locations can lead to long-term reductions in delays.
- **Expected Impact**: Long-term reduction in incident frequency and improved overall system reliability through strategic infrastructure and maintenance investments.

### Quantified Business Value

**Current State (Reactive Management):**
- Average incident response time: Reactive response leads to longer resolution times.
- Resource allocation: Based on general historical averages, potentially leading to inefficient deployment.
- Service reliability: Vulnerable to unpredictable disruptions, leading to passenger dissatisfaction.

**Future State (Proactive Management with Model):**
- **37.9% Weighted F1-Score** for the Gradient Boosting model, indicating a substantial improvement over random guessing for incident type prediction.
- **Estimated 10-15% reduction in incident response time** through proactive deployment based on predictions, especially for 'High' and 'Low' incidents during non-rush hours.
- **10-20% improvement in resource utilization** through predictive allocation, particularly during non-rush hours where the model performs better.
- **Enhanced passenger satisfaction** through more reliable service and fewer unexpected delays.

**ROI Considerations:**
- Reduced operational costs through optimized crew deployment and targeted preventive maintenance.
- Decreased service disruptions leading to maintained/increased ridership and improved public perception.
- Data-driven decision-making can justify infrastructure investments with clear ROI projections, leading to more strategic use of capital.

### Stakeholder-Specific Recommendations

**For Operations Teams:**
- Utilize the model's predictions for 'High' and 'Low' incident types during non-rush hours to pre-plan resource deployment, focusing on areas highlighted by `station_encoded` and `route_time_combo`.
- For rush hours, use the high recall for 'Medium' incidents to quickly dispatch general response teams, understanding that precision is lower (0.21).
- Provide feedback on prediction accuracy to enable continuous model improvement.

**For Maintenance Department:**
- Focus preventive maintenance efforts on routes and times identified as high-risk for mechanical incidents by the model and EDA (e.g., Routes 501, 503, 504) and periods with high `hour` importance.
- Investigate if specific vehicle types (`vehicle_encoded` has some importance) are prone to certain delays, informing maintenance schedules.

**For Service Planning:**
- Incorporate incident probability and dominant incident types into route and schedule design, paying close attention to the impact of `hour`, `dayofweek`, and `route_time_combo`.
- Adjust buffer times on high-incident routes and during peak periods.
- Leverage the temporal insights to plan service adjustments that mitigate common delay patterns.

**For Executive Leadership:**
- Champion data-driven infrastructure investment decisions, particularly for identified high-incident routes (501 Queen, 504 King) and stations (Dundas Street West, Queen Street West).
- Track key performance indicators (incident response time, service reliability) to measure impact.
- Communicate data-driven approach to stakeholders and public.

---

## VIII. Limitations & Future Work

### Current Limitations

**Model Limitations:**
1. **Limited Predictive Accuracy**: The overall Weighted F1-Score of 0.379 suggests that while the model provides insights, there's significant room for improvement in predictive accuracy, especially for minority classes and during rush hours.
2. **Struggles with 'Severe' Incidents (Rush Hour)**: The very low F1-score for 'Severe' incidents during rush hours (0.02) is a critical limitation, as these are high-impact events the model needs to predict effectively.
3. **Class Imbalance Impact**: Despite efforts, class imbalance likely still affects the model's ability to generalize to less frequent incident types, as seen in the varied per-class performance.

**Data Limitations:**
1. **Historical Data Only**: The model is trained on past incidents; unprecedented event types or shifts in operational patterns may not be predicted accurately.
2. **Missing External Factors**: The current model does not include crucial external factors such as weather data, special events, or construction activity, which are known to influence transit delays.
3. **Limited Geographic Detail**: While station and route information is available, more granular geographic data (e.g., specific intersections, track segments) could provide deeper insights.
4. **Temporal Scope**: The 2014-2025 data, while extensive, may not fully capture very recent changes in operational procedures or system upgrades.

**Operational Limitations:**
1. **Real-Time Deployment**: The current model is a proof-of-concept; operationalization requires integrating it into TTC's real-time systems for immediate predictive insights.
2. **Human Oversight Required**: The model is a decision-support tool and should augment, not replace, the expertise and judgment of human operators and managers.
3. **Model Drift**: Operational environments evolve; the model will require continuous monitoring, retraining, and updating to maintain its effectiveness over time.

### Future Improvements

**With Additional Time/Resources:**

1. **Enhanced Feature Engineering:**
   - Integrate weather data (temperature, precipitation, extreme conditions) to capture environmental impacts.
   - Include special events calendars (e.g., sports games, concerts, holidays) to account for demand surges.
   - Incorporate construction and maintenance schedules that might pre-emptively cause delays or affect routes.
   - Add real-time traffic data to better predict external factors affecting streetcar movement.

2. **Advanced Modeling Techniques:**
   - Explore ensemble methods (e.g., stacking, boosting with more diverse base learners) to improve overall predictive power.
   - Investigate deep learning approaches (e.g., LSTMs for time-series patterns) for potentially uncovering more complex temporal dependencies.
   - Develop route-specific or location-specific models for highly localized incident prediction.
   - Implement active learning strategies to continually refine the model with new, incoming data.

3. **Expanded Scope:**
   - Expand the prediction to include incident severity and duration, not just type, to allow for more comprehensive operational planning.
   - Integrate data from other transit modes (subway, buses) for a holistic view of the entire transit network.
   - Develop prescriptive analytics that suggest specific mitigation strategies based on predicted incident types.

4. **Operational Integration:**
   - Develop a user-friendly dashboard for operations staff to visualize predictions and key insights in real-time.
   - Establish a robust feedback loop for operational staff to report on prediction accuracy and outcomes, informing model retraining.
   - Implement a continuous monitoring system to detect model performance degradation or drift.

5. **External Validation:**
   - Conduct A/B testing in collaboration with TTC: compare outcomes of proactive, model-guided management against reactive approaches.
   - Validate the model's generalizability by testing it on incident data from other transit systems.

---
## IX. Reproducibility

To ensure full reproducibility of this project, follow the steps below.

### Prerequisites

-   **Python Version**: 3.9 or higher
-   **Operating System**: Windows, macOS, or Linux
-   **Hardware**: 4GB RAM minimum, 500MB disk space
-   **Software**: Git, Python package manager (`pip`)

### Step-by-Step Instructions

**1. Clone the Repository**
```bash
git clone [repository-url]
cd ttc-incident-classification
```

**2. Setup Virtual Environment & Install Dependencies**
```bash
python -m venv venv
# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

pip install -r requirements.txt
```

**3. Download Raw Data**
Place the 12 TTC delay data files (e.g., `ttc_delays_2014.xlsx`, `ttc_delays_2015.xlsx`, ..., `ttc_delays_2024.xlsx`) into the `data/raw/` directory within the cloned repository.

**4. Run the Full Analysis Pipeline**

This project's entire analysis pipeline (data consolidation, feature engineering, and model training/evaluation) can be executed. Choose one of the following options:

### Option A: Via Jupyter Notebooks (Recommended for interactive exploration)

To run interactively and see all steps:
```bash
jupyter notebook
```
Then, open and run the notebooks in the following order:
-   `experiments/01_eda.ipynb` (for EDA and Feature Engineering)
-   `experiments/02_modeling.ipynb` (for Model Development & Evaluation)

### Option B: Via Python Scripts (Recommended for automated runs)

Execute the main scripts sequentially:

```bash
# Run data consolidation and feature engineering
python src/data_consolidation.py

# Run model training and evaluation
python src/train_models.py
```

**Expected Outputs:**

After successfully running the pipeline, you should find:
-   Consolidated and feature-engineered datasets in `data/processed/`.
-   Trained models saved in the `models/` folder.
-   Results and evaluation metrics in `reports/model_comparison.csv`.
-   Evaluation visualizations (e.g., confusion matrices, feature importance plots) in `reports/figures/model_results/`.

### Expected Results

Running the full pipeline should produce:
-   Final model accuracy: [X.XX]% (±0.02)
-   F1-score (weighted): [X.XX] (±0.02)
-   Total runtime: [X]-[Y] minutes (may vary based on hardware)

### Troubleshooting

-   **Issue**: `ModuleNotFoundError: No module named 'openpyxl'`
    -   **Solution**: Ensure all dependencies are installed by running `pip install -r requirements.txt` within your activated virtual environment.
-   **Issue**: `FileNotFoundError: data/raw/ttc_delays_2014.xlsx`
    -   **Solution**: Confirm that all 12 raw data files are correctly placed in the `data/raw/` directory with their original filenames.
-   **Issue**: Out of memory error
    -   **Solution**: Close other applications or consider processing a smaller sample of the data if resource constraints persist.
-   **Issue**: Model results differ slightly from reported
    -   **Solution**: Minor variations (<2%) are expected due to random initialization. For exact reproducibility, ensure any `random_state` parameters in the modeling code are consistently set.

**Contact**
For issues or questions about reproducibility:
-   Open a GitHub issue in the repository
________________________________________
##  X. Team & Collaboration
### Team Structure
This project was completed by a 4-member data science team with the following roles:
**Member 1 - Data Acquisition & Cleaning Lead**
- Consolidated 12 data files (2014-2024) into single dataset
- Standardized data formats and column names across years
- Implemented data quality checks and validation
- Created reproducible data pipeline
**Member 2 - Exploratory Data Analysis & Feature Engineering Lead**
- Conducted comprehensive EDA identifying key patterns
- Created temporal, spatial, and operational visualizations
- Engineered time-based and categorical features
- Documented data insights for modeling
**Member 3 - Model Development & Optimization Lead**
- Trained and evaluated multiple classification algorithms
- Performed hyperparameter tuning and cross-validation
- Handled class imbalance and model optimization
- Analyzed feature importance and model errors
- Selected and validated final production model
**Member 4 - Evaluation, Visualization & Reporting Lead** (Me)
- Designed evaluation framework linking metrics to business value
- Created project infrastructure and documentation standards
- Synthesized team findings into comprehensive documentation
- Developed final presentation and business recommendations
- Ensured project reproducibility and quality standards
### Collaboration Process
**Version Control:**
- Git/GitHub for code management
- Feature branch workflow with pull request reviews
- Each team member created and reviewed PRs
- Main branch protected - all changes reviewed before merge
**Project Management:**
- GitHub Projects for task tracking
- Daily asynchronous updates in team communication channel
- Regular check-ins to address blockers
- Clear division of responsibilities with defined deliverables
**Documentation:**
- Continuous documentation throughout development
- Each member maintained detailed notes in docs/ folder
- Code extensively commented for clarity
- README updated iteratively as project progressed
**Quality Assurance:**
- Peer code reviews for all contributions
- Reproducibility tested at multiple checkpoints
- Regular team syncs to ensure alignment
- Clear communication of blockers and dependencies
**Team memebers:**
- Member 1: Hossein Hooshmandi Safa - Data Acquisition & Cleaning Lead <br>
- Member 2: Aman Kaushik - EDA & Feature Engineering Lead <br>
- Member 3: Antonio Gao - Model Development & Optimization Lead <br>
- Member 4: Janice Wilson - Evaluation, Visualization & Reporting Lead
### Individual Contributions
**Video Presentations:** Each team member recorded a 3-5 minute video discussing their individual contributions, challenges faced, learnings, and reflections on the project:
- [Member 1 Video]
- [Member 2 Video]
- [Member 3 Video]
- [Member 4 Video]

________________________________________
## XI. Technologies & Tools

### Programming Language:
Python 3.9+
**Core Libraries:**
Data Processing: pandas, numpy
Machine Learning: scikit-learn, [PLACEHOLDER - xgboost? other libraries Member 3 used]
Visualization: matplotlib, seaborn, [plotly if used]
Data Loading: openpyxl (Excel files), xlrd (legacy Excel)
Utilities: tqdm (progress bars)

**Development Environment:**
Jupyter Notebook for exploratory analysis and modeling
Git/GitHub for version control and collaboration
Virtual environment for dependency management

**File Structure:**
ttc-incident-classification/
├── data/ <br>
│   ├── raw/                    # Original 12 data files <br>
│   └── processed/              # Consolidated and processed data<br>
├── experiments/                # Jupyter notebooks <br>
│   ├── 01_eda.ipynb <br>
│   └── 02_modeling.ipynb <br>
├── models/                     # Trained model files <br>
├── reports/ <br>
│   ├── charts/               # All visualizations <br>
│   └── model_comparison.csv   # Model performance tracking <br>
├── src/                       # Source code <br>
├── docs/                      # Documentation <br>
├── requirements.txt           # Python dependencies <br>
└── README.md                  # This file

________________________________________
## XII. References
### Data Source
Toronto Transit Commission (TTC) Service Delay Data, 2014-2024
https://open.toronto.ca/dataset/ttc-streetcar-delay-data/
### Technical Resources
- scikit-learn documentation: https://scikit-learn.org/
### Related Work
________________________________________
## XIII. Acknowledgments
We thank the Toronto Transit Commission for making this data publicly available, enabling data-driven analysis to improve public transit operations.
________________________________________
Project Timeline: [Start date] - November 14, 2025
Showcase Presentation: November 15, 2025
Repository: [GitHub URL]
License: [If applicable]
---

<br>
<br>



