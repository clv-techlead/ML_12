
<h1 style="border-bottom:none;">ML_12 TTC Streetcar Delays Classification Project Proposal
<br>
<br>

## Project Purpose & Overview



This project develops a machine learning classification model to predict Toronto Transit Commission (TTC) streetcar incident types using historical delay data from 2014 to 2025. By analyzing patterns in route, time of day, delay duration, and location, we aim to transform reactive incident management into proactive, data-driven operations.

**Goal**: Our goal is to enable the TTC to anticipate incident types before they occur, optimize resource allocation, and improve service reliability for Toronto's transit riders.

**Deliverable**: A reproducible classification model with actionable insights for operational improvements, supported by the analysis of 11+ years of incident data.

**Team**: 4-member data science team applying machine learning, feature engineering, and statistical analysis to real-world transit operations.

<br>

## I. Business Motivation

### Industry Context
Public transit systems are the backbone of urban mobility, serving millions of passengers daily. The Toronto Transit Commission (TTC), as one of North America's largest transit systems, faces the complex challenge of managing diverse service incidents that impact operations, passenger experience, and resource allocation. Service delays and incidents have direct consequences on rider satisfaction, operational costs, and system reliability.

### The Problem
This project aims to help the TTC improve service reliability and operational response by identifying and predicting the types of streetcar incidents that cause delays. By building a classification model that learns from historical data (2014–2025), the organization can better understand which factors (e.g. route, time of day, delay duration, location) are most associated with different incident types. 

Currently, transit authorities face challenges in:
- **Reactive Operations**: Incidents are often managed as they occur without predictive insights into incident types
- **Resource Misallocation**: Without accurate incident classification, maintenance crews, vehicles, and personnel may be deployed inefficiently
- **Decision-Making**: Operations managers lack adequate data-driven insights about which routes, times, and locations are most vulnerable to specific incident types
- **Customer Dissatisfaction**: Inability to anticipate and prevent specific incident patterns leads to recurring delays and ultimately customer dissatisfaction.

### Business Value & Expected Impact
From a business perspective, this analysis delivers data-driven decision support to reduce downtime, improve passenger satisfaction, and enhance resource efficiency. With accurate incident classification and trend analysis, TTC planners can:

- **Optimize scheduling and resource allocation**: Deploy maintenance crews more effectively based on predicted incident types and high-risk periods
- **Enhance coordination**: Improve communication between transit control, operators, and emergency response teams with better incident categorization
- **Prioritize capital investments**: Make informed decisions about infrastructure improvements (signal upgrades, track maintenance) where recurrent delays occur
- **Anticipate high-risk periods**: Proactively prepare for routes and times with elevated incident probability
- **Reduce operational costs**: Minimize downtime and improve fleet utilization through predictive maintenance
- **Improve on-time performance metrics**: Target interventions that directly impact service reliability KPIs
- **Enable transparent public reporting**: Provide accurate, data-backed service reliability information to maintain public trust and ridership

Over time, these capabilities translate to measurable improvements in operational efficiency **(an estimated 10-15% reduction in incident response time)**, passenger satisfaction scores, and cost savings through optimized resource deployment.

### Stakeholder Impact
The resulting insights from this project will provide a number of positive impacts to the following stakeholder groups:

- **Transit Operations Teams** can deploy resources proactively based on predicted incident types rather than reacting after incidents occur.

- **Maintenance Departments** gain insights into which routes and times experience mechanical versus operational incidents, enabling targeted preventive maintenance schedules.

- **Service Planning Teams** can adjust route schedules, identify high-risk periods, and implement service improvements based on historical incident patterns.

- **Executive Leadership** receives quantified, actionable intelligence to justify infrastructure investments and operational policy changes with data-driven ROI projections.

- **Passengers** ultimately benefit from reduced delays, more reliable service, and transparent communication about service reliability improvements.

## II. Business Objective

Our project aims to develop a machine learning classification model that can accurately predict transit incident types based on operational features such as route, time of day, delay duration, and location. By successfully classifying incidents, the TTC can:

- Improve operational efficiency by 10-15% through better resource allocation
- Reduce incident response times by pre-positioning appropriate resources
- Enable predictive maintenance by identifying patterns in mechanical incidents
- Enhance passenger communication with more accurate delay predictions and explanations
- Support data-driven investment decisions for infrastructure improvements

This classification model transforms raw incident data into actionable operational intelligence, moving transit management from reactive to proactive.


## III. Research Question

**Primary Classification Goal:** Can we classify transit incidents based on the type of incident using features such as route, time of day, delay duration, and location?

**Success Metrics:**
- Achieve classification accuracy of 75%+ across incident types
- Identify top 3 most predictive features for incident classification
- Provide actionable insights that could reduce incident misclassification by 20%+
- Deliver reproducible model that can be retrained with new data

## IV. Dataset

### Data Source
We will analyze TTC streetcar service delay data spanning 2014 to 2025, consisting of:<br>
(Source: [TTC Streetcar Delay Data historical CSV files](https://open.toronto.ca/dataset/ttc-streetcar-delay-data/) )

- 12 data files (mix of CSV and Excel formats)
- 2 additional files (readme with data files column descriptions and a code description file)
- Each file contains monthly tabs (12 tabs per year file)
- Comprehensive incident records across 11+ years of transit operations
- Estimated 100,000+ incident records (to be confirmed during consolidation)

****Key Features:
Based on the dataset and readme file, our data includes:****

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

## V. Risks & Unknowns 


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
