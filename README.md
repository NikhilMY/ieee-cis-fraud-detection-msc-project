# Financial Fraud Detection using Machine Learning: Comparing Models and Imbalance Techniques with Explainability

MSc Data Science and Artificial Intelligence — Final Project (ECS750P/ECS753P/ECS754P)
Queen Mary University of London

Author: Nikhil Malige Yathiraj (Student Number: 250424014)
Supervisor: Dr. Marc Roth

## What this is

This repository holds the supporting material for my MSc dissertation. The dissertation compares five classifiers (Logistic Regression, Random Forest, XGBoost, LightGBM, Isolation Forest) against three imbalance-handling strategies (SMOTE, random undersampling, class weighting) plus an untreated baseline, evaluated on the IEEE-CIS Fraud Detection dataset. The best-performing configuration is then explained using SHAP, stress-tested with a temporal train/test split, and assessed with a cost-sensitive business-value framework.

## What's in this repository

- `IEEE_CIS_Fraud_Detection_Pipeline.ipynb` — the full pipeline: data loading and merging, preprocessing, all 17 model/imbalance-strategy configurations, the temporal-split experiment, SHAP explainability, and the cost-sensitive evaluation. Every result reported in the dissertation is reproducible from this notebook.
- - `data/` — the smaller dataset files included directly in this repo: `train_identity.csv`, `test_identity.csv`.
- `figures/` — the output figures and result files produced by running the notebook (model comparison plots, SHAP summary/local plots, threshold tuning, cost comparison, risk tiers, plus `ieee_cis_risk_tiers.csv`), included so results can be checked without re-running the full pipeline.
- `README.md` — this file.

The two large transaction files (`train_transaction.csv`, ~652MB, and `test_transaction.csv`, ~585MB) are not included in this repository, since GitHub does not accept files over 100MB. They are hosted on Google Drive instead — see below.

## Getting the data

- `data/train_identity.csv` and `data/test_identity.csv` are already in this repository — no download needed.
- `train_transaction.csv` and `test_transaction.csv` are available here: **[https://drive.google.com/drive/folders/1C6lmhIK-Pj-7F_rjKpggXQOvwTqzE3ue?usp=sharing]**

Download the two transaction files from that link and place them in the `data/` folder alongside the two identity files before running the notebook.

## Running the notebook

This notebook was developed and run on Google Colab (Colab Pro, High-RAM runtime) because of the memory demands of the full dataset (590,540 rows x 434 columns after merging).

1. Open the notebook in Google Colab (or Jupyter, if you have enough RAM available — 25GB+ recommended).
2. Get all five data files together in the `data/` folder (the three already in this repo, plus the two large ones from the Google Drive link above).
3. If using Colab: upload the `data/` folder to your Google Drive, then update the `DATA_DIR` path near the top of the notebook (in the "Load and Merge the Dataset" section) to point to it.
4. If running locally in Jupyter instead of Colab: replace the `google.colab.drive.mount(...)` cell with a plain local path to the `data/` folder.
5. Run all cells in order from top to bottom. Training all 17 configurations end-to-end is compute-intensive and can take a while depending on the runtime tier available. Output figures will be written out — these are the same files already included in `figures/`.

Required libraries: `pandas`, `numpy`, `scikit-learn`, `xgboost`, `lightgbm`, `imbalanced-learn`, `shap`, `matplotlib`, `seaborn`.

## How this maps to the dissertation

- The 17-row results table in the notebook corresponds to Table I in the dissertation.
- The temporal-split experiment reproduces the PR-AUC drop from 0.6975 (random split) to 0.5105 (temporal split) reported in the Results/Discussion sections.
- The SHAP section produces both the global summary plot and the local waterfall explanation referenced in the Explainability section.
- The cost-sensitive evaluation section reproduces the business-value comparison (net cost in GBP across models/strategies) discussed in the Cost-Sensitive Evaluation section.

## Generative AI usage

Where and how Generative AI tools (Claude, Perplexity) were used during this project is documented in the signed Generative AI Usage Statement included in the appendix of the dissertation paper, per the EECS MSc Project handbook's submission requirements.

## Note on reproducibility

Random seeds are fixed (`RANDOM_STATE = 42`) throughout, but exact runtimes and minor floating-point differences may vary depending on library versions and hardware/runtime tier.
