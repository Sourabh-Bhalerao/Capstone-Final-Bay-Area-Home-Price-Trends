# Bay Area Home Price Trends – Capstone Project  (Module 20 Submission)
**Author:** Sourabh Bhalerao

---

## 📌 Executive Summary

This project analyzes **housing market trends at the ZIP-code level** in the **San Francisco Bay Area** using three major data sources:  
- **Zillow ZHVI (home value index)**  
- **Redfin Market Tracker (local supply/demand metrics)**  
- **Federal Reserve (macro-economic indicators)**  

The goal is to explore the drivers of home price changes in the Bay Area and build a **baseline machine-learning model** that can predict ZHVI home values using local housing activity and macroeconomic signals.

After combining and cleaning more than **100,000 monthly ZIP-level records**, I conducted exploratory data analysis (EDA), built multiple visualizations, engineered features, handled missing data, and trained a baseline **Linear Regression model**.  
This model serves as the foundation for further modeling in Module 24.

---

## 🎯 Rationale

Bay Area housing prices significantly impact:  
- buyers and sellers  
- local governments  
- investors and developers  
- affordability planning  
- market forecasting  

Understanding the relationship between **housing supply, demand, and macro-economic factors** is important for policy, investment, and personal financial planning.

This project demonstrates how open datasets can be combined to form a **multi-source analytical pipeline** capable of producing insight into one of the most dynamic real estate markets in the U.S.

---

## ❓ Research Question

**What factors drive month-to-month home price changes in Bay Area ZIP codes, and can we build a baseline predictive model using local housing activity and macroeconomic indicators?**

Sub-questions explored:

- Are Redfin measures (inventory, homes sold, list vs. sale price) predictive?  
- How do macroeconomic indicators (interest rates, unemployment, CPI) relate to ZIP-level home values?  
- Which ZIP codes show the strongest and weakest growth?  
- Can a baseline ML model reasonably predict ZHVI home prices?

---

## 📂 Data Sources

### 1. **Zillow ZHVI (ZIP-level Home Value Index)**  
- Monthly home value index for 5-digit ZIP codes  
- Provides long-term price history  
- Highly granular and standardized  

### 2. **Redfin Zip_Code_Market_Tracker TSV**  
Columns used after filtering:  
- `median_sale_price`  
- `median_list_price`  
- `inventory`  
- `homes_sold`  
- `price_drops`  
- `property_type` (kept only “All Residential”)  

### 3. **FRED (Federal Reserve Economic Data)**  
- `FEDFUNDS` – Federal Funds Rate  
- `CPIAUCSL` – Consumer Price Index  
- `UNRATE` – Unemployment Rate  

All datasets were aligned to **month-end frequencies**, merged on ZIP and date, and cleaned to produce a combined **panel dataset** of ~105k records.

---

## 🧹 Methodology

### **1. Data Cleaning**
- Loaded Zillow (wide format → melted to long format)  
- Chunk-loaded Redfin TSV (1.4GB) to avoid memory issues  
- Filtered Bay Area ZIP codes (13 counties)  
- Forward-filled and monthly-aligned FRED data  
- Removed duplicates  
- Removed extreme outliers (ZHVI < 50,000 or > 5,000,000)  
- Filtered only `All Residential` property type  

### **2. Feature Engineering**
- `zhvi_lag1` (previous month ZHVI)  
- `zhvi_pct_change_1m`  
- `sales_inventory_ratio = homes_sold / inventory`  
- Month-end alignment column  

### **3. Exploratory Data Analysis**
- Correlation Heatmap  
- Price Distribution  
- Time series trends by ZIP  
- Scatterplots exploring supply/demand dynamics  
- Macro indicators vs home price trends  

### **4. Baseline Modeling (Module 20 requirement)**
Model: **Linear Regression**  
Pipeline:  
- `SimpleImputer(strategy="median")`  
- `LinearRegression()`  

Train/Test Split: 80/20  
Evaluation Metrics:  
- RMSE  
- R²  

---

## 📊 Results

### **Baseline Linear Regression (No Macro Variables)**
- **RMSE:** ~13,586  
- **R²:** ~1.000  

Interpretation:  
- Near-perfect R² due to strong predictive power of lagged ZHVI  
- RMSE ~13k means typical prediction error is about ±13k on home value index  

### **Baseline Model With Macro Alignment**
After aligning FRED indicators to month-end:  
- **RMSE:** ~36,204  
- **R²:** ~0.997  

Interpretation:  
- Slight drop due to additional noise from macro features  
- Still strong predictive power  
- Model demonstrates local Redfin + macro impacts  

---

## 🔍 Key Findings

### 1. **ZHVI is strongly autocorrelated**
Lagged home values (`zhvi_lag1`) explain most of next month’s values.

### 2. **Local supply/demand metrics matter**
Higher `sales_inventory_ratio` often correlates with stronger price growth.

### 3. **Macro indicators influence trends**
- Lower interest rates → stronger price appreciation  
- Higher unemployment → mild cooling effect  
- CPI inflation correlates with long-term ZHVI drift  

### 4. **ZIP-level variation is large**
- Silicon Valley ZIPs show highest median values  
- Alameda & Contra Costa show more volatility  

### 5. **Data integration is non-trivial**
- Redfin markets multiple property types per ZIP/month  
- Needed filtering to avoid duplicate monthly entries  
- FRED alignment required forward-filling and month-end merging  

---

## 🚀 Next Steps (Module 24)

The full project requires additional models and refined reporting. Next steps include:

### **Modeling**
- Add Random Forest, XGBoost, Lasso, Ridge  
- Perform GridSearchCV for hyperparameter tuning  
- Compare multiple evaluation metrics  

### **Feature Engineering**
- Rolling-window volatility  
- Multi-month lags  
- Seasonality variables (month-of-year)  

### **Analysis**
- Deep-dive ZIP clusters  
- Price elasticity with interest rates  
- Identifying leading vs lagging indicators  

### **Artifact Generation**
- Produce final non-technical report  
- Cleaned notebooks with polished visualizations  
- Improve interpretability via SHAP values  

---

## 📁 Project Structure

project/
│
├── data/
│ ├── raw/
│ │ ├── zillow_zhvi_zip.csv
│ │ ├── zip_code_market_tracker.tsv000
│ │ └── acs_zcta_selected.csv # Not used in Module 20
│ │
│ └── processed/
│ ├── zillow_zhvi_zip_long.csv # Melted Zillow dataset
│ ├── redfin_zip_monthly.csv # Clean Redfin ZIP-level data
│ ├── fred_monthly.csv # FRED macro indicators (aligned)
│ └── panel_zip_monthly.csv # Final merged dataset (used in EDA + modeling)
│
├── capstone_initial_report_eda.ipynb # Module 20 notebook
├── README.md

---

## 👉 Notebook Link

[📘 capstone_initial_report_eda.ipynb](#)

---

## 📬 Contact
For questions or collaboration:  
**Sourabh Bhalerao**  

---
