# UNSW-NB15 Data Preprocessing & Pipeline Architecture

## Project Overview
An optimized data preprocessing pipeline designed to handle the large-scale **UNSW-NB15 cybersecurity dataset** (~2.5 Million records) for machine learning workflows.

## Technical Highlights
- **Domain-Specific Imputation:** Handled protocol-specific missing values (`ct_ftp_cmd`, `ct_flw_http_mthd`, `is_ftp_login`) representing inactivity.
- **Memory Optimization:** Applied `OneHotEncoder` with sparse matrix structures to handle high-cardinality features efficiently.
- **Leakage Prevention & Scaling:** Excluded session identifiers (IPs/Ports) to prevent data leakage and normalized numerical values with `StandardScaler`.

## Tech Stack
Python, Pandas, NumPy, Scikit-Learn
