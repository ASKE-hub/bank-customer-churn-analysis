# Bank Customer Churn Analysis

## Project Overview

This project analyzes customer banking data to identify patterns associated with customer churn and understand which customer characteristics may be linked to account closure.

The analysis covers the full data analytics workflow, including data integration, quality assurance, data cleaning, exploratory data analysis, feature engineering, and preparation of the dataset for machine learning.

## Objectives

* Import and combine customer and account information.
* Clean and validate the merged dataset.
* Identify and handle missing, duplicate, and erroneous data.
* Standardize inconsistent country labels.
* Analyze customer churn across categorical and numerical variables.
* Engineer new features to support churn analysis.
* Prepare the dataset for predictive modeling.

## Dataset

The final dataset contains **10,004 customer records and 14 columns**.

Key variables include:

* `CustomerId`
* `CreditScore`
* `Geography`
* `Gender`
* `Age`
* `Tenure`
* `EstimatedSalary`
* `Balance`
* `NumOfProducts`
* `HasCrCard`
* `IsActiveMember`
* `Exited`

`Exited` was used as the target variable:

* `0` → Customer did not churn
* `1` → Customer churned

## Data Import & Integration

Two tables were imported from the Excel workbook:

* `Customer_Info`
* `Account_Info`

The tables were combined using a **left join** based on `CustomerID`.

During the integration stage, duplicate rows and duplicate/redundant columns were identified and removed where appropriate.

## Data Cleaning & Quality Assurance

The initial data-quality assessment identified several issues.

The merged dataset contained:

* **10,004 rows**
* **14 columns**
* Missing values in `Surname`
* Missing values in `Age`
* Numeric fields stored as `object`
* Categorical fields stored as text
* Inconsistent country labels
* Erroneous/extreme numeric values

For example, `EstimatedSalary` contained an invalid value of **-999,999**, which was identified as a non-sensical value and handled during the cleaning process.

Missing values were treated according to data type:

* Categorical missing values → `MISSING`
* Numeric missing values → median imputation

Country labels in `Geography` were also standardized to ensure that different representations of the same country were treated as a single category.

## Exploratory Data Analysis

The target variable was analyzed to understand the overall churn distribution.

The dataset contained approximately **20.37% churned customers**, meaning the majority of customers remained with the bank.

### Categorical Analysis

Customer churn was explored across categorical variables including:

* Geography
* Gender
* Credit card ownership
* Active membership status

Bar charts and percentage-based comparisons were used to identify differences in churn behavior between customer groups.

### Numerical Analysis

Numerical variables were analyzed using:

* Box plots
* Histograms
* Descriptive statistics

Variables examined included:

* Credit Score
* Age
* Tenure
* Estimated Salary
* Balance
* Number of Products

These visualizations helped identify distributions, differences between churners and non-churners, and potential outliers.

## Feature Engineering

A new feature called `Balance_v_Sal` was created:

```python
modelling_df["Balance_v_Sal"] = (
    modelling_df["Balance"] /
    modelling_df["EstimatedSalary"]
)
```

This feature represents the customer's bank balance relative to their estimated salary.

The analysis showed that this ratio contained significant extreme values:

* Median: approximately **0.75**
* 75th percentile: approximately **1.52**
* Maximum: approximately **10,614.66**

This highlighted the importance of identifying and handling outliers before using engineered features in a modeling workflow.

## Data Preparation for Modeling

Before modeling, unsuitable columns were removed and categorical variables were transformed into numerical representations.

Dummy variables were created for categorical features to make them suitable for machine learning algorithms.

The dataset was then structured around the target variable `Exited` and the selected customer features.

## Key Data Quality Findings

Several important data-quality issues were identified during the project:

1. Missing values were present in `Surname` and `Age`.
2. `EstimatedSalary` and `Balance` were initially stored as text instead of numeric data types.
3. `HasCrCard` and `IsActiveMember` were stored as categorical text values.
4. Geography contained inconsistent country labels such as `FRA` and `French`.
5. An invalid `EstimatedSalary` value of `-999999` was identified.
6. The engineered `Balance_v_Sal` feature contained extreme outliers.

## Key Findings

* Approximately **20.37%** of customers in the cleaned dataset were classified as churners.
* Customer churn was analyzed across demographic, financial, and account-related characteristics.
* Data preparation revealed several inconsistencies that could have affected the accuracy of downstream analysis.
* Feature engineering provided additional information about the relationship between customer balance and estimated salary.
* The project demonstrated the importance of data quality before performing predictive analytics.

## Tools & Technologies

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Jupyter Notebook**
* **Excel**

## Project Workflow

```text
Raw Excel Data
      ↓
Import Customer & Account Data
      ↓
Left Join on CustomerID
      ↓
Duplicate & Data Quality Checks
      ↓
Missing Value Treatment
      ↓
Data Type Correction
      ↓
Outlier & Erroneous Value Handling
      ↓
Geography Standardization
      ↓
Exploratory Data Analysis
      ↓
Feature Engineering
      ↓
Categorical Encoding
      ↓
Modeling Preparation
```

## Conclusion

This project demonstrates an end-to-end data analytics workflow for a customer churn problem.

Rather than focusing only on visualization, the analysis covered the complete process from raw data integration and quality assurance through exploratory analysis and feature preparation for machine learning.

The project highlights how effective data cleaning and feature engineering can improve the reliability of customer churn analysis and provide a stronger foundation for predictive modeling.
