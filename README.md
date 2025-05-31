# 🛒 Rossmann Store Sales Forecasting
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
## 📌 Project Overview

This project focuses on forecasting daily sales for Rossmann drug stores using historical transaction data, store-specific information, and promotional activity. It is designed to improve demand forecasting and help managers make better scheduling decisions. The workflow includes steps from data loading to final prediction submission.

---

## 📁 Dataset Explanation

### 1. `train.csv`

* Historical daily sales data from 2013 to 2015.
* Includes store ID, number of customers, whether the store was open, ongoing promotions, state and school holidays.

### 2. `test.csv`

* Same structure as `train.csv`, but without the `Sales` column.
* Used for final prediction and submission.

### 3. `store.csv`

* Contains additional store-level info such as:

  * `StoreType`, `Assortment`, `CompetitionDistance`
  * Whether the store is running `Promo2` and when it started.

### 4. `sample_submission.csv`

* Template to structure the predictions for Kaggle submission.

---

## 📊 Project Steps Explained

### 🔹 1. Load and Merge Data

* All datasets are loaded using `pandas` and merged with store info using the `Store` key to enrich the training and test datasets.

### 🔹 2. Handle Missing Values

* Median imputation is used for numerical columns with missing values.
* Categorical values (e.g. `PromoInterval`) are filled with a default category.

### 🔹 3. Feature Engineering with Dates

The `Date` column is converted to datetime format, and new features such as `Day`, `Month`, and `Year` are extracted to help models learn seasonality.

### 🔹 4. Filter for Open Stores

Closed stores (`Open == 0`) are excluded from training data since their sales would be zero and uninformative.

### 🔹 5. Exploratory Data Analysis (EDA)

* Histogram of `Sales` to understand distribution.
* Bar plots for categorical features like `Promo`, `DayOfWeek`, etc.
* Correlation heatmap of numerical features to examine multicollinearity.

### 🔹 6. Data Preprocessing

* **Numerical Features**: Scaled using `MinMaxScaler` after imputation.
* **Categorical Features**: Encoded with `OneHotEncoder` to convert them into numerical format.

### 🔹 7. Modeling

A variety of models are trained to evaluate baseline and advanced performance:

* **Linear Models**: LinearRegression, Ridge, Lasso, ElasticNet
* **Tree Models**: DecisionTreeRegressor, RandomForestRegressor

### 🔹 8. Ensemble Learning

Predictions from Ridge, Decision Tree, and Random Forest are combined via weighted averaging. The weights are optimized using `scipy.optimize.minimize` to minimize validation RMSE.

### 🔹 9. Evaluation Metrics

* **RMSE (Root Mean Squared Error)** measures absolute prediction error.
* **RMSPE (Root Mean Square Percentage Error)** considers percentage-based error (more relevant for sales).

| Model        | RMSE    | RMSPE  |
| ------------ | ------- | ------ |
| RandomForest | 1154.43 | 18.74% |
| DecisionTree | 1469.77 | 21.88% |
| Ridge        | 2718.66 | 48.44% |
| Ensemble     | 1201.49 | 19.34% |

### 🔹 10. Feature Importance

Top 10 features from each model are visualized using horizontal bar charts to understand which features most influenced the predictions.

### 🔹 11. Final Submission

Predictions are made on the test set using the trained ensemble model. The results are multiplied by the `Open` flag and saved in `submission.csv`.

---

## 📦 Project Directory Structure

```
Rossmann-Sales-Forecasting/
├── data
│   ├── train.csv
│   ├── test.csv
│   ├── store.csv
│   └── sample_submission.csv
│
├── notebooks
│   └── Rossmann Sales Forecasting.ipynb
│
├── outputs
│   └── submission.csv
```

---

## 🛠️ Setup & Installation

```bash
pip install -r requirements.txt
```

---

## 📤 Submission Format

Ensure your output file `submission.csv` follows this structure:

```
Id,Sales
1,5263.0
2,6064.0
...
```

---

