# UNSW-NB15 Network Intrusion Detection & ML Pipeline

## Project Overview
This project implements an end-to-end machine learning pipeline for network traffic classification using the large-scale **UNSW-NB15 dataset**. The goal is to accurately distinguish between normal background traffic and network attacks (binary classification: `Label`).

## What I Did (Step-by-Step)
1. **Data Loading & Merging:** Combined multiple CSV split files of the UNSW-NB15 dataset and dynamically assigned official feature names from the dataset description file.
2. **Data Cleaning & Leakage Prevention:** 
   - Dropped identifier columns (`srcip`, `dstip`, `sport`, `dsport`), timestamps (`Stime`, `Ltime`), and the explicit attack category (`attack_cat`) to completely eliminate data leakage and prevent the model from "cheating."
   - Cleaned target missing values and filtered out invalid rows.
3. **Domain-Specific Imputation:** Handled missing values in specialized command/login features (`ct_ftp_cmd`, `ct_flw_http_mthd`, `is_ftp_login`) by filling them with `0`, reflecting true network inactivity.
4. **Pipeline & Preprocessing Architecture (`ColumnTransformer`):**
   - **Numerical Features:** Standardized using `StandardScaler` to bring all features to a common scale.
   - **Categorical Features:** Encoded using `OneHotEncoder` (`drop='first'`, `handle_unknown='ignore'`) to safely process protocols and states without risking test-set errors.
5. **Model Training & Evaluation:**
   - Built a robust Scikit-Learn `Pipeline` combining the preprocessor and a `RandomForestClassifier` (`n_estimators=100`, `max_depth=20`).
   - Performed proper data splitting *before* any transformation to ensure rigorous evaluation.

## Performance Results
Tested on an unseen test subset, the Random Forest model achieved outstanding performance:
- **Accuracy:** `99.41%`
- **ROC-AUC Score:** `0.9998`
- **F1-Score (Attack Class):** `0.9787`

## Tech Stack
- **Python**
- **Pandas & NumPy** (Data manipulation)
- **Scikit-Learn** (Preprocessing pipelines, evaluation metrics, and Random Forest classifier)
