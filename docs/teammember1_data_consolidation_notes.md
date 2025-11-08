# TTC Streetcar Delay Data Consolidation Review (2014–2025)

## Overview
This document summarizes the data integration and preprocessing steps used to consolidate all TTC Streetcar Delay records (2014–2025) into a single, standardized dataset.  
The objective was to merge multiple yearly Excel sheets (2014–2024) and a CSV file (2025) into a consistent structure suitable for further feature engineering and machine-learning modeling.

---

## Input Sources

| Year Range | File Type | Structure | Notes |
|-------------|------------|------------|-------|
| **2014–2024** | `.xlsx` | 12 sheets per file (one per month) | Columns: `Report Date`, `Route`, `Time`, `Day`, `Location`, `Incident`, `Min Delay`, `Min Gap`, `Direction`, `Vehicle` |
| **2025** | `.csv` | Single file | Columns: `_id`, `Date`, `Line`, `Time`, `Day`, `Station`, `Code`, `Min Delay`, `Min Gap`, `Bound`, `Vehicle` |

All files were stored under the `data/` directory.

---

## Processing Workflow

### File Discovery and Loading
- The script uses `glob` to detect both `.xlsx` and `.csv` files in the `data` folder.
- Each Excel file is read with the **OpenPyXL** engine and iterates through all monthly sheets.
- Each sheet is tagged with its source filename and month for traceability.
- The CSV file for 2025 is read independently and aligned with the same schema.

### Schema Standardization
- Column names are cleaned (`lowercase`, `underscored`, trimmed).
- Duplicate column headers are removed.
- Excel columns are renamed to match CSV fields using this map:

  ```python
  rename_map = {
      "report_date": "date",
      "route": "line",
      "location": "station",
      "incident": "code",
      "direction": "bound"
  }

## Structural Alignment
A common schema was defined:

sql
Copy code
date, line, time, day, station, code, min_delay, min_gap, bound, vehicle
Both datasets were subset and ordered according to this schema before merging.

## Data Merging
pd.concat() combined all years (2014–2025) into a single DataFrame.

Columns were revalidated for uniqueness before concatenation.

## Data Cleaning and Type Conversion
Dates: parsed with pd.to_datetime() (invalid formats coerced to NaT).

Time: custom parser handles both 12-hour (6:31 AM) and 24-hour (20:05) formats.

Hour: extracted as numeric (0–23) for modeling.

Delays: min_delay and min_gap converted to numeric and NaNs replaced with 0.

Rows with missing critical fields (line, code, station) were dropped.

## Output
The final dataset was saved as:

kotlin
Copy code
data/TTC_Streetcar_Delays_2014_2025.csv
It now contains a unified schema across all years and is ready for downstream feature engineering and modeling.

## Summary Statistics (Post-Merge)
Metric	Count
Total Records	~60–70k (depending on source files)
Unique Routes	30+
Unique Incident Codes	100+ (before simplification)
Time Span	2014 – 2025
Output Columns	10 standardized fields + derived hour

## Key Improvements
Standardized date/time across inconsistent historical files.

Unified all column names and structures across formats.

Consolidated >10 years of TTC delay records into one clean, analysis-ready file.

Extracted hour feature for temporal modeling.

Ensured numeric consistency for delay and gap durations.
## Next Steps
Perform data cleaning and normalization (already implemented in a separate script).

Conduct exploratory data analysis (EDA) and feature engineering for predictive modeling.

Use the merged file as the foundation for:

Delay cause classification models (Random Forest, XGBoost)

Time-series delay forecasting

Visualization dashboards (hourly, route-wise, incident-wise trends)

Final Output File:
data/TTC_Streetcar_Delays_2014_2025.csv
Purpose: Single, high-quality dataset ready for machine-learning and operational analytics.Record notes about process and how you handled and data issues, any potential risks suggested workarounds etc
