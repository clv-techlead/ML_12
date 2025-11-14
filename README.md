
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

**Data Quality Issues:** [PLACEHOLDER - From Member 1 & Member 2]
- Missing values:  time (6), bound (2280), vehicle (4649), and hour (6) had missing values.
**Data cleaning steps:**
- Numeric columns (vehicle, hour): Missing values were filled with 0.
- Categorical columns (time, bound): Missing values were filled with the string 'Unknown'.
- The date column was converted to datetime format with errors='coerce'.
- The dataset was sorted by date for temporal consistency.

## V. Risks & Limitations 
**Risks & Limitations:**
- **Class Imbalance**:  The EDA revealed that most delays are short, but a few severe incidents skew the average, necessitating specialized handling for modeling. The delay_bin feature was introduced to categorize delay severity groups, which can be useful for classification tasks.
- **Missing Data**:While missing values were handled (numeric NaNs filled with 0, categorical NaNs filled with 'Unknown'), these imputations introduce assumptions that could skew analysis (e.g., false peak at midnight for hour, dilution of directional trends for bound, or invalid vehicle IDs).
- **Temporal Consistency**: Data collection methodology may have changed over 11 years

---

## Methodology

Our analysis followed a structured, milestone-driven approach moving from data consolidation to model deployment:

### Phase 1: Data Consolidation & Quality Assessment

**Objective:** Create clean, consolidated dataset ready for analysis

**Process:** [PLACEHOLDER - Summarize Member 1's work in 3-4 sentences]
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

**Key Questions Investigated:** [PLACEHOLDER - From Member 2's notes]

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
- Delay by incident type: [patterns]
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

## Results

[PLACEHOLDER - This entire section from Member 3]

### Model Performance

**Final Model**: Gradient Boosting (GB)

**Overall Performance:**
| Metric | Score |
|--------|-------|
| Accuracy | [X.XX]% |
| Precision (weighted) | [X.XX] |
| Recall (weighted) | [X.XX] |
| F1-Score (weighted) | 0.379 |

**Per-Class Performance:**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| High | 0.44 | 0.57 | 0.49 | 1731 |
| Low | 0.64 | 0.34 | 0.44 | 1224 |
| Medium | 0.18 | 0.40 | 0.24 | 641 |
| Severe | 0.57 | 0.26 | 0.36 | 1410 |

**Model Comparison:**
[Insert model comparison chart]

Figure 1: Performance comparison across all models tested (Weighted F1-Score)

### Performance in Critical Scenarios

**Peak Rush Hours (7-9 AM, 4-6 PM weekdays):**
- Accuracy: 0.29
- Performance vs overall: Lower than overall non-rush hour performance, suggesting incidents during rush hours are harder to predict or have different underlying patterns.
- Insight: The model struggles with 'Low' and 'Severe' categories during rush hours, achieving F1-scores of 0.21 and 0.02 respectively, while 'Medium' has a high recall (0.74) but low precision (0.21).

**Non-Rush Hours (Gradient Boosting):**
- Accuracy: 0.40
- Performance vs overall: Higher than rush hour performance, indicating better predictability during less congested periods.
- Insight: The model performs best on 'High' (F1: 0.49) and 'Low' (F1: 0.44) incident types during non-rush hours, showing potential for targeted interventions during these periods.
  
**High-Incident Routes (501 Queen, 504 King):**
- Accuracy: [X.XX]%
- Performance vs overall: [comparison]
- Insight: [interpretation]

### Feature Importance

**Top 10 Most Influential Features:**
1. gap_ratio - Importance: 0.147
2. min_gap - Importance: 0.145
3. min_delay - Importance: 0.143
4. station_encoded - Importance: 0.098
5. route_time_combo - Importance: 0.089
6. hour - Importance: 0.068
7. dayofweek - Importance: 0.045
8. station - Importance: 0.045
9. line_encoded - Importance: 0.038
10. month - Importance: 0.031

[Insert feature importance visualization]

Figure X: Feature importance for final model

**Key Insights:**
- min_gap, min_delay, and gap_ratio are highly influential, confirming the strong correlation observed in EDA and their importance in classifying incident types.
- station_encoded, route_time_combo, hour, and dayofweek also rank high, emphasizing the importance of location and temporal factors in incident prediction.
- The importance of engineered interaction features like route_time_combo highlights the value of capturing non-linear relationships between route and time.
- [Business implications]

### Error Analysis

**Confusion Matrix (Gradient Boosting - Non-Rush Hours Example):**
[Insert confusion matrix visualization]

Figure X: Confusion matrix showing actual vs predicted incident types

**Common Misclassifications:**
1. [Class A] confused with [Class B]: [X]% of cases
   - Possible reason: [explanation]
2. [Class C] confused with [Class D]: [X]% of cases
   - Possible reason: [explanation]
- Medium incidents are frequently misclassified, indicating the model struggles to distinguish this category effectively. Despite a high recall of 0.74 in rush hours and 0.40 in non-rush hours, its precision is low (0.21 and 0.18, respectively), suggesting it often predicts 'Medium' when it's not.

**Model Strengths:**
- Excels at predicting 'High' and 'Low' incident types during non-rush hours.
- Achieves reasonable precision for 'Severe' incidents during non-rush hours (0.57).

**Model Limitations:**
- Struggles with the 'Medium' incident type, leading to low precision.
- Overall lower performance during rush hours compared to non-rush hours.
- The low F1-score for 'Severe' incidents during rush hours (0.02) is a significant limitation, as these are critical for proactive management.

---

## Business Impact & Recommendations

[YOU WRITE THIS - Based on Member 3's results]

### Operational Improvements Enabled

Based on our model's performance and feature importance analysis, TTC can implement the following data-driven improvements:

**1. Predictive Resource Allocation**
[PLACEHOLDER - Example based on results]
- **Finding**: While overall accuracy in rush hours is 29%, the model achieves a recall of 0.74 for 'Medium' incidents during these periods. During non-rush hours, 'High' incidents have an F1-score of 0.49.
- **Recommendation**: Pre-position maintenance crews at [location] before 7 AM on weekdays. During rush hours, focus on resource allocation for 'Medium' incidents, acknowledging potential false positives due to lower precision. For non-rush hours, prioritize 'High' and 'Low' incident types for proactive deployment of maintenance crews, especially for mechanical issues.
- **Expected Impact**: Increased preparedness for common incident types and better resource utilization during non-rush hours, leading to an overall 10% reduction in mechanical incident response time. 

**2. Route-Specific Interventions**
- **Finding**: Routes [list] account for [X]% of all incidents. Engineered features like station_encoded and route_time_combo are highly important. EDA confirmed that Routes 501 Queen and 504 King and stations like Dundas Street West and Queen Street West are hotspots.
- **Recommendation:** Implement targeted interventions such as preventive maintenance and increased monitoring for specific route-time combinations and high-incident stations identified in the EDA. For example, Route 501 during 5 PM rush hour. (Add more specific routes and time)
- **Expected Impact:** Reduced incident frequency in historically problematic areas such as. (where?)
  
**3. Time-Based Staffing Optimization**
[PLACEHOLDER]
- **Finding**: [Incident type] peaks during [time period]. The hour and dayofweek features are predictive, and the model performs better during non-rush hours.
- **Recommendation**: [Adjust staffing levels and resource availability during high-risk periods] Optimize staffing levels, particularly for types like 'High' and 'Low' incidents, during non-rush hours when the model's predictive power is higher. During rush hours, focus on rapidly responding to 'Medium' incidents where recall is strong.
- **Expected Impact**: Improved incident response times tailored to specific temporal patterns. (which ones?)

**4. Infrastructure Investment Priorities**
- **Finding**: [Location/route] shows recurring [incident type] Mechanical and general operational issues (Mechanical, MTPU, General Delay, MTGD) are the most frequent incident types. The station_encoded feature is highly important.
- **Recommendation**: Prioritize capital investments in vehicle maintenance and infrastructure upgrades (such as?) at high-incident stations (which ones?), addressing the root causes of dominant incident types.
- **Expected Impact**: Long-term reduction in incident frequency and improved overall system reliability.

### Quantified Business Value

**Current State (Reactive Management):**
- Average incident response time: [estimate]Reactive response leads to longer resolution times.
- Resource allocation: [Based on historical averages] Based on general historical averages, potentially leading to inefficient deployment.
- Service reliability: Vulnerable to unpredictable disruptions, leading to passenger dissatisfaction.

**Future State (Proactive Management with Model):**
- 37.9% Weighted F1-Score for the Gradient Boosting model, indicating a substantial improvement over random guessing for incident type prediction.
- Estimated [X]% reduction in incident response time through proactive deployment based on predictions (e.g., pre-positioning maintenance crews).
- [Y]% improvement in resource utilization through predictive allocation, especially during non-rush hours where the model performs better.
- Enhanced passenger satisfaction through more reliable service and fewer unexpected delays.

**ROI Considerations:**
- Reduced operational costs through optimized crew deployment and targeted preventive maintenance.
- Decreased service disruptions leading to maintained/increased ridership and improved public perception.
- Data-driven decision-making can justify infrastructure investments with clear ROI projections, leading to more strategic use of capital.

### Stakeholder-Specific Recommendations

**For Operations Teams:**
- Use model predictions to guide daily resource deployment 
- Focus on high-probability incident scenarios during peak periods
- Monitor model performance and provide feedback for continuous improvement
- Utilize the model's predictions for 'High' and 'Low' incident types during non-rush hours to pre-plan resource deployment.
- For rush hours, use the high recall for 'Medium' incidents to quickly dispatch general response teams, understanding that precision is lower.
- Provide feedback on prediction accuracy to enable continuous model improvement.

**For Maintenance Department:**
- Prioritize preventive maintenance on routes/times with high mechanical incident probability
- Use feature importance insights to guide vehicle inspection schedules

**For Service Planning:**
- Incorporate incident probability into schedule design
- Adjust buffer times on routes/times with high incident risk
- Plan service improvements based on identified incident patterns

**For Executive Leadership:**
- Use model insights to justify infrastructure investment decisions
- Track key performance indicators (incident response time, service reliability) to measure impact
- Communicate data-driven approach to stakeholders and public

---

## Limitations & Future Work

### Current Limitations

**Model Limitations:**
1. Limited Predictive Accuracy: The overall Weighted F1-Score of 0.379 suggests that while the model provides insights, there's significant room for improvement in predictive accuracy, especially for minority classes and during rush hours
2. Struggles with 'Severe' Incidents (Rush Hour): The very low F1-score for 'Severe' incidents during rush hours (0.02) is a critical limitation, as these are high-impact events the model needs to predict effectively.
3. Class Imbalance Impact: Despite efforts, class imbalance likely still affects the model's ability to generalize to less frequent incident types, as seen in the varied per-class performance.

**Data Limitations:**
1. **Historical Data Only**: Model trained on past incidents; unprecedented event types may not be predicted accurately
2. **Missing External Factors**: The current model does not include crucial external factors such as weather data, special events, or construction activity, which are known to influence transit delays.
3. **Limited Geographic Detail**:  While station and route information is available, more granular geographic data (e.g., specific intersections, track segments) could provide deeper insights.
4. **Temporal Scope**: The 2014-2025 data, while extensive, may not fully capture very recent changes in operational procedures or system upgrades.

**Operational Limitations:**
1. **Real-Time Deployment**: The current model is a proof-of-concept; operationalization requires integrating it into TTC's real-time systems for immediate predictive insights.
2. **Human Oversight Required**: The model is a decision-support tool and should augment, not replace, the expertise and judgment of human operators and managers.
3. **Model Drift**:  Operational environments evolve; the model will require continuous monitoring, retraining, and updating to maintain its effectiveness over time.

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
   - Include data from other transit modes (subway, buses) for a holistic view of the entire transit network.
   - Develop prescriptive analytics that suggest specific mitigation strategies based on predicted incident types.

4. **Operational Integration:**
   - Develop a user-friendly dashboard for operations staff to visualize predictions and key insights in real-time.
   - Establish a robust feedback loop for operational staff to report on prediction accuracy and outcomes, informing model retraining.
   - Implement a continuous monitoring system to detect model performance degradation or drift.

5. **External Validation:**
   - Conduct A/B testing in collaboration with TTC: compare outcomes of proactive, model-guided management against reactive approaches.
   - Validate the model's generalizability by testing it on incident data from other transit systems.

---

## Reproducibility

### Prerequisites

- **Python Version**: 3.9 or higher
- **Operating System**: Windows, macOS, or Linux
- **Hardware**: 4GB RAM minimum, 500MB disk space
- **Software**: Git, Python package manager (pip)

### Step-by-Step Instructions

**1. Clone the Repository**
```bash
git clone [repository-url]
cd ttc-incident-classification

2. Create Virtual Environment
python -m venv venv
```
### Activate virtual environment:
### On macOS/Linux:
source venv/bin/activate
### On Windows:
venv\Scripts\activate

3. Install Dependencies
pip install -r requirements.txt

4. Download Data Place the 12 TTC delay data files in the data/raw/ directory:
ttc_delays_2014.xlsx
ttc_delays_2015.xlsx
... (list all files)
ttc_delays_2024.xlsx
5. Run Data Consolidation [PLACEHOLDER - Update based on Member 1's final implementation]
### Option A: If using Jupyter notebook
jupyter notebook models/model.ipynb

### Option B: If using Python script
python src/data_consolidation.py

Expected Output:
Consolidated dataset: data/processed/streetcar_delays_2014_2024.csv
Record count: [X] incidents
Processing time: Approximately [Y] seconds
6. Run EDA (Optional - to view analysis)
jupyter notebook experiments/01_eda.ipynb

This notebook contains all exploratory analysis and visualizations.
7. Train Models
jupyter notebook experiments/02_modeling.ipynb

Or if Member 3 created a script:
python src/train_models.py

Expected Output:
Trained models saved in models/ folder
Results saved in reports/model_comparison.csv
Evaluation visualizations in reports/figures/model_results/
Training time: Approximately [X] minutes
8. View Results
Model comparison: reports/model_comparison.csv
Best model: models/[final_model_name].pkl
All visualizations: reports/figures/
### Expected Results
Running the full pipeline should produce:
Final model accuracy: [X.XX]% (±0.02)
F1-score (weighted): [X.XX] (±0.02)
Total runtime: [X]-[Y] minutes
### Troubleshooting
Issue: ModuleNotFoundError: No module named 'openpyxl'
Solution: Run pip install -r requirements.txt to install all dependencies
Issue: FileNotFoundError: data/raw/ttc_delays_2014.xlsx
Solution: Ensure all 12 data files are in data/raw/ directory with correct filenames
Issue: Out of memory error
Solution: Close other applications or reduce sample size in configuration
Issue: Model results differ slightly from reported
Solution: Minor variations (<2%) are expected due to random initialization. Set random_state parameter for exact reproducibility.
Contact
For issues or questions about reproducibility:
Open a GitHub issue in the repository
Contact: [team contact information]
________________________________________
##  Team & Collaboration
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
### Individual Contributions
**Video Presentations:** Each team member recorded a 3-5 minute video discussing their individual contributions, challenges faced, learnings, and reflections on the project:
- [Member 1 Video]
- [Member 2 Video]
- [Member 3 Video]
- [Member 4 Video]
________________________________________
## Technologies & Tools
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
├── data/
│   ├── raw/                    # Original 12 data files
│   └── processed/              # Consolidated and processed data
├── experiments/                # Jupyter notebooks
│   ├── 01_eda.ipynb
│   └── 02_modeling.ipynb
├── models/                     # Trained model files
├── reports/
│   ├── figures/               # All visualizations
│   └── model_comparison.csv   # Model performance tracking
├── src/                       # Source code
├── docs/                      # Documentation
├── requirements.txt           # Python dependencies
└── README.md                  # This file

________________________________________
## References
### Data Source
Toronto Transit Commission (TTC) Service Delay Data, 2014-2024
[Add specific data source URL if available]
### Technical Resources
- scikit-learn documentation: https://scikit-learn.org/
- [PLACEHOLDER - Add any specific papers, tutorials, or resources used]
### Related Work
- [PLACEHOLDER - Any similar transit incident classification studies referenced]
________________________________________
## Acknowledgments
We thank the Toronto Transit Commission for making this data publicly available, enabling data-driven analysis to improve public transit operations.
________________________________________
Project Timeline: [Start date] - November 14, 2025
Showcase Presentation: November 15, 2025
Repository: [GitHub URL]
License: [If applicable]
---
+++

| Category | Title | Risk / Unknown | Impact | Mitigation / Approach |
|----------|-------|----------------|--------|------------------------|
|**Data Quality**| Inconsistent Data Formats Across Years | Column names, encoding schemes, or incident categorization may have changed over 11 years | Could complicate data consolidation and require extensive data mapping | Early data inventory phase to document all format variations; create robust parsing functions that handle multiple formats |
|              | Missing or Incomplete Data | Critical features may have missing values, especially in earlier years (2014-2016) | Could reduce usable dataset size or introduce bias in model training | Comprehensive missing data analysis; document missingness patterns; implement appropriate imputation strategies or exclude incomplete records with justification |
|             | Data Collection Methodology Changes | TTC may have changed how incidents are recorded or classified over time | Could introduce temporal bias where earlier years aren't comparable to recent years | Analyze data collection practices by year; consider training separate models by time period if necessary; document any identified methodology shifts |
|**Modeling**| Class Imbalance | Some incident types may be far more common than others (e.g., mechanical issues vs. security incidents) | Model may over-predict common classes and struggle with rare incident types | Implement SMOTE (Synthetic Minority Over-sampling Technique), adjust class weights, or use stratified sampling; evaluate with balanced metrics (F1-score, per-class recall) |
|          | Feature Correlation and Multicollinearity | Route, location, and time features may be highly correlated | Could affect model interpretability and performance | Conduct correlation analysis during EDA; use feature selection techniques; test models robust to multicollinearity (tree-based models) |
|          | Temporal Data Leakage | Using future information to predict past events in train/test split | Artificially inflated performance metrics that won't generalize | Implement time-based train/test splits; careful feature engineering to exclude future-looking variables |
|**Execution** | Time Constraints | Two-week timeline is aggressive for data consolidation, modeling, and documentation | May need to limit scope or depth of analysis | Clear milestone deadlines; prioritize core requirements; document "future work" early; daily standups to identify blockers quickly |
|           | Merge Conflicts and Integration | Four team members working simultaneously could create code conflicts | Time lost resolving conflicts; potential code breaks | Small, frequent PRs; clear feature branch strategy; immediate conflict resolution; work on different files when possible |
|           | Reproducibility Challenges | Complex data pipeline may be difficult to reproduce | Project evaluation may fail reproducibility requirements | Document as we build; test reproducibility at each milestone; clear requirements.txt; step-by-step README instructions |
|**Unknowns** | Business Context Gaps | We may not fully understand TTC's operational definitions of incident types |   | Research TTC incident classification system; may need to make assumptions (document all assumptions clearly) |
|         | Feature Availability | Exact features available across all 12 files not yet confirmed |   | Complete data inventory in first 2 days; adjust feature engineering plan based on actual available data |
|         | Computational Resources | Dataset size may require significant processing power for model training |   | Assess during data consolidation; may need to sample data or use cloud resources if local machines insufficient | 

-----

<br>
<br>

## VI. Approach to Analysis

Our analysis will follow a structured, milestone-driven approach moving from broad industry context to specific technical solutions:

### Project Plan Overview

| Phase | Days | Objective | Task Group | Tasks |
|-------|------|-----------|------------|-------|
| **Phase 1: Data Foundation** | 1–3 | Consolidated, clean dataset ready for analysis | **Data Inventory & Assessment** | - Document all 12 files: structure, columns, formats, record counts<br>- Review data dictionary/readme for column definitions<br>- Identify format variations across years<br>- Assess data quality: missing values, duplicates, inconsistencies |
| | | | **Data Consolidation Pipeline** | - Develop scripts to load Excel/CSV files and extract monthly tabs<br>- Standardize column names across all years<br>- Merge into single consolidated dataset<br>- Handle data type conversions and encoding issues |
| | | | **Data Cleaning** | - Address missing values (imputation or exclusion with justification)<br>- Remove duplicate records<br>- Standardize categorical variables (incident types, routes, locations)<br>- Create data quality report documenting all transformations |
| **Phase 2: EDA & Feature Engineering** | 4–6 | Deep understanding of data patterns and engineered features ready for modeling | **Exploratory Data Analysis** | - Time-related Analysis: yearly, seasonal, monthly patterns<br>- Incident Type Distribution: class balance, common vs. rare<br>- Route Analysis: incident frequency and type by route<br>- Time-of-Day Patterns: rush hour vs. off-peak; weekend vs. weekday<br>- Delay Duration Analysis: distribution and relationship to incident type<br>- Geographic Patterns: hotspots, station vs. between-station<br>- Correlation Analysis: feature relationships |
| | | | **Feature Engineering** | - Time-Based Features: hour, day, month, season, rush hour, weekend, time since last incident<br>- Categorical Encoding: route, location, service type<br>- Delay Features: bins, normalized by route average<br>- Interaction Features: route × time/day, location × time |
| | | | **Train/Test Split Strategy** | - Time-based split (e.g., 2014–2023 train, 2024–2025 test)<br>- Stratified by incident type<br>- Validation set for hyperparameter tuning |
| **Phase 3: Model Development & Optimization** | 7–10 | Trained, optimized classification model with documented performance | **Baseline Model** | - Logistic Regression or Decision Tree<br>- Establish baseline metrics (accuracy, precision, recall, F1-score)<br>- Identify issues (class imbalance, feature separation) |
| | | | **Advanced Model Testing** | - Random Forest: non-linear relationships, feature importance<br>- Gradient Boosting (XGBoost/LightGBM): strong tabular performance<br>- SVM: high-dimensional data (if feasible)<br>- Compare models using consistent evaluation |
| | | | **Handling Class Imbalance** | - Test SMOTE<br>- Adjust class weights<br>- Try undersampling<br>- Evaluate per-class performance |
| | | | **Hyperparameter Optimization** | - GridSearchCV or RandomizedSearchCV<br>- Cross-validation (5-fold or 10-fold)<br>- Optimize for F1-score |
| | | | **Feature Selection** | - Analyze tree-based feature importance<br>- Remove low-importance/redundant features<br>- Test reduced feature set |
| | | | **Final Model Selection** | - Compare on hold-out test set<br>- Select based on metrics, interpretability, efficiency<br>- Document rationale |
| **Phase 4: Evaluation & Interpretation** | 9–11 | Comprehensive understanding of model performance and business implications | **Performance Evaluation** | - Confusion matrix<br>- Per-class metrics<br>- ROC & AUC<br>- Precision-Recall curves<br>- Overall accuracy & weighted F1-score |
| | | | **Error Analysis** | - Misclassified incident types<br>- Feature confusion<br>- Systematic error patterns |
| | | | **Feature Importance Analysis** | - Key predictors<br>- Alignment with domain knowledge<br>- Visualizations |
| | | | **Business Insights Generation** | - Actionable recommendations<br>- Quantify operational improvements<br>- Identify high-risk routes/times/locations |
| **Phase 5: Documentation & Presentation** | 12–14 | Complete, reproducible project with compelling narrative | **Code Finalization** | - Clean, comment, modularize code<br>- Remove unused files<br>- Create reproducible scripts |
| | | | **README Documentation** | - Complete all sections<br>- Clear reproducibility instructions<br>- Include visualizations<br>- Link videos |
| | | | **Reproducibility Testing** | - Team member tests full pipeline<br>- Verify requirements.txt<br>- Confirm step-by-step instructions |
| | | | **Videos & Showcase Prep** | - Each member records 3–5 min video<br>- Team prepares 5-min elevator pitch<br>- Practice timing |

-----
<br>
<br>

## VII. Team Roles & Responsibilities


### Team Roles:


| Member      | Role | Main Goal | Collaboration Responsibilities |
|-------------|------|-----------|-------------------------------|
|**Member 1**| Data Acquisition & Cleaning Lead | Collect, merge, and clean raw TTC delay datasets | - Review PRs from Member 3<br>- Support team with data-related questions<br>- Participate in daily standups |
|**Member 2**| EDA & Feature Engineering Lead | Understand data patterns and design predictive features | - Review PRs from Member 4<br>- Provide feature importance interpretation to modeling team<br>- Participate in daily standups |
|**Member 3**| Model Development & Optimization Lead | Train and tune classification models | - Review PRs from Member 1<br>- Collaborate with Member 2 on feature selection<br>- Participate in daily standups |
|**Member 4**| Evaluation, Visualization & Reporting Lead | Interpret model results, visualize findings, and prepare final deliverable | - Review PRs from Member 2<br>- Coordinate README content with all members<br>- Lead final documentation review<br>- Participate in daily standups |

---

### Team Responsibilities (Days 1–14):

| Day | Member 1: Data Lead | Member 2: EDA Lead | Member 3: Model Lead | Member 4: Reporting Lead |
|-----|---------------------|--------------------|----------------------|--------------------------|
| 1–2 | GitHub setup<br>Data inventory | Initial EDA setup | Research modeling approaches | Evaluation framework planning |
| 3–4 | Data consolidation pipeline<br>Standardization | Temporal & route analysis<br>Visualizations | Baseline model implementation | Metric definitions<br>Confusion matrix setup |
| 5–6 | Data cleaning<br>Quality report | Feature engineering<br>Interaction features | Class imbalance handling<br>Model comparison | ROC/PR curve generation<br>Error analysis |
| 7–8 | Reproducibility testing<br>requirements.txt | Feature refinement based on model feedback | Hyperparameter tuning<br>Feature selection | Visualization suite development |
| 9–10 | Support model team<br>Review PRs | Finalize features<br>Document rationale | Final model selection<br>Save trained model | README writing<br>Business insights generation |
| 11–12 | Assist with reproducibility testing | Support documentation | Model documentation | README finalization<br>Interactive visuals |
| 13–14 | Final review & support | Final review & support | Final review & support | Showcase prep<br>Video integration<br>Presentation coordination |

-----

<br>

### Shared Responsibilities (All Team Members)

**Git & Collaboration:**
- Each member must create at least 1 Pull Request
- Each member must review and merge a different member's PR
- Conduct thorough code reviews with constructive feedback
- Follow branching strategy (never commit directly to main)
- Make small, frequent commits with clear messages
- Address merge conflicts promptly

**Communication:**
- Attend daily 15-minute standup meetings
- Update project management board (GitHub Projects) daily
- Immediately communicate blockers or delays
- Collaborate on problem-solving when team members are stuck

**Documentation:**
- Comment code as it's written
- Use clear, descriptive variable and function names
- Write docstrings for all functions
- Contribute to respective README sections
- Document decisions and rationale

**Quality Assurance:**
- Test own code before creating PR
- Test reproducibility of components created
- Participate in final reproducibility testing
- Clean up unused code and files

**Individual Videos:**
- Each member records 3-5 minute video covering:
- Personal contributions to the project
- Technical challenges faced and how you overcame them
- What you learned through the project
- What you would add/improve with more time
- How you contributed to team collaboration
- Upload video (YouTube/Google Drive) and provide link

**Showcase Presentation:**
- Participate in presentation preparation
- Practice 5-minute elevator pitch as a team
- Be prepared to answer questions about the project

**Team Collaboration Framework**
- Daily Standup:
    What did you complete since last standup?
    What are you working on today?
    Any blockers or challenges?

**Project Management:**
- Use project spreadsheet to track all tasks
- Tasks organized by milestone
- Each task assigned to specific team member(s)
- Status updated daily (Not Started, In Progress, Review, Completed)

**Decision-Making:**
- Major decisions (model selection, approach changes) discussed as full team
- If disagreement, defer to person with primary responsibility for that area

<br>

## VIII. Project Timeline Summary
<br>

| Milestone | Target Date | Key Deliverables |
|-----------|-------------|------------------|
| **Milestone 1: Foundation & Setup** | End of Day 3 | - README proposal<br>- Data inventory<br>- Team aligned on scope and roles |
| **Milestone 2: Data Ready & EDA** | End of Day 6 | - Consolidated dataset<br>- EDA complete<br>- Features engineered<br>- Baseline model implemented |
| **Milestone 3: Models Trained** | End of Day 10 | - Multiple models trained<br>- Models optimized<br>- Evaluation completed |
| **Milestone 4: Final Deliverable** | Nov 14 | - Complete README<br>- Individual videos recorded<br>- Presentation materials finalized |
| **Showcase** | Nov 15 | - 5-minute team presentation |

<div style="border-top: 1px solid #ccc; width: 580px;"></div>

<br>

## IX. Success Criteria

This project will be considered successful when:
1. Classification model achieves 75%+ accuracy across incident types
2. Code is clean, well-documented, and fully reproducible
3. README provides comprehensive documentation accessible to technical and non-technical readers
4. All team members have meaningfully contributed (visible in PRs, videos, and collaboration)
5. Actionable insights are provided that could improve TTC operations
6. Model and methodology could be deployed or extended by TTC staff
7. Project demonstrates application of skills across all program modules
8. Team can confidently present and defend technical and business decisions

## X. Project Team Members

Member 1: Hossein Hooshmandi Safa - Data Acquisition & Cleaning Lead <br>
Member 2: Aman Kaushik - EDA & Feature Engineering Lead <br>
Member 3: Antonio Gao - Model Development & Optimization Lead <br>
Member 4: Janice Wilson - Evaluation, Visualization & Reporting Lead

Project Start Date: November 4, 2025 <br>
Showcase Presentation: November 15, 2025
<br>
<br>
<br>
<br>


**-----End of Project Proposal---**

## Techniques & Technologies
(Highllight the tools and methods used)


## Key Findings & Instructions
(Summarize outcomes and provide setup instructions)


## Visuals & Credits
(Enhance with visuals, Acknowledge Contributors )
=======
