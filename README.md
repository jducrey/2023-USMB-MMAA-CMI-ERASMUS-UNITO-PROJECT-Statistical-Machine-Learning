# PROJECT: Statistical Machine Learning
## Overview
This project focuses on Data Analytics, Data Visualization, Statistical Machine Learning, and Predictive Analysis.
🎓 Project realised during my mobility of studies Erasmus+ of my Master's degree MMAA – Université Savoie Mont Blanc

## PROJECT CHALLENGE 
### Context
As a data scientist for a multinational retail company, your objective is to analyze sales and market data to provide business insights.

### Company description: 
The company operates a vast network of hypermarkets, supermarkets, and minimarkets worldwide. It offers a wide range of products, from groceries to electronics and household goods, catering to diverse consumer needs.

### THE DATASETS 
The company gives you the access to two datasets: sales and market.

##### sales.csv (Daily sales per market)
This file contains the daily sales for each market.

Column name  | Data type | Notes 

market_id    | string    | Reference the column “id” in the “market.csv” file 

date         | date      | Format DD/MM/YYYY. Dates range from 01/01/2021 to 31/12/2022.

is_open      | string    |  YES: the market was open on that day. NO: the market was closed on that day. If a market is closed then sales_amount has to be zero. No strings different than YES/NO should be present.

sales_amount | float     | Daily sales in €. It contains only actual sales, no refunds. This implies that only values >= 0 should be present. 

##### market.csv (Market registry)
This file contains the market registry (that is, one row per market).

Column name         | Data type | Notes 

id                  | string    | Unique identifier of the market 

country             | string    | Location (country) of the market 

market_type         | string    | Type of the market. Can be MINI/SUPER/HYPER 

square_feet         | integer   | Square feet of the market 

avg_customers       | integer   | Daily average of customers in the market 

competitor_distance | integer   | Distance in meters from nearest competitor 

has_promotion       | string    | YES: the market may have promotions during the year. NO: the market cannot apply any promotion.

### Company Objectives 
The company is interested in 2 objectives. Below are the details. 
 
#### Objective 1 : Understanding Predictive Relationships
Considering a linear relationship between target and predictors, the company is interested in 
understanding the delta changes (that is, a 1-unit increase in the predictor leads to a XX 
variation in the target).  
 
#### Objective 2 : Selecting New Market Locations
The company in 2024 wants to open 3 new markets: 1 MINI, 1 SUPER and 1 HYPER. 
There are multiple options to choose from. 

##### Options for MINI markets:
Country | Square feet | Estimated average customers | Nearest competitor distance | Will it run promotions? 

SPAIN   | 1850        | 190                         | 4500                        | YES 

FRANCE  | 2100        | 215                         | 1850                        | YES 

ITALY   | 1920        | 220                         | 1450                        | YES 

##### Options for SUPER markets:
Country | Square feet | Estimated average customers | Nearest competitor distance | Will it run promotions? 

SPAIN   | 5880        | 420                         | 580                         | YES 

FRANCE  | 5120        | 390                         | 2560                        | YES 

ITALY   | 4970        | 410                         | 3520                        | YES 

##### Options for HYPER markets:
Country | Square feet | Estimated average customers | Nearest competitor distance | Will it run promotions?

SPAIN   | 10560       | 860                         | 8940                        | YES

FRANCE  | 12570       | 880                         | 7580                        | YES

ITALY   | 11980       | 790                         | 11560                       | YES 

This second objective is to determine the best market to open in 2024 for each type.

### The Data Sciences Methods applied:
Data Cleaning (Deduplication, Datatypes Conversion)

Imputation on missing values

Monovariate Analysis

Bivariate Analysis

Outliers Analysis

Data Standardisation

Encoding of Categorical Variables (One-Hot Encoding, Binarization, Ordinal Mapping)

Machine Learning Models Fitting Tests:
- Multilinear Regression Model
- BestSubsetSelection (Feature Selection Method)
- Principal Component Analysis (PCA) (Dimension Reduction Method)
- Partial Least Square (PLS) (Dimension Reduction Method)
- Ridge Regression (Shrinkage Method)
- Lasso Regression (Shrinkage Method)
- Polynomial Regression Model (order 2 and 3)
- General Additive Model (GAM)
- RadomForest Regression Model
- GradientBoosting Regression Model
- Support Vector Machine (SVM) : Computationnaly too expensive.
- Regression Neural Network (Deep Learning Method)
  
### The Results:
#### Objective 1 : Model Insights
Looking at the p-value of each coefficient, we can reject the null hypothesis beacuse we have p-value(<0.05) for each predictors.

We clearly see that some predictors are more useful than others especially "square_feet","market_type","avg_customers".

We also check the confidence intervals of each coefficients:
- The 95% confidence interval for const is [6790.47389936 ; 7066.0735999 ]
- The 95% confidence interval for square_feet is [24289.06603758 ; 24660.94885055]
- The 95% confidence interval for avg_customers is [18483.28774107 ; 18780.68912206]
- The 95% confidence interval for competitor_distance is [-2748.34651976 ; -2663.02433942]
- The 95% confidence interval for FRANCE is [3151.68579136 ; 3249.63746199]
- The 95% confidence interval for ITALY is [1476.26302459 ; 1579.20568879]
- The 95% confidence interval for SPAIN is [2149.7063918 ; 2250.04914072]
- The 95% confidence interval for market_type is [14113.09164343 ; 14411.25968925]
- The 95% confidence interval for has_promotions is [-701.81525501 ; -333.56766394]

To estimate the accuracy of our model, we compute the MSE and also others statistics like RSE and R2, to have more information about our model.
The RSE is 4075.63, the R2 is 0.93 and the MSE is 16609081.09, which is not so bad.

#### Objective 2: Model Comparison
Comparasion of the different MSE of all fitted models and choose of the model with the lowest estimated test error(mse):

Model	                             | MSE

Linear_Model                       | 1.660908e+07

Linear_Model_Best_Subset_Selection | 1.652662e+07

Linear_Model_PCA                   | 1.652662e+07

Linear_Model_PLS                   | 1.652662e+07

Ridge	                             | 1.652662e+07

Lasso	                             | 1.652662e+07

Polynomial_Regression_order_2	     | 2.486403e+06

Polynomial_Regression_order_3	     | 2.464412e+06

GAM                                | 2.789227e+06

Pruning                            | 3.672416e+06

RandomForest                       | 2.463885e+06

GradientBoosting                   | 2.464341e+06

NeuralNetwork	                     | 3.330243e+06

We conclude that the best fitting model for these datas is the Random Forest Regression.

#### Best Model and Market Selection

We use our best fitting model found previously (Random Forest Regression), fitted on the whole available training datasets, to make predictions of the potentials sales amounts, for each of these markets candidates. For each type of market, the one with the higher sales amount predictions, was choosen.

From these predictions, we answer to the company that the best choice, among the candidates is:
- the french market, for the minimarket, with potential sales amount of 12469,46 €.
- the french market, for the supermarket, with potential sales amount of 24609,50 €.
- the french market, for the hypermarket, with potential sales amount of 58743,30 €.

Thus, the recommended locations for new markets in 2024 are all in France.

### Conclusion

This project demonstrates the application of machine learning to support strategic business decisions in retail. The insights derived from statistical models help optimize market expansion strategies and improve overall sales predictions.

