# 🧠 Project: Statistical Machine Learning

🎓 *Realised during my Erasmus+ mobility – Master MMAA*  
Université Savoie Mont Blanc × Università degli Studi di Torino

---

## 📌 Overview

This project focuses on **Data Analytics**, **Data Visualization**, **Statistical Machine Learning**, and **Predictive Analysis**.

---

## 🏢 Business Scenario

As a data scientist in a multinational retail company, your task is to analyze sales and market data to derive business insights and support strategic decisions.

The company operates a global network of **hypermarkets**, **supermarkets**, and **minimarkets**, offering everything from groceries to electronics and home goods.

---

## 📊 Datasets

### 1. `sales.csv` – Daily Sales per Market

| Column         | Type   | Notes                                                                 |
|----------------|--------|------------------------------------------------------------------------|
| `market_id`    | string | Refers to `id` in `market.csv`                                         |
| `date`         | date   | Format: `DD/MM/YYYY` (01/01/2021 → 31/12/2022)                         |
| `is_open`      | string | `YES` or `NO`; if `NO`, then `sales_amount` = 0                        |
| `sales_amount` | float  | Daily sales in €; only positive values (no refunds)                    |

### 2. `market.csv` – Market Registry

| Column              | Type    | Notes                                                       |
|---------------------|---------|-------------------------------------------------------------|
| `id`                | string  | Unique market ID                                            |
| `country`           | string  | Country location                                            |
| `market_type`       | string  | Either `MINI`, `SUPER`, or `HYPER`                          |
| `square_feet`       | integer | Market area in square feet                                  |
| `avg_customers`     | integer | Daily average customer visits                               |
| `competitor_distance` | integer | Distance in meters to nearest competitor                 |
| `has_promotion`     | string  | Whether promotions can run: `YES` or `NO`                   |

---

## 🎯 Company Objectives

### 🔹 Objective 1: Understand Predictive Relationships

> Identify how each predictor influences the sales target using linear regression.  
> Interpret delta changes: “a 1-unit increase in X leads to a variation of Y in sales”.

### 🔹 Objective 2: Market Expansion – 2024

The company plans to open 3 new markets:

- 1 `MINI`  
- 1 `SUPER`  
- 1 `HYPER`  

Determine the best performing candidate for each.

---

## 🔍 Candidate Locations

### MINI Markets

| Country | Sq. Feet | Avg. Customers | Competitor Distance | Promotion |
|---------|----------|----------------|----------------------|-----------|
| SPAIN   | 1850     | 190            | 4500                 | YES       |
| FRANCE  | 2100     | 215            | 1850                 | YES       |
| ITALY   | 1920     | 220            | 1450                 | YES       |

### SUPER Markets

| Country | Sq. Feet | Avg. Customers | Competitor Distance | Promotion |
|---------|----------|----------------|----------------------|-----------|
| SPAIN   | 5880     | 420            | 580                  | YES       |
| FRANCE  | 5120     | 390            | 2560                 | YES       |
| ITALY   | 4970     | 410            | 3520                 | YES       |

### HYPER Markets

| Country | Sq. Feet | Avg. Customers | Competitor Distance | Promotion |
|---------|----------|----------------|----------------------|-----------|
| SPAIN   | 10560    | 860            | 8940                 | YES       |
| FRANCE  | 12570    | 880            | 7580                 | YES       |
| ITALY   | 11980    | 790            | 11560                | YES       |

---

## 🛠️ Methods Used

- **Data Cleaning:** deduplication, type conversion  
- **Imputation:** handling missing values  
- **Exploratory Analysis:** monovariate & bivariate  
- **Outlier Detection**  
- **Feature Engineering:**  
  - One-hot encoding  
  - Binarization  
  - Ordinal mapping  
  - Standardisation  
- **Modeling Techniques:**  
  - Multilinear Regression  
  - Feature Selection: Best Subset Selection  
  - Dimension Reduction: PCA, PLS  
  - Regularisation: Ridge, Lasso  
  - Polynomial Regression (order 2 & 3)  
  - General Additive Model (GAM)  
  - Tree-based Models: Random Forest, Gradient Boosting  
  - Deep Learning: Neural Network  
  - SVM (too computationally expensive here)  

---

## 📈 Objective 1: Results & Interpretation

### 🔑 Key Findings

- Most relevant predictors: `square_feet`, `market_type`, `avg_customers`  
- All p-values < 0.05 → predictors are statistically significant  
- R² = **0.93**, RSE = **4075.63**, MSE = **16,609,081.09 €²**

### 📏 Confidence Intervals (95%)

| Predictor             | 95% CI                    |
|-----------------------|---------------------------|
| Const                 | [6790.47 ; 7066.07]       |
| square_feet           | [24289.07 ; 24660.95]     |
| avg_customers         | [18483.29 ; 18780.69]     |
| competitor_distance   | [-2748.35 ; -2663.02]     |
| FRANCE                | [3151.69 ; 3249.64]       |
| ITALY                 | [1476.26 ; 1579.21]       |
| SPAIN                 | [2149.71 ; 2250.05]       |
| market_type           | [14113.09 ; 14411.26]     |
| has_promotions        | [-701.82 ; -333.57]       |

---

## 🧪 Objective 2: Model Comparison

| Model                         | MSE (€²)     |
|-------------------------------|--------------|
| Linear                        | 16,609,080   |
| Best Subset Selection         | 16,526,620   |
| PCA / PLS / Ridge / Lasso     | 16,526,620   |
| Polynomial Regression (order 2)| 2,486,403   |
| Polynomial Regression (order 3)| 2,464,412   |
| General Additive Model (GAM)  | 2,789,227    |
| Decision Tree (Pruned)        | 3,672,416    |
| **Random Forest**             | **2,463,885** ✅ |
| Gradient Boosting             | 2,464,341    |
| Neural Network                | 3,330,243    |

📌 **Best model:** `Random Forest Regression`

---

## 📊 Objective 2: Predictions & Market Recommendations

**Predicted daily sales using Random Forest:**

| Market Type | Best Country | Predicted Sales (€) |
|-------------|--------------|---------------------|
| MINI        | FRANCE       | 12,469.46           |
| SUPER       | FRANCE       | 24,609.50           |
| HYPER       | FRANCE       | 58,743.30           |

✅ **Recommendation:** Open all 3 markets in **France** in **2024**

---

## ✅ Conclusion

This project shows how **Statistical Machine Learning** can support data-driven strategic decisions in the retail industry:

- 🎯 **Objective 1:** Explain predictive relationships and understand key business drivers.  
- 🧠 **Objective 2:** Guide optimal market expansion decisions through accurate forecasting.

By leveraging **Random Forest** and data science best practices, we delivered actionable insights with real business impact.
