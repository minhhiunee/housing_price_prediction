# Housing Price Prediction Using Multiple Linear Regression

## Project Overview

This project focuses on predicting residential housing prices using Multiple Linear Regression. By analyzing a structured housing dataset, the project explores relationships between housing attributes (such as area, number of bathrooms, furnishing status, and proximity to the main road) and the target variable — house price.

The project follows a structured data science workflow, from exploratory data analysis and preprocessing through feature selection and model evaluation.

---

## Objectives

- Explore the housing dataset to understand its structure and feature distributions.
- Analyze relationships between housing features and prices.
- Preprocess numerical and categorical features for model readiness.
- Examine multicollinearity among independent variables.
- Select relevant features using systematic methods.
- Train a Multiple Linear Regression model to predict housing prices.
- Evaluate the model's predictive performance on both training and testing sets.

---

## Dataset

The dataset used in this project is `Housing.csv`, located at:

```
data/raw/Housing.csv
```

### Dataset Summary

| Property | Value |
|---|---|
| Number of rows | 545 |
| Number of columns | 13 |
| Target variable | `price` (house price) |

### Features

**Numerical features:**
- `area` — house area (in square feet)

**Categorical / ordinal features:**
- `bedrooms` — number of bedrooms
- `bathrooms` — number of bathrooms
- `stories` — number of stories
- `parking` — number of parking spots
- `mainroad` — whether the house is on a main road (yes/no)
- `guestroom` — whether the house has a guest room (yes/no)
- `basement` — whether the house has a basement (yes/no)
- `hotwaterheating` — whether the house has hot water heating (yes/no)
- `airconditioning` — whether the house has air conditioning (yes/no)
- `prefarea` — whether the house is in a preferred area (yes/no)
- `furnishingstatus` — furnishing status (furnished / semi-furnished / unfurnished)

---

## Project Structure

```
Project_DS/
├── README.md
├── requirements.txt
├── data/
│   └── raw/
│       └── Housing.csv
├── notebooks/
│   └── housing_price_prediction.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
└── reports/
    └── slides/
```

---

## Methodology

The project follows these steps:

1. **Data Loading** — Load `Housing.csv` from `data/raw/`.
2. **Data Inspection** — Inspect data types, shape, and unique value counts.
3. **Exploratory Data Analysis (EDA)** — Visualize target variable distribution and feature relationships.
4. **Data Preprocessing** — Check for and handle missing values, duplicates, and outliers.
5. **Categorical Encoding** — Apply one-hot encoding to binary and multi-class categorical features.
6. **Train-Test Split** — Split the dataset into 80% training and 20% testing sets.
7. **Feature Scaling** — Standardize features using `StandardScaler` (fitted on training set only).
8. **Multicollinearity Analysis** — Use VIF (Variance Inflation Factor) to detect collinear features.
9. **Feature Selection** — Apply RFE (Recursive Feature Elimination) with `LinearRegression` to select the 10 most informative features out of 13.
10. **Multiple Linear Regression Training** — Train the model exclusively on the RFE-selected features.
11. **Model Evaluation** — Evaluate performance using R², RSS, MSE, and RMSE on both sets.
12. **Residual Analysis** — Analyze error distribution and actual vs. predicted plots.

---

## Model

### Multiple Linear Regression

Multiple Linear Regression estimates the linear relationship between housing price and multiple independent variables. Each regression coefficient represents the expected change in price for a unit change in the corresponding feature, holding all other features constant.

The model is implemented using `sklearn.linear_model.LinearRegression`, trained on the **10 features selected by RFE**:

| Feature | Description |
|---|---|
| `area` | House area (sq ft) |
| `bathrooms` | Number of bathrooms |
| `stories` | Number of stories |
| `parking` | Number of parking spots |
| `mainroad_yes` | On main road |
| `basement_yes` | Has basement |
| `hotwaterheating_yes` | Has hot water heating |
| `airconditioning_yes` | Has air conditioning |
| `prefarea_yes` | In preferred area |
| `furnishingstatus_unfurnished` | Unfurnished status |

> Features eliminated by RFE: `bedrooms`, `guestroom_yes`, `furnishingstatus_semi-furnished`.

---

## Evaluation Metrics

The following metrics are used to assess model performance:

| Metric | Description |
|---|---|
| **R² Score** | Proportion of variance in house price explained by the model |
| **Residual Sum of Squares (RSS)** | Total squared difference between actual and predicted values |
| **Mean Squared Error (MSE)** | Average squared prediction error |
| **Root Mean Squared Error (RMSE)** | Square root of MSE; in the same unit as the target |

---

## Results

The Multiple Linear Regression model was trained on 10 RFE-selected features and evaluated on both training and testing sets:

| Set | R² | RMSE |
|---|---|---|
| **Training** | 0.6579 | 1,080,025 |
| **Testing** | 0.7216 | 981,706 |

> The model generalizes well to unseen data, with the test R² (0.7216) slightly exceeding the training R² (0.6579), indicating no overfitting.

Detailed results are available in:
- Notebook: `notebooks/housing_price_prediction.ipynb`
- Tables: `outputs/tables/`
- Figures: `outputs/figures/`

---

## Installation

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Usage

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Then open:

```
notebooks/housing_price_prediction.ipynb
```

Run all cells sequentially from top to bottom.

---

## Limitations

- The dataset is relatively small (545 records), which may limit the model's ability to generalize.
- Multiple Linear Regression assumes a linear relationship between features and the target variable.
- The model is sensitive to multicollinearity and outliers.
- Complex nonlinear patterns in housing prices may not be fully captured by a linear model.

---

## Future Improvements

- Apply cross-validation for more robust model evaluation.
- Perform systematic feature engineering to enrich the feature set.
- Tune the preprocessing pipeline for better data quality.
- Compare the baseline Multiple Linear Regression model with nonlinear algorithms (e.g., Random Forest, Gradient Boosting) as a future extension.

---

## Authors

- Nguyễn Minh Hiếu: 0.8
- Vũ Nam Hải: 0.2
