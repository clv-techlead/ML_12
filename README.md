
<h1 style="border-bottom:none;">Transit Incident Classification - TTC Streetcar Delay Analysis
<br>
<br>

## Executive Summary

The Toronto Transit Commission (TTC) manages thousands of service incidents annually, each causing delays that impact operations, costs, and passenger satisfaction. This project develops a machine learning classification model to predict streetcar incident types before they occur based on historical data (2014-2024), enabling TTC to shift from reactive incident management to proactive operational planning and improve service reliability for Toronto's transit riders..

**Deliverable**: A reproducible classification model with actionable insights for operational improvements, supported by the analysis of 11+ years of incident data.

**Key Results:** [PLACEHOLDER - Member 3 to provide]
- Final model achieves [X]% accuracy in classifying incident types
- [X]% improvement over baseline reactive approach
- Model excels at predicting [top incident types]
- Enables [estimated impact] reduction in incident response time

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

**Data Consolidation:** [PLACEHOLDER - Summarize Member 1's work]
- All 12 files merged into single dataset
- Column names standardized across years
- Processing time: [X] seconds for [Y] records

**Data Quality Issues:** [PLACEHOLDER - From Member 1 & Member 2]
- Missing values: [percentage/columns]
- Duplicates: [count/handling]
- Data cleaning steps: [list]

## V. Risks & Limitations 
**Risks & Limitations:**
- **Class Imbalance**: [PLACEHOLDER - Member 2 to document from EDA] Some incident types significantly more common than others
- **Missing Data**: [PLACEHOLDER] 
- **Temporal Consistency**: Data collection methodology may have changed over 11 years
- **2025 Data Excluded**: Incomplete year (only 10 months) excluded to avoid skewing temporal analysis

---

## Methodology

Our analysis followed a structured, milestone-driven approach moving from data consolidation to model deployment:

### Phase 1: Data Consolidation & Quality Assessment

**Objective:** Create clean, consolidated dataset ready for analysis

**Process:** [PLACEHOLDER - Summarize Member 1's work in 3-4 sentences]
- Loaded 12 Excel/CSV files spanning 2014-2024
- Standardized column names and data types across years
- Merged monthly data into single consolidated dataset
- Performed initial data quality checks

**Output:**
- Consolidated dataset: `data/processed/streetcar_delays_2014_2024.csv`
- [X] total incident records
- [Y] features available for analysis

### Phase 2: Exploratory Data Analysis (EDA)

**Objective:** Understand data patterns and design predictive features

**Key Questions Investigated:** [PLACEHOLDER - From Member 2's notes]

1. **Incident Type Distribution:**
   - [Number] distinct incident types identified
   - [List top 3-5 types with percentages]
   - Class imbalance: [describe]

2. **Temporal Patterns:**
   - **Peak Incident Times**: [findings about rush hour vs off-peak]
   - **Day of Week Patterns**: [weekday vs weekend findings]
   - **Seasonal Patterns**: [monthly/seasonal trends]
   - **Trends Over Time**: [2014-2024 trends]

3. **Geographic Patterns:**
   - **High-Incident Routes**: [Top routes and their incident counts]
   - **Location Hotspots**: [Key stations/intersections]

4. **Delay Characteristics:**
   - Average delay duration: [X] minutes
   - Delay by incident type: [patterns]
   - Relationship between features and delays

**Key Findings:** [PLACEHOLDER - Member 2's top 3-5 insights]
1. [Finding 1]
2. [Finding 2]
3. [Finding 3]

**Visualizations:**
[Include 3-4 key EDA charts here with captions]
- Figure 1: Incident Type Distribution
- Figure 2: Temporal Heatmap (Hour × Day of Week)
- Figure 3: Top 10 Routes by Incident Count
- Figure 4: Delay Duration by Incident Type

### Phase 3: Feature Engineering

**Objective:** Create meaningful features from raw data to improve model performance

**Features Created:** [PLACEHOLDER - From Member 2's notes]

**Time-Based Features:**
- `hour`: Hour of day (0-23)
- `day_of_week`: Day of week (0=Monday, 6=Sunday)
- `month`: Month (1-12)
- `season`: Season (Winter/Spring/Summer/Fall)
- `is_rush_hour`: Boolean flag for 7-9 AM and 4-6 PM
- `is_weekend`: Boolean flag for Saturday/Sunday
- `is_morning_rush`: Boolean flag for 7-9 AM
- `is_evening_rush`: Boolean flag for 4-6 PM

**Categorical Encoding:**
- Route encoding: [method used]
- Location encoding: [method used]
- [Other categorical features]

**Rationale:** [PLACEHOLDER - Brief explanation from Member 2]
These features capture temporal patterns identified in EDA, enabling the model to learn that certain incident types are more common during specific times, days, or seasons.

**Output:**
- Enhanced dataset: `data/processed/data_with_features.csv`
- [X] total features for modeling

### Phase 4: Model Development & Optimization

**Objective:** Train and optimize classification models to predict incident types

[PLACEHOLDER - Most of this section comes from Member 3]

**Models Tested:**

1. **Baseline Model**: [Model type]
   - Purpose: Establish baseline performance
   - Performance: [accuracy, F1-score]

2. **Model 2**: [e.g., Random Forest]
   - Rationale: [why this model]
   - Hyperparameters: [key parameters]
   - Performance: [metrics]

3. **Model 3**: [e.g., XGBoost]
   - Rationale: [why this model]
   - Hyperparameters: [key parameters]
   - Performance: [metrics]

**Handling Class Imbalance:**
- Approach used: [SMOTE, class weights, etc.]
- Impact: [improvement in minority class performance]

**Hyperparameter Tuning:**
- Method: [GridSearchCV, RandomizedSearchCV]
- Parameters optimized: [list]
- Performance improvement: [before/after metrics]

**Final Model Selection:**
- **Selected Model**: [Model name]
- **Rationale**: [Why this model - balance of performance, interpretability, speed]

---

## Results

[PLACEHOLDER - This entire section from Member 3]

### Model Performance

**Final Model**: [Model name and configuration]

**Overall Performance:**
| Metric | Score |
|--------|-------|
| Accuracy | [X.XX]% |
| Precision (weighted) | [X.XX] |
| Recall (weighted) | [X.XX] |
| F1-Score (weighted) | [X.XX] |

**Per-Class Performance:**
| Incident Type | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| [Type 1] | [X.XX] | [X.XX] | [X.XX] | [count] |
| [Type 2] | [X.XX] | [X.XX] | [X.XX] | [count] |
| [Type 3] | [X.XX] | [X.XX] | [X.XX] | [count] |
| [Type 4] | [X.XX] | [X.XX] | [X.XX] | [count] |
| [Type 5] | [X.XX] | [X.XX] | [X.XX] | [count] |

**Model Comparison:**
[Insert model comparison chart]

Figure X: Performance comparison across all models tested

### Performance in Critical Scenarios

**Peak Rush Hours (7-9 AM, 4-6 PM weekdays):**
- Accuracy: [X.XX]%
- Performance vs overall: [comparison]
- Insight: [interpretation]

**High-Incident Routes (501 Queen, 504 King):**
- Accuracy: [X.XX]%
- Performance vs overall: [comparison]
- Insight: [interpretation]

### Feature Importance

**Top 10 Most Influential Features:**
1. [Feature name] - Importance: [X.XXX]
2. [Feature name] - Importance: [X.XXX]
3. [Feature name] - Importance: [X.XXX]
4. [Feature name] - Importance: [X.XXX]
5. [Feature name] - Importance: [X.XXX]
[Continue to 10]

[Insert feature importance visualization]

Figure X: Feature importance for final model

**Key Insights:**
- [What these features tell us about incident classification]
- [Business implications]

### Error Analysis

**Confusion Matrix:**
[Insert confusion matrix visualization]

Figure X: Confusion matrix showing actual vs predicted incident types

**Common Misclassifications:**
1. [Class A] confused with [Class B]: [X]% of cases
   - Possible reason: [explanation]
2. [Class C] confused with [Class D]: [X]% of cases
   - Possible reason: [explanation]

**Model Strengths:**
- Excels at predicting [incident types]
- Strong performance during [conditions]

**Model Limitations:**
- Struggles with [incident types]
- Lower performance during [conditions]

---

## Business Impact & Recommendations

[YOU WRITE THIS - Based on Member 3's results]

### Operational Improvements Enabled

Based on our model's performance and feature importance analysis, TTC can implement the following data-driven improvements:

**1. Predictive Resource Allocation**
[PLACEHOLDER - Example based on results]
- **Finding**: Model identifies [route X] has [Y]% higher mechanical incident probability during morning rush
- **Recommendation**: Pre-position maintenance crews at [location] before 7 AM on weekdays
- **Expected Impact**: [X]% reduction in mechanical incident response time

**2. Route-Specific Interventions**
[PLACEHOLDER]
- **Finding**: Routes [list] account for [X]% of all incidents
- **Recommendation**: Implement targeted preventive maintenance schedules for these routes
- **Expected Impact**: [estimated reduction in incidents]

**3. Time-Based Staffing Optimization**
[PLACEHOLDER]
- **Finding**: [Incident type] peaks during [time period]
- **Recommendation**: Adjust staffing levels and resource availability during high-risk periods
- **Expected Impact**: Improved incident response times

**4. Infrastructure Investment Priorities**
[PLACEHOLDER]
- **Finding**: [Location/route] shows recurring [incident type]
- **Recommendation**: Prioritize capital improvements (track maintenance, signal upgrades) at identified hotspots
- **Expected Impact**: Long-term reduction in incident frequency

### Quantified Business Value

**Current State (Reactive Management):**
- Average incident response time: [estimate]
- Resource allocation: Based on historical averages
- Service reliability: Vulnerable to unpredictable disruptions

**Future State (Proactive Management with Model):**
- **[X]% improvement in incident type prediction accuracy**
- **Estimated [Y]% reduction in incident response time** through proactive deployment
- **[Z]% improvement in resource utilization** through predictive allocation
- **Enhanced passenger satisfaction** through more reliable service

**ROI Considerations:**
- Reduced operational costs through optimized crew deployment
- Decreased service disruptions leading to maintained/increased ridership
- Improved public perception and trust through transparent, data-driven operations

### Stakeholder-Specific Recommendations

**For Operations Teams:**
- Use model predictions to guide daily resource deployment decisions
- Focus on high-probability incident scenarios during peak periods
- Monitor model performance and provide feedback for continuous improvement

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
[PLACEHOLDER - From Member 3]
1. [Limitation 1 - e.g., lower performance on minority classes]
2. [Limitation 2 - e.g., cannot predict novel incident types]
3. [Limitation 3 - e.g., performance degrades in extreme weather]

**Data Limitations:**
1. **Historical Data Only**: Model trained on past incidents; unprecedented event types may not be predicted accurately
2. **Missing External Factors**: Weather data, special events, construction activity not included in current model
3. **Limited Geographic Detail**: Location data may not capture micro-level factors (e.g., specific track conditions)
4. **Temporal Scope**: 2014-2024 data may not reflect future operational changes or system upgrades

**Operational Limitations:**
1. **Real-Time Deployment**: Current model requires batch processing; real-time prediction infrastructure needed for operational use
2. **Human Oversight Required**: Model should augment, not replace, human decision-making
3. **Model Drift**: Performance may degrade over time as operational patterns change

### Future Improvements

**With Additional Time/Resources:**

1. **Enhanced Feature Engineering:**
   - Integrate weather data (temperature, precipitation, extreme conditions)
   - Include special events calendar (sports games, concerts, holidays)
   - Add construction/maintenance schedules
   - Incorporate real-time traffic data

2. **Advanced Modeling Techniques:**
   - Ensemble methods combining multiple models
   - Deep learning approaches (LSTM for temporal patterns)
   - Route-specific models for high-incident corridors
   - Real-time prediction system with continuous learning

3. **Expanded Scope:**
   - Include subway and bus incidents for system-wide prediction
   - Predict incident severity/duration in addition to type
   - Develop incident prevention recommendations (not just classification)
   - Create early warning system for cascading delays

4. **Operational Integration:**
   - Deploy model into TTC's operational systems
   - Develop user-friendly dashboard for operations staff
   - Implement feedback loop for continuous model improvement
   - Establish monitoring system for model performance drift

5. **External Validation:**
   - Test model on other transit systems
   - Collaborate with TTC to validate real-world impact
   - Conduct A/B testing: proactive (model-guided) vs reactive management

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
# Activate virtual environment:
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

3. Install Dependencies
pip install -r requirements.txt

4. Download Data Place the 12 TTC delay data files in the data/raw/ directory:
ttc_delays_2014.xlsx
ttc_delays_2015.xlsx
... (list all files)
ttc_delays_2024.xlsx
5. Run Data Consolidation [PLACEHOLDER - Update based on Member 1's final implementation]
# Option A: If using Jupyter notebook
jupyter notebook models/model.ipynb

# Option B: If using Python script
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
