Readme for data folder
Data Folder : ML_12 TTC Streetcar Delays Classification Project

Overview

The data/ directory contains all datasets used in the TTC Streetcar Delays Classification Project (2014–2025).

The raw dataset was obtained from the City of Toronto’s Open Data Portal:
https://open.toronto.ca/dataset/ttc-streetcar-delay-data/

Folder Structure

data/
│
├── raw/                         # Original TTC data (downloaded from Open Toronto)
│   ├── TTC_Streetcar_Delays_2014_2025.csv
│   └── *.xlsx, *.csv (yearly/monthly files)
│
├── processed/                   # Cleaned and standardized datasets
│   └── TTC_Streetcar_Delays_Cleaned_2014_2025.csv
│
├── TTC_Feature_Engineered_2014_2025.csv   # Final dataset for modeling
│
└── README.md                    # Documentation for this data folder


Data Source & Collection:

Source:

Toronto Open Data Portal

Dataset:

TTC Streetcar Delay Data (2014–2025)

URL:

🔗 https://open.toronto.ca/dataset/ttc-streetcar-delay-data/

Publisher:

Toronto Transit Commission (TTC)

License:

Open Government License – Toronto
(Free for public and academic use)

Dataset Description:

The TTC Streetcar Delay dataset contains detailed operational records of Toronto’s streetcar system from 2014 to 2025. Each record represents a delay or service disruption event logged by TTC operations.

Included Fields:

Date & Time – when the delay occurred

Route Number – streetcar line involved

Location / Intersection – where the incident occurred

Incident Type – root cause (Mechanical, Collision, Overhead, etc.)

Delay Duration (min) – number of minutes delayed

Direction (bound) – EB / WB / NB / SB

Vehicle Number – identifier for involved streetcar

This data forms the foundation for our EDA, feature engineering, and incident-type classification model.

How to Load the Final Dataset:

import pandas as pd

# Load the feature-engineered dataset used for modeling
df = pd.read_csv("data/TTC_Feature_Engineered_2014_2025.csv")

print(df.shape)   # prints number of rows and columns
df.head()         # preview the first few rows
