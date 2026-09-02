# India-Asia-Export-Analytics-using-Python

India International Trade Data Analysis | Python **  Analysis of India’s country-wise international trade data using Python. The project combines multi-year trade datasets, performs data cleaning and aggregation, and analyzes country-wise and year-wise export and total trade trends to identify key markets, growth patterns, and trade insights.

# **Dataset Information**

Source: indiadataportal.com

Location: https://indiadataportal.com/p/export-trade-statistics/r/mci-tradestat_export_lfy-cn-mn-asi

Year/Timeline: 2015-2026

Domain: Trade Statistics

# India–Asia Export Analytics (2015–2025)

An end-to-end exploratory data analysis (EDA) project studying India's export trade with Asian countries between 2015 and 2025. The project cleans a raw ~5.5 million-row government trade dataset, engineers commodity and time-based features, and derives business-relevant insights on trade seasonality, top trading partners, and sector-level pricing behavior.

Built in Python on Google Colab, using Pandas, NumPy, Matplotlib, and Seaborn.

---

## Table of Contents

- [Dataset](#dataset)
- [Objectives](#objectives)
- [Tech Stack](#tech-stack)
- [Project Workflow](#project-workflow)
  - [Stage 1: Data Understanding](#stage-1-data-understanding)
  - [Stage 2: Data Cleaning & Feature Engineering](#stage-2-data-cleaning--feature-engineering)
  - [Stage 3: Statistical Analysis & Visualization](#stage-3-statistical-analysis--visualization)
- [Key Findings](#key-findings)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Dataset

- **Source:** [India Data Portal – Export Trade Statistics](https://indiadataportal.com/p/export-trade-statistics/r/mci-tradestat_export_lfy-cn-mn-asi)
- **Domain:** Commerce / International Trade
- **Time period:** 2015–2025
- **Size:** ~5.54 million rows × 15 columns

**Original columns:**

| Column | Description |
|---|---|
| `id` | Unique record identifier |
| `date` | Transaction/reporting date |
| `country_name`, `alpha_3_code`, `country_code` | Destination country details |
| `region_name`, `region_code` | Continental region (Asia) |
| `subregion_name`, `subregion_code` | Sub-region (e.g. Western Asia, Southern Asia) |
| `hs_code` | Harmonized System commodity code |
| `commodity` | Commodity description |
| `unit` | Unit of measurement (Kgs, Nos, Ltr, etc.) |
| `value_qt` | Quantity exported |
| `value_rs` | Export value in Indian Rupees |
| `value_dl` | Export value in US Dollars |

---

## Objectives

1. **Track trade trends** — Understand whether India's exports to Asia are growing, shrinking, or stable year over year.
2. **Compare country performance** — Identify top trading partners and emerging/rising markets.
3. **Evaluate subregion trade share** — Compare Western, Eastern, Southern, South-eastern, and Central Asia.
4. **Detect seasonality** — Find monthly/yearly patterns, spikes, and drops in export activity.
5. **Analyze pricing behavior** — Compare unit value realization (₹ per unit) across commodity sectors.
6. **Map commodity specialization** — See which subregions import which commodity categories most heavily.

---

## Tech Stack

- **Language:** Python 3
- **Data handling:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Environment:** Google Colab / Jupyter Notebook

---

## Project Workflow

### Stage 1: Data Understanding

- Loaded the raw CSV (`exports-to-asian-countries.csv`) from Google Drive
- Inspected shape (`5,541,809 rows × 15 columns`), data types, and summary statistics
- Checked for nulls (`unit`, `value_qt`, `value_rs`, `value_dl` had missing values) and duplicates (none found)

### Stage 2: Data Cleaning & Feature Engineering

- Standardized column names to uppercase and renamed `VALUE_QT` → `QUANTITY`, `VALUE_DL` → `VALUE_USD`
- Converted `DATE` to proper datetime format
- Cleaned inconsistent unit labels (e.g. `Kg` → `Kgs`, `Mts` → `Mtr`, `Cum` → `Cbm`) and filled missing units as `Unknown`
- Cleaned and normalized noisy `COMMODITY` text (expanded abbreviations like `Mlk` → `Milk`, `Pwdr` → `Powder`, `Nes` → `NES`)
- Engineered a new `COMMODITY_CATEGORY` feature by regex-classifying commodities into groups: Food & Agriculture, Textiles & Fabrics, Apparel & Garments, Pharmaceuticals, Plastics, Cosmetics & Personal Care, Leather & Travel Goods, Jewellery & Accessories, Packaging, Stationery, Medical & Healthcare Equipment, Wood & Wooden Products, Rubber & Tyres, Tobacco & Related Products, Paper & Paper Products, and Agriculture & Plantation
- Imputed missing numeric values (`QUANTITY`, `VALUE_RS`) using the median (robust to right-skew)
- Dropped redundant columns (`VALUE_USD`, `REGION_CODE`, `SUBREGION_CODE`)
- Extracted `MONTH` and `YEAR` from `DATE` for time-based analysis

### Stage 3: Statistical Analysis & Visualization

Each visualization is paired with a written business interpretation. Analyses performed:

- **Univariate:** Measures of central tendency (mean, median, mode) and dispersion (variance, standard deviation) for `QUANTITY` and `VALUE_RS`, with annotated distribution histograms
- **Bivariate:** Monthly total export value trend line (2015–2025); top 10 subregions by export revenue (bar chart)
- **Multivariate:** Top/bottom 10 countries by export value (pie charts); monthly seasonality heatmap by year; unit price distribution by commodity sector (boxplot); commodity-by-subregion specialization matrix (bubble scatter plot)

---

## Key Findings

**Seasonality**
- Exports peak in **March** (₹66.16M) and **December** (₹66.36M) — driven by India's financial year-end (March 31) and global holiday demand
- **April** is consistently the weakest month (₹55.40M), reflecting a post-March-rush reset
- **April 2020** shows a sharp, isolated drop tied to COVID-19 lockdowns
- **2021** was the strongest year overall, with December 2021 marking the single highest month in the 10-year dataset

**Trading Partners**
- **Western Asia** (UAE, Saudi Arabia, Türkiye) is India's largest export subregion at ₹247.8M, ahead of Eastern Asia (₹190.9M) and South-eastern Asia (₹159.4M)
- **UAE alone** accounts for 26.5% of top-10 country export value; UAE + China + Hong Kong together exceed 53%
- Central Asia is a minor market (~₹2.3M, well behind other subregions)
- Smallest export destinations include State of Palestine and Turkmenistan

**Pricing & Commodities**
- **Pharmaceuticals** show the widest unit-price spread (up to ~₹122/unit), reflecting a mix of generic and specialized high-value drugs
- **Wood & Wooden Products** and **Medical & Healthcare Equipment** also show long right-tail pricing, driven by niche high-value shipments
- **Plastics, Packaging, Stationery,** and **Agriculture & Plantation** are high-volume, low-unit-price sectors where revenue depends on quantity rather than per-unit value
- **Jewellery & Accessories** and **Cosmetics & Personal Care** show moderate, consistent pricing

## Future Improvements

- Add year-over-year growth rate calculations and CAGR by country/subregion
- Build an interactive dashboard (Plotly/Streamlit) for exploring trade data
- Incorporate forecasting (e.g. ARIMA/Prophet) to project future export trends
- Expand commodity classification with a supervised model instead of regex rules

---

## Author
Minu M
Analysis conducted as part of a Python data analytics project.

