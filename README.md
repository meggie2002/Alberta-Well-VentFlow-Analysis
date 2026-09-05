# Vent-Flow Event Severity Classification in Alberta Wells

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Domain](https://img.shields.io/badge/Domain-Data_Analytics_|_Environmental_Safety-green.svg)
![Framework](https://img.shields.io/badge/Libraries-rpart_|_caret_|_smotefamily-orange.svg)

## Project Overview
Surface Casing Vent Flow (SCVF) and Gas Migration (GM) events in oil and gas wells present environmental and safety hazards, including potential groundwater contamination and greenhouse gas emissions. This project utilizes public dataset records from the **Alberta Energy Regulator (AER)** to analyze, model, and classify vent-flow event severity (`Serious` vs. `Non-Serious`).

Through statistical analysis, stratified cross-validation, decision trees (`rpart`), and resampling strategies (SMOTE oversampling and undersampling), this project establishes empirical decision thresholds for well safety and risk assessment.

---

## Decision Tree Architecture

![Decision Tree Diagram](decision_tree_architecture.png)

### Core Split Rules
* **Flow Rate $\ge 299\ m^3/day$**: Signals high probability ($96\%$) of a **Serious** event.
* **Shut-In Pressure $\ge 1448\ kPa$**: Significant indicator of elevated severity risk.
* **Source Depth $\ge 113\ mkb$**: Interacts with lower surface pressures to drive serious event risk in deeper well sources.

---

## Model Evaluation & Performance Comparison

| Approach / Model | Validation Method | Overall Accuracy | Non-Serious Sensitivity | Serious Recall / Specificity |
| :--- | :---: | :---: | :---: | :---: |
| **Decision Tree (Stratified 10-Fold CV)** | 10-Fold CV | **84.05%** | **97.50%** | **45.19%** |
| **Decision Tree (Baseline Split)** | 75/25 Split | 84.19% | 98.14% | 36.94% |
| **Decision Tree (SMOTE Oversampling)** | 5-Fold CV | 79.20% | Balance Adjusted | Improved |
| **Decision Tree (SMOTE Undersampling)** | 5-Fold CV | 78.50% | Balance Adjusted | Improved |

---

## Analytical Workflow
1. `01_data_cleaning_and_preprocessing.Rmd`: Handles raw data ingestion, trims whitespace, standardizes column names, and maps target labels (`Considered Non Serious` $\rightarrow$ `Non Serious`).
2. `02_exploratory_data_analysis.Rmd`: Analyzes target variable class distributions, feature distributions, and bivariate relationships.
3. `03_decision_tree_10fold_cv.Rmd`: Trains baseline decision tree models evaluated via Stratified 10-Fold Cross-Validation (`caret`).
4. `03_decision_tree_train_test_split.Rmd`: Validates baseline decision tree performance using a 75/25 train-test split.
5. `04_smote_oversampling.Rmd` & `04_smote_undersampling.Rmd`: Implements Synthetic Minority Over-sampling Technique (SMOTE) and majority downsampling to address minority class imbalance.
6. `04_smote_pruned_tree.Rmd`: Evaluates cost-complexity parameters (`cp`) to prune decision tree depth and mitigate overfitting.

---

## Repository Artifacts
* `Alberta_VentFlow_Severity_Report.pdf`: Full written academic and analytical report detailing problem context, methodology, statistical models, and risk mitigation strategies.
* `cleaned_vent_flow_data.csv`: Structured, 7-feature dataset containing 9,750 well observation records processed directly from AER public reports.
* `decision_tree_architecture.png`: Trained decision tree diagram highlighting split thresholds and leaf distributions.

---

## Requirements & Dependencies
* **Language**: R (v4.x)
* **Libraries**: `rpart`, `rpart.plot`, `caret`, `dplyr`, `smotefamily`, `ggplot2`, `gridExtra`, `tidyverse`
