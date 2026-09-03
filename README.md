# **Trade Flows Between India and Asia: Statistical & Business Insights | Python | 2015–2025**

An end-to-end exploratory data analysis (EDA) project studying India's export trade with Asian countries between 2015 and 2025. The project cleans a raw ~5.5 million-row government trade dataset, engineers commodity and time-based features, and derives business-relevant insights on trade seasonality, top trading partners, and sector-level pricing behavior.

Built in Python on Google Colab, using Pandas, NumPy, Matplotlib, and Seaborn.

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

**Track Trade and Export Trends Over the Years**

Study how India's total trade and exports have changed from year to year, in order to understand whether trade is growing, shrinking, or staying steady over time.

**Objective 1:** Track Trade and Export Trends Over Time
Analyze how India's total export value to Asian countries has changed month-by-month and year-by-year (2015–2025) to identify overall growth, decline, or stability in trade.

**Objective 2:** Identify Top Subregions by Export Revenue
Determine which Asian subregions (Western Asia, Eastern Asia, South-eastern Asia, Southern Asia, Central Asia) generate the highest export revenue for India, and quantify the gap between top and bottom performers.

**Objective 3:** Evaluate Geographic Trade Share Across Countries
Identify India's top 10 and bottom 10 trading partner countries by export value, and assess how concentrated or diversified India's export revenue is across its Asian partners.

**Objective 4:** Uncover Monthly Trade Seasonality Across Years
Examine seasonal patterns in export revenue using a year-by-month heatmap to detect recurring peaks (e.g., financial year-end surges) and anomalies (e.g., pandemic-driven drops).

**Objective 5:** Compare Unit Value Realization (Value/Quantity) Across Sectors
Calculate and compare price-per-unit realization across commodity categories to distinguish high-margin, low-volume sectors from high-volume, low-margin bulk sectors.

**Objective 6:** Analyze Commodity Specialization Across Asian Subregions
Map which commodity categories dominate exports to each Asian subregion, revealing regional specialization patterns in India's trade basket.

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

Central Tendency & Dispersion

-	Quantity: Mean 54,876.85 | Median 3.00 | Mode 0.00 → strongly right-skewed
-	Value_RS: Mean 130.56 | Median 2.82 | Mode 0.00 → strongly right-skewed
-	Quantity Std Dev: 3,926,595.81 | Variance: ~15.4 trillion
-	Value_RS Std Dev: 3,051.99 | Variance: ~9.3 million
<img width="1222" height="582" alt="Screenshot 2026-09-02 191727" src="https://github.com/user-attachments/assets/fbfb4abf-c1d9-495d-9cc4-087f02fcd3e3" />

<img width="1201" height="492" alt="Screenshot 2026-09-02 191739" src="https://github.com/user-attachments/assets/c3579f09-e3a6-49a2-85fe-5def9b280309" />

## Key Findings

**Seasonality**
- Exports peak in **March** (₹66.16M) and **December** (₹66.36M) — driven by India's financial year-end (March 31) and global holiday demand
- **April** is consistently the weakest month (₹55.40M), reflecting a post-March-rush reset
- **April 2020** shows a sharp, isolated drop tied to COVID-19 lockdowns
- **2021** was the strongest year overall, with December 2021 marking the single highest month in the 10-year dataset
<img width="802" height="330" alt="Screenshot 2026-09-02 140725" src="https://github.com/user-attachments/assets/ed6d0048-4293-462e-8ecc-0b034977d970" />

<img width="1121" height="562" alt="Screenshot 2026-09-02 150102" src="https://github.com/user-attachments/assets/5a652f42-b4ab-45bd-9330-a06bf91a6fad" />


**Trading Partners**
- **Western Asia** (UAE, Saudi Arabia, Türkiye) is India's largest export subregion at ₹247.8M, ahead of Eastern Asia (₹190.9M) and South-eastern Asia (₹159.4M)
- **UAE alone** accounts for 26.5% of top-10 country export value; UAE + China + Hong Kong together exceed 53%
- Central Asia is a minor market (~₹2.3M, well behind other subregions)
- Smallest export destinations include State of Palestine and Turkmenistan
<img width="1075" height="556" alt="Screenshot 2026-09-02 142538" src="https://github.com/user-attachments/assets/b840682b-1482-45b4-a40d-033576a04903" />

<img width="1758" height="675" alt="Screenshot 2026-09-02 142854" src="https://github.com/user-attachments/assets/92e9e861-65ea-49b8-8fa4-48b8cbb08924" />


**Pricing & Commodities**
- **Pharmaceuticals** show the widest unit-price spread (up to ~₹122/unit), reflecting a mix of generic and specialized high-value drugs
- **Wood & Wooden Products** and **Medical & Healthcare Equipment** also show long right-tail pricing, driven by niche high-value shipments
- **Plastics, Packaging, Stationery,** and **Agriculture & Plantation** are high-volume, low-unit-price sectors where revenue depends on quantity rather than per-unit value
- **Jewellery & Accessories** and **Cosmetics & Personal Care** show moderate, consistent pricing

<img width="1427" height="557" alt="Screenshot 2026-09-02 150403" src="https://github.com/user-attachments/assets/a653241e-583b-40af-8ddc-51774ecf607b" />

 **Commodity Specialization by Subregion**
 
•	Cosmetics & Personal Care dominates exports, contributing the majority of revenue across Eastern, South-eastern, Southern, and Western Asia.

•	Western Asia is the largest overall market, with the biggest share in Cosmetics & Personal Care, making it the strongest subregion-commodity pairing.

•	India exports all 10 commodity categories to all 5 subregions, showing broad market presence despite revenue concentration in consumer care products.

<img width="1242" height="602" alt="Screenshot 2026-09-02 153020" src="https://github.com/user-attachments/assets/05b4f5b8-787b-4a9c-900b-e2fa0236b3d4" />

**Four-Layer Analytics Interpretation**

- Descriptive — What Happened: The analysis confirms that Western Asia dominates India’s export landscape, accounting for the largest share of trade revenue. Within commodities, Cosmetics & Personal Care clearly leads, dwarfing other categories in both transaction count and value. This establishes the baseline picture: India’s exports are concentrated in one sector and one region. 

- Diagnostic — Why It Happened: The recurring peaks in March and December are explained by fiscal cycles (March year-end targets) and global consumer demand (December holiday season). Meanwhile, Central Asia consistently underperforms due to limited market size and weaker trade corridors. These diagnostic insights highlight structural drivers behind the observed patterns. 

- Predictive — What Will Happen: Given the skewed distributions and high variance, the dataset suggests that mega-deals will continue to dominate overall revenue. A handful of large transactions will disproportionately influence averages, meaning future trade performance will remain vulnerable to fluctuations in these big-ticket deals. 

- Prescriptive — What Should Be Done: To mitigate risks, India should diversify into underpenetrated subregions such as Northern and Eastern Asia. Policymakers and exporters must protect single-category corridors (e.g., cosmetics, pharmaceuticals) from supply chain shocks. Additionally, logistics segmentation should be strengthened to handle high-value, low-volume shipments differently from bulk, low-margin goods. 

**Business Recommendations** 

- Expand into Northern & Eastern Asia: Reduce reliance on Western Asia by building stronger trade corridors with underpenetrated regions. 

- Strengthen supply chain protections: Safeguard narrow corridors like cosmetics and pharmaceuticals against disruptions by diversifying suppliers and logistics routes. 

- Segment logistics operations: Route high-value, low-volume shipments through premium channels, while bulk goods continue via cost-efficient freight. 

- Automate anomaly detection: Implement real-time monitoring systems to flag sudden shocks (like COVID-19) and enable faster response. 

**Conclusion**

India’s exports to Asia are structurally concentrated in Cosmetics & Personal Care and Western Asia, creating both opportunities and risks. While the export basket is diversified across categories, revenue is skewed by a few large transactions. This concentration makes trade performance highly sensitive to mega-deals and regional demand cycles. To ensure resilience, India must strategically diversify markets, protect vulnerable corridors, and modernize logistics and monitoring systems. Doing so will strengthen India’s position in Asia and reduce exposure to external shocks. 
## Author
Minu M
Data Analyst

