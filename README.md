### Transit Incident Classifier: Predicting Incident Types from Route, Time, Delay, and Location
Data Science Institute - Cohort 7 - ML Team 12 Team Project

## Business case
This project aims to help the TTC improve service reliability and operational response by identifying and predicting the types of streetcar incidents that cause delays. By building a classification model that learns from historical data (2014–2025), the organization can better understand which factors, such as route, time of day, delay duration, or location, are most associated with different incident types. These insights can be used to optimize scheduling, allocate maintenance crews more effectively, and enhance coordination between transit control, operators, and emergency response teams.

From a business perspective, this analysis delivers data-driven decision support to reduce downtime, improve passenger satisfaction, and enhance resource efficiency. With accurate incident classification and trend analysis, TTC planners can prioritize investments (for example signal upgrades or track maintenance) where recurrent delays occur, and potentially anticipate high-risk periods or routes. Over time, this leads to lower operational costs, improved on-time performance metrics, and more transparent public reporting of service reliability, key factors in maintaining trust and ridership in Toronto’s transit system.


## Members
* Aman Kaushik
* Hossein Hooshmandi Safa
* Janice Wilson 
* Antonio Gao


## Project Overview 
-  [Purpose and Overview](#purpose-and-overview)
-  
-
-
-  



## Purpose and Overview
This repository delivers a supervised machine-learning solution that classifies transit incidents (e.g., mechanical, security, weather) using operational features such as route, time of day, delay duration, and location. The capability standardizes incident labeling, accelerates triage, and strengthens performance analytics, enabling more targeted interventions and clearer reporting.

# Problem Statement
Incident classification is frequently manual and inconsistent across operators and shifts. Variability in labels delays response coordination, inflates “Other/Unknown” categories, and limits root-cause analysis, trend detection, and stakeholder reporting.

# Objectives
* Accuracy & Consistency: Achieve high precision/recall in predicting incident type and reduce label variance.
* Operational Impact: Shorten time-to-classify to support faster routing of the appropriate response.
* Analytics Enablement: Deliver standardized labels that improve dashboards, KPI tracking, and root-cause analysis.

# Solution Overview
* Approach: Multi-class classification with a transparent baseline (Logistic Regression) and a tuned model (e.g., Random Forest / XGBoost).
* Features: Route/line identifiers, timestamp-derived signals (hour, day of week, peak/off-peak), delay minutes, location text/stop metadata.
* Outputs: Top-1 prediction (optional Top-3) with confidence; feature importance for explainability; confusion matrix and class-level metrics.

## Data
Source: TTC Streetcar Delay Data [historical CSV files](https://open.toronto.ca/dataset/ttc-streetcar-delay-data/)
