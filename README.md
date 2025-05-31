# 🛒 Rossmann Store Sales Forecasting
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Project Overview
Rossmann operates over **3,000 drug stores** in **7 European countries**. In this Kaggle competition, the task is to forecast daily sales for 6 weeks across 1,115 Rossmann stores in Germany. Accurate forecasts help store managers improve planning and resource allocation.

This project implements a complete machine learning pipeline to tackle this business problem, including:
- Data Cleaning
- Exploratory Data Analysis
- Feature Engineering
- Model Training
- Ensemble Learning
- Final Submission to Kaggle

---

## 📁 Dataset Description

### `train.csv`
- Historical sales data from 2013–2015.
- Includes Store ID, Sales, Customers, Open/Closed status, and Promotion info.

### `test.csv`
- Same structure as `train.csv` **without Sales**.
- Used for making final predictions.

### `store.csv`
- Store metadata: StoreType, Assortment level, Competition distance, Promo2 status, etc.

### `sample_submission.csv`
- Format template to structure predictions for Kaggle evaluation.

---

## 📊 Workflow Summary

### 🔹 1. Load & Merge Data
- Merged `train.csv` and `test.csv` with `store.csv` on the `Store` column.

### 🔹 2. Handle Missing Values
- Filled missing numerical values with median (e.g. `CompetitionDistance`).
- Filled `PromoInterval` with the most frequent value.

### 🔹 3. Feature Engineering
- Extracted `Day`, `Month`, `Year` from the `Date` column.
- Filtered training data to include only rows where stores were open (`Open == 1`).

### 🔹 4. EDA (Exploratory Data Analysis)
- Visualized sales distributions.
- Examined relationships between `Sales` and `Promo`, `DayOfWeek`, `Month`, `Year`.
- Generated a correlation heatmap to identify feature relationships.

### 🔹 5. Data Preprocessing
- Applied **MinMaxScaler** to normalize numeric features.
- Applied **OneHotEncoder** to convert categorical columns into numeric format.

### 🔹 6. Modeling
Trained a variety of models:
- **Linear Models**: Linear Regression, Ridge, Lasso, ElasticNet
- **Tree-Based Models**: Decision Tree, Random Forest

### 🔹 7. Ensemble Learning
- Combined **Ridge**, **Decision Tree**, and **Random Forest** predictions using weighted averaging.
- Weights: `0.6 * RandomForest + 0.3 * DecisionTree + 0.1 * Ridge`

### 🔹 8. Evaluation Metrics
- **RMSE**: Root Mean Squared Error
- **RMSPE**: Root Mean Square Percentage Error (used by Kaggle)

| Model        | RMSE    | RMSPE  |
|--------------|---------|--------|
| RandomForest | 1154.43 | 18.74% |
| DecisionTree | 1469.77 | 21.88% |
| Ridge        | 2718.66 | 48.44% |
| Ensemble     | 1306.09 | 18.76% |

### 🔹 9. Feature Importance
Visualized top 10 features contributing to each model's prediction using bar charts.

### 🔹 10. Final Submission
- Predictions were made on the test set.
- Final results were stored in `submission.csv` as per Kaggle format:
```
csv
Id,Sales
1,5263.0
2,6064.0
...
```

## 🗂️ Project Structure
```
Rossmann-Sales-Forecasting/
├── data/
│   ├── train.csv
│   ├── test.csv
│   ├── store.csv
│   └── sample_submission.csv
│
├── notebooks/
│   └── Rossmann_Sales_Forecasting.ipynb
│   └── Updated_Rossmann_Sales_Forecasting.ipynb
|
├── outputs/
│   └── submission.csv
│
├── README.md
└── .gitignore
```

