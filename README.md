# Bay Area Home Price Trends – Capstone Project  
**Author:** Sourabh Bhalerao  
**Program:** Professional Certificate in Machine Learning & Artificial Intelligence  
**Final Submission – Module 24**

---

## 📌 Executive Summary

San Jose sits at the center of the Bay Area’s dynamic housing market. This project examines **how home prices vary across ZIP codes**, how they **cluster into economic segments**, and whether **machine learning models can accurately predict ZIP-level home values**.

Using Zillow ZHVI, Redfin market activity data, and macroeconomic indicators from FRED, we:

- Segmented San Jose ZIP codes into **Entry-Level**, **Mid-Market**, and **High-Price/Luxury** clusters.
- Compared San Jose against the broader Bay Area market.
- Built and evaluated predictive models **with** and **without** lagged price features.
- Produced actionable recommendations for buyers, sellers, investors, and policymakers.

---

## 🎯 Research Question

**How can machine learning models accurately predict housing prices in San Jose while uncovering distinct market segments that behave differently under changing economic and local conditions?**

---

## 🧠 Key Findings

### **1. Market Segmentation**
San Jose ZIP codes naturally fall into **three economic tiers**:
- **Entry-Level** – lower ZHVI, higher turnover  
- **Mid-Market** – stable, moderate pricing  
- **High-Price / Luxury** – highest ZHVI, low supply  

On a Bay Area–wide basis, San Jose mostly sits in the **mid-market and luxury ranges**, confirming its premium status within the region.

---

### **2. Predictive Modeling**
We compare models **with lag (zhvi_lag1)** vs **no-lag features**:

| Model Type | RMSE | R² | Notes |
|-----------|------|------|------|
| Linear Regression (with lag) | ~15K | 0.998–0.999 | Very strong — past prices dominate |
| Random Forest (with lag) | ~4.8K | 0.9998 | Best forecasting performance |
| Linear Regression (no lag) | ~213K | ~0.72 | Moderate signal |
| Random Forest (no lag) | ~170K | ~0.82 | Better, but still limited |

**Conclusion:**  
- For **forecasting**, lagged models are extremely accurate.  
- For **scenario analysis**, no-lag models reveal driver importance (prices, inventory, macro trends).  

---

## 📂 Data Sources

| Source | Dataset | Description |
|--------|---------|-------------|
| Zillow | `zillow_zhvi_zip_long.csv` | Home Value Index (ZHVI) for all Bay Area ZIPs |
| Redfin | `redfin_zip_monthly.csv` | Monthly inventory, sales, price metrics |
| FRED | `fred_monthly.csv` | Interest rates, CPI, unemployment |
| Merged Panel | `panel_zip_monthly.csv` | Final ZIP × Month dataset |

---

## 🧪 Methods Used

- **Data Cleaning & Merging** (pandas)  
- **Visualization** (Matplotlib & Seaborn)  
- **Clustering** (K-Means, PCA visualization)  
- **Regression Modeling**  
  - Linear Regression  
  - Random Forest Regressor  
  - Ridge & Lasso (no-lag scenario)  
- **Cross-Validation & Grid Search**  
- **Feature Importance** & Explainability  

---

## 📁 Project Structure
```
Capstone-Final-Bay-Area-Home-Price-Trends/
│
├── data/
│ ├── raw/
│ │ ├── zillow_zhvi_zip.csv
│ │ └── zip_code_market_tracker.tsv000
│ │
│ └── processed/
│ ├── zillow_zhvi_zip_long.csv  # Melted long-form Zillow data
│ ├── redfin_zip_monthly.csv    # Cleaned Redfin ZIP-level monthly metrics
│ ├── fred_monthly.csv          # Monthly macroeconomic data from FRED
│ └── panel_zip_monthly.csv     # Final merged panel dataset (used for EDA + modeling)
│
├── capstone_final_analysis.ipynb       # Final Notebook (Module 24)
├── Capstone_Project_Final_Report.docx  # Final written report
├── README.md
└── .gitignore					# Ensures raw data not uploaded to GitHub
```
## Why Raw Data Is Not Included in the Repository

The `/data/raw/` folder contains very large proprietary datasets such as:

- `zip_code_market_tracker.tsv000` (≈1.4 GB Redfin data)
- `zillow_zhvi_zip.csv`
- `acs_zcta_selected.csv`

These files are **too large for GitHub** and exceed the platform's file-size limits.  
Additionally, some datasets (e.g., Redfin) have redistribution restrictions.

For these reasons:

✔ Raw data is **excluded using `.gitignore`**  
✔ Only **processed, lightweight CSVs** (safe and <100 MB) are included  
✔ The README clearly explains how to recreate these files for replication  

## Rebuilding the Processed Data (If Needed)

To reproduce the processed datasets:

1. Place the raw files into:

```
data/raw/
    ├── zillow_zhvi_zip.csv
    ├── zip_code_market_tracker.tsv000
```
	
---

## 🔗 GitHub Links

### **📘 Final Capstone Notebook (Module 24)**
**https://github.com/Sourabh-Bhalerao/Capstone-Final-Bay-Area-Home-Price-Trends/blob/main/capstone_final_analysis_bay_area_home_prices.ipynb**

### **📗 Module 20 Notebook (Initial EDA & Panel Construction)** - as reference
**https://github.com/Sourabh-Bhalerao/Bay-Area-Home-Price-Trends/blob/main/capstone_initial_report_eda.ipynb**

### **📄 Final Word Report**
**https://github.com/Sourabh-Bhalerao/Capstone-Final-Bay-Area-Home-Price-Trends/blob/main/Capstone_Project_Final_Report_SB_11-16-2025.docx**

---

## 🚀 Next Steps

- Add **school quality, zoning, demographics, commute times** to enrich ZIP clusters  
- Explore **time-series forecasting** models (ARIMA, Prophet, LSTM)  
- Build an **interactive dashboard** for ZIP-level housing insights  
- Expand analysis to **forecast future price changes** (not just levels)  

---

**GitHub:** https://github.com/Sourabh-Bhalerao  

---
