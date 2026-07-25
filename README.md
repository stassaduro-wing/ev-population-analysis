# Washington State Electric Vehicle Population Analysis

Full analyst workflow on the Washington State Electric Vehicle Population dataset: data cleaning, exploratory data analysis, spatial analysis, and data-driven conclusions.

**Stack:** PostgreSQL 18 (pgAdmin 4) for data cleaning and storage · Python (pandas, Plotly, NumPy) for analysis and visualization in Jupyter.

📊 **[View the full notebook with rendered charts (nbviewer)](https://nbviewer.org/github/stassaduro-wing/ev-population-analysis/blob/main/notebooks/eda.ipynb)**
*(GitHub's built-in preview doesn't render large interactive Plotly charts — use the nbviewer link above for the full experience.)*

## Repository Structure

├── data/
│ ├── Electric_Vehicle_Population_Data_changed(in).csv # raw source file
│ ├── ev_popul_dirty.csv # staging table export (TEXT columns)
│ └── ev_popul_clean.csv # final cleaned & typed dataset
├── notebooks/
│ ├── eda.ipynb # main analysis: EDA, spatial analysis, hypotheses, data quality notes
│ ├── teslafix.ipynb # standalone fix for corrupted "TESLA" byte sequence
│ └── quotefix.ipynb # standalone fix for broken CSV quote escaping
└── README.md

## Data Source

Raw dataset: [Electric Vehicle Population Data](https://catalog.data.gov/dataset/electric-vehicle-population-data) — publicly available from the Washington State Department of Licensing.

## Project Summary

The raw dataset (~250,000 rows) required significant cleaning before analysis, including fixing corrupted UTF-8 byte sequences, broken CSV quote escaping, invalid values, and type casting. See `notebooks/eda.ipynb` for the full documented methodology and `notebooks/teslafix.ipynb` / `notebooks/quotefix.ipynb` for the standalone byte-level fixes applied to the raw file.

The analysis covers:
- **Data Understanding & Cleaning** — full methodology with SQL and Python code
- **Exploratory Data Analysis** — registration trends by year, manufacturer/model breakdown, BEV vs PHEV adoption, electric range distribution, CAFV eligibility, price distribution
- **Spatial Analysis** — county-level breakdown and a registration density heatmap
- **Hypotheses & Conclusions** — data-driven takeaways
- **Data Quality Details** — documented anomalies and edge cases found during cleaning

## Key Findings

- Tesla dominates the Washington State EV market; Model Y and Model 3 alone account for **35.6%** of all registered EVs.
- The share of fully electric vehicles (BEV) has grown faster than plug-in hybrids (PHEV) over time.
- EV adoption is heavily concentrated in King County (Greater Seattle area), correlating with population density and income levels.
- 60.7% of records have an "unknown" CAFV eligibility status, closely tied to unresearched electric range values for newer/rarer models — a systemic gap in the state's verification process rather than a data quality issue.
- Base MSRP is populated for only 1.28% of records; where present, pricing follows a typical long-tail distribution (e.g. a Porsche 918 Spyder at $845,000).

## How to Reproduce

1. Load the raw CSV into a PostgreSQL staging table (see `eda.ipynb` for schema and cleaning steps).
2. Run `teslafix.ipynb` and `quotefix.ipynb` to resolve byte-level corruption in the raw file before import.
3. Run the cleaning SQL documented in `eda.ipynb` to produce the final typed table.
4. Run `eda.ipynb` end-to-end (`Kernel → Restart & Run All`) to reproduce the analysis and charts.

**Requirements:** `pandas`, `sqlalchemy`, `psycopg2-binary`, `plotly`, `numpy`
