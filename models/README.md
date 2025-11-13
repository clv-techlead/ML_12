# Models Folder – ML_12 TTC Streetcar Delays Classification Project

## Overview

The `models/` directory contains all **machine-learning notebooks** used to build and evaluate
classification models for TTC streetcar delays.

These notebooks load the feature-engineered dataset, create compact modeling features,
train several classifiers, and export evaluation figures and tables to the `reports/`
folder for the final presentation.

---

## Files in This Folder

```text
models/
│
├── ttc_modeling.ipynb
│     End-to-end modeling pipeline:
│       - Loads TTC_Feature_Engineered_2014_2025.csv
│       - Builds compact numeric + categorical feature set
│       - Trains 3 classifiers (LogReg, Random Forest, Gradient Boosting)
│       - Uses time-aware 80/10/10 train/validation/test split
│       - Saves confusion matrices, feature importance plots,
│         per-class performance charts, and model comparison figure
│
├── model.ipynb
│     Earlier / exploratory modeling notebook
│     (kept for reference; ttc_modeling.ipynb is the final version)
│
├── TTC_Streetcar_Delays_2014_2025.csv
│     Intermediate combined file produced during development.
│     Final, cleaned data lives in data/processed/ and data root.
│
└── README.md
      This documentation file
Main Notebook: ttc_modeling.ipynb
Goal
Build an end-to-end, reproducible modeling pipeline that:

Loads the final feature-engineered dataset

Creates compact time, route, and location features

Trains multiple classification models

Evaluates them using time-based splits (no leakage)

Exports all required plots and CSVs to reports/ for the project report & slides

Target Variable
The notebook supports multiple targets via the TARGET parameter:

python
Copy code
TARGET = "delay_bin"        # default: severity classification (Low / Medium / High / Severe)
# or:
# TARGET = "incident_type"  # full incident text label (collapsed to incident_slim)
# TARGET = "incident_slim"  # grouped incident categories
Set TARGET at the top of the notebook to switch between:

delay_bin – 4-class delay severity (Low, Medium, High, Severe)

incident_type / incident_slim – incident-type classification problems

readme file for models folder
