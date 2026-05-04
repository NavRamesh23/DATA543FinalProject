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
| `notebook1_eda.ipynb` | Exploratory analysis — top tactics, vendors, CWE types, and yearly trends |
| `notebook2_logistic_regression.ipynb` | Logistic Regression model to classify CVEs by ATT&CK tactic |
| `notebook3_random_forest.ipynb` | Random Forest classifier — compared against Logistic Regression |
| `notebook4_arima.ipynb` | ARIMA time series forecast of monthly KEV additions (next 12 months) |
| `notebook5_monte_carlo.ipynb` | Monte Carlo simulation estimating annual financial cyber risk exposure |

---

## Data Sources

- **sample.xlsx** — CISA KEV catalog with ATT&CK mappings (1,539 entries), sheet: `KEV Enriched`
- **cve_epss.csv** — CVSS base scores, impact scores, and EPSS exploit probability scores
- Financial baseline: IBM Cost of a Data Breach Report 2025 ($4.44M global average)

---

## Key Results

- **Logistic Regression** achieved **93.8%** accuracy predicting ATT&CK tactics across 4 classes
- **Random Forest** achieved **96.9%** accuracy — outperforming LR on the same data and split
- Majority class baseline (always guessing Initial Access) would score **59.0%** — both models significantly exceed this
- Initial Access is the most common tactic, making up ~58% of all KEV entries
- **ARIMA(2,1,2)** forecast predicts approximately **[X]** new KEV entries over the next 12 months
- **Monte Carlo simulation** (10,000 runs) estimates annual cyber exposure:
  - Best case (10th pct): **$56.84M**
  - Expected (mean): **$71.78M**
  - Worst case (90th pct): **$86.94M**

---

## How to Run

1. Open any notebook in [Google Colab](https://colab.research.google.com/)
2. Upload `sample.xlsx` when prompted (Notebooks 1–4), using sheet `KEV Enriched`
3. Upload both `sample.xlsx` and `cve_epss.csv` when prompted (Notebook 5)
4. Run all cells in order from top to bottom

No local setup needed — all dependencies install automatically in the first cell.

---

## Models

| Model | Accuracy | Classes | Notes |
|-------|----------|---------|-------|
| Logistic Regression | 93.8% | 4 ATT&CK tactics | Requires feature scaling |
| Random Forest | 96.9% | 4 ATT&CK tactics | No scaling needed; provides feature importance |
| Majority class baseline | 59.0% | — | Always predicts Initial Access |

Both models used: Platform type, CWE category, and Year added as features.
Train/test split: 80/20, random state 42, stratified by tactic class.

---

## Output Files

All generated charts and CSV files are downloaded directly from Colab after each cell runs:

| File | Description |
|------|-------------|
| `eda_tactics.png` | Top 10 ATT&CK tactics by CVE count |
| `eda_years.png` | KEV entries added per year |
| `eda_vendors.png` | Top 10 most exploited vendors |
| `eda_cwes.png` | Top 10 CWE vulnerability types |
| `logreg_confusion.png` | Logistic Regression confusion matrix |
| `logreg_probabilities.png` | Avg predicted probability per tactic |
| `logreg_probabilities.csv` | Raw LR probability scores per CVE |
| `model_comparison.png` | LR vs RF accuracy bar chart |
| `rf_confusion.png` | Random Forest confusion matrix |
| `rf_feature_importance.png` | Top features driving RF predictions |
| `rf_probabilities.csv` | RF probability scores per CVE |
| `kev_historical.png` | Historical monthly KEV additions |
| `kev_forecast.png` | ARIMA 12-month forecast with 90% confidence interval |
| `financial_risk_distribution.png` | Per-CVE financial risk score distribution |
| `risk_by_tactic.png` | Avg financial risk by ATT&CK tactic |
| `monte_carlo_final.png` | Monte Carlo annual cost simulation results |

---

## Tools & Libraries

Python · pandas · scikit-learn · statsmodels · matplotlib · numpy · openpyxl

---

## Notes on Class Imbalance

Initial Access makes up ~58% of the dataset, which inflates overall accuracy scores.
A model that always guesses Initial Access would still hit 59% — the majority class floor.
Both models beat this by a significant margin, but results should be interpreted with
this imbalance in mind. Future work could apply SMOTE or class weighting to get a
fairer evaluation across all 4 tactic classes.
