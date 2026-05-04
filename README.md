# DATA543 Final — Cybersecurity Risk Analysis

A data-driven cybersecurity risk management project using the CISA Known Exploited
Vulnerabilities (KEV) catalog and MITRE ATT&CK framework to classify exploitation
tactics, forecast future vulnerability trends, and estimate financial exposure.

---

## Project Overview

This project analyzes 1,500+ real-world CVEs from the CISA KEV catalog to answer:
- Which ATT&CK tactics are most common in actively exploited vulnerabilities?
- Can we predict which tactic a CVE belongs to based on its features?
- How many new CVEs will be added to the KEV catalog over the next 12 months?
- What is the estimated annual financial impact of these vulnerabilities?

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `notebooks/notebook1_eda.ipynb` | Exploratory analysis — top tactics, vendors, CWE types, and yearly trends |
| `notebooks/notebook2_logistic_regression.ipynb` | Logistic Regression model to classify CVEs by ATT&CK tactic |
| `notebooks/notebook3_random_forest.ipynb` | Random Forest classifier — compared against Logistic Regression |
| `notebooks/notebook4_arima.ipynb` | ARIMA time series forecast of monthly KEV additions (next 12 months) |
| `notebooks/notebook5_monte_carlo.ipynb` | Monte Carlo simulation estimating annual financial cyber risk exposure |

---

## Data Sources

- **sample.xlsx** — CISA KEV catalog with ATT&CK mappings (1,539 entries)
- **cve_epss.csv** — CVSS base scores, impact scores, and EPSS exploit probability scores
- Financial baseline: IBM Cost of a Data Breach Report 2025 ($4.44M global average)

---

## Key Results

- Random Forest and Logistic Regression both achieved ~99.5% accuracy predicting ATT&CK tactics
- ARIMA forecast predicts approximately **[X]** new KEV entries over the next 12 months
- Monte Carlo simulation (10,000 runs) estimates annual cyber exposure between **$[X]M – $[X]M**

---

## How to Run

1. Open any notebook in [Google Colab](https://colab.research.google.com/)
2. Upload `sample.xlsx` when prompted (Notebooks 1–4)
3. Upload both `sample.xlsx` and `cve_epss.csv` when prompted (Notebook 5)
4. Run all cells in order from top to bottom

No local setup needed — all dependencies install automatically in the first cell.

---

## Output Files

All generated charts and CSV files are saved in the `outputs/` folder:

| File | Description |
|------|-------------|
| `eda_tactics.png` | Top 10 ATT&CK tactics by CVE count |
| `eda_years.png` | KEV entries added per year |
| `eda_vendors.png` | Top 10 most exploited vendors |
| `eda_cwes.png` | Top 10 CWE vulnerability types |
| `logreg_confusion.png` | Logistic Regression confusion matrix |
| `logreg_probabilities.png` | Avg predicted probability per tactic |
| `logreg_probabilities.csv` | Raw probability scores per CVE |
| `model_comparison.png` | LR vs RF accuracy bar chart |
| `rf_confusion.png` | Random Forest confusion matrix |
| `rf_feature_importance.png` | Top features driving RF predictions |
| `rf_probabilities.csv` | RF probability scores per CVE |
| `kev_historical.png` | Historical monthly KEV additions |
| `kev_forecast.png` | ARIMA 12-month forecast with confidence interval |
| `financial_risk_distribution.png` | Per-CVE financial risk distribution |
| `risk_by_tactic.png` | Avg financial risk by ATT&CK tactic |
| `monte_carlo_final.png` | Monte Carlo annual cost simulation results |

---

## Tools & Libraries

Python · pandas · scikit-learn · statsmodels · matplotlib · numpy

---

## Dashboard

An interactive HTML summary is available in `dashboard.html` — open it directly in any browser, no setup required.
