# EDA Findings – Team Member 2 (Aman Kaushik)

## Key Patterns Discovered
- Verified and cleaned the consolidated dataset (2014–2025) shared by Hossein.
- Found missing values mainly in `incident`, `route`, and `location` columns — imputed appropriately.
- Majority of incidents occurred between **7–9 AM** and **4–7 PM**, indicating strong rush-hour impact.
- Yearly analysis shows delay frequency increased after 2020, peaking around 2023.
- Weekend operations have fewer total incidents but a higher proportion of long delays.


## Incident Type Distribution
- Mechanical and General Delay incidents dominate, together accounting for ~60% of total delays.
- Security, Overhead, and Collision categories appear less frequently (<10% each).
- This class imbalance should be considered in the model training phase.


## Time-related Patterns
- Monthly pattern shows consistent peaks during winter months (Jan–Feb) due to weather.
- Weekly pattern reveals more incidents on weekdays, particularly Monday and Friday.
- Hourly trend confirms morning and evening rush-hour concentration.
- Annual trend demonstrates an upward trajectory in total delays post-2020, possibly due to service adjustments and ridership recovery.


## Route Patterns
- Routes such as **504 King**, **501 Queen**, and **505 Dundas** account for the highest incident volumes.
- Several high-delay intersections (Broadview, Dundas West, Bathurst) are repeated hotspots.
- These routes show both operational (traffic-related) and mechanical incident overlap.


## Visualizations Created
1. **Top 20 Incident Type Distribution:** Bar chart showing frequency and percentage labels.  
2. **Yearly Delay Trends:** Line chart showing total incidents per year (2014–2025).  
3. **Top 10 Locations by Frequency:** Horizontal bar plot of major delay-prone locations.  
4. **Monthly Pattern:** Bar chart showing seasonal distribution of incidents.  
5. **Delay Duration Distribution:** Histogram showing concentration around 10–12 minutes.

## Feature Engineering Summary
- Added time-based variables: `year`, `month`, `day`, `hour`, `is_weekend`
- Created `delay_category` (Low, Medium, High) from delay duration.
- Encoded categorical columns (`incident`, `route`, `location`) for modeling readiness.
- Replaced missing values: numeric with `0`, categorical with `"Unknown"`.
- Prepared dataset (`TTC_Streetcar_Delays_Cleaned_2014_2025.csv`) for classification.


## Implications for Modeling Step
-
- Dataset is finalized and ready for Antonio (Member 3) to begin model training and optimization.
