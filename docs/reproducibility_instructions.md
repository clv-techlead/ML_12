# Reproducibility Instructions - TTC Streetcar Delays Classification

## Prerequisites

To ensure full reproducibility of this project, follow the steps below.

-   **Python Version**: 3.9 or higher
-   **Operating System**: Windows, macOS, or Linux
-   **Hardware**: 4GB RAM minimum, 500MB disk space
-   **Software**: Git, Python package manager (`pip`)

## Step-by-Step Instructions

###1. Clone the Repository
```bash
git clone [repository-url]
cd ttc-incident-classification
```

### 2. Setup Virtual Environment & Install Dependencies
```bash
python -m venv venv
# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

pip install -r requirements.txt
```

### 3. Download Raw Data
Place the 12 TTC delay data files (e.g., `ttc_delays_2014.xlsx`, `ttc_delays_2015.xlsx`, ..., `ttc_delays_2024.xlsx`) into the `data/raw/` directory within the cloned repository.

### 4. Run the Full Analysis Pipeline

This project's entire analysis pipeline (data consolidation, feature engineering, and model training/evaluation) can be executed. Choose one of the following options:

**Option A: Via Jupyter Notebooks (Recommended for interactive exploration)**

To run interactively and see all steps:
```bash
jupyter notebook
```
Then, open and run the notebooks in the following order:
-   `experiments/01_eda.ipynb` (for EDA and Feature Engineering)
-   `experiments/02_modeling.ipynb` (for Model Development & Evaluation)

**Option B: Via Python Scripts (Recommended for automated runs)**

Execute the main scripts sequentially:

```bash
# Run data consolidation and feature engineering
python src/data_consolidation.py

# Run model training and evaluation
python src/train_models.py
```

## Expected Outputs

After successfully running the pipeline, you should find:
-   Consolidated and feature-engineered datasets in `data/processed/`.
-   Trained models saved in the `models/` folder.
-   Results and evaluation metrics in `reports/model_comparison.csv`.
-   Evaluation visualizations (e.g., confusion matrices, feature importance plots) in `reports/figures/model_results/`.

## Expected Results

Running the full pipeline should produce:
-   Final model accuracy: [X.XX]% (±0.02)
-   F1-score (weighted): [X.XX] (±0.02)
-   Total runtime: [X]-[Y] minutes (may vary based on hardware)

## Troubleshooting

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
