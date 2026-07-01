# Healthcare Expenditure Analysis Using MEPS 2022 Data

## Project Description

This project analyzes the 2022 Medical Expenditure Panel Survey (MEPS) Household Component (HC-243) to identify the demographic, socioeconomic, and clinical factors associated with high healthcare expenditure in the U.S. population. The analysis combines statistical modeling in Python with an interactive Power BI dashboard to surface patterns in spending across age, gender, region, insurance coverage, and chronic disease burden.

The outcome variable, high expenditure, was defined as total annual healthcare spending (`TOTEXP22`) above the sample median, and modeled using logistic regression and LASSO-regularized logistic regression. A composite multimorbidity score, built from six chronic condition flags (hypertension, coronary heart disease, stroke, cancer, arthritis, and asthma), was the strongest predictor of high spending across every model and subgroup tested.

## Objectives

- Quantify how age, sex, region, poverty category, insurance coverage, and education relate to the odds of high healthcare expenditure
- Build a multimorbidity index from chronic condition indicators and test its association with spending
- Compare full-sample and gender-stratified logistic regression models using odds ratios and confidence intervals
- Apply LASSO logistic regression for feature selection and regularization, and evaluate classification performance
- Visualize regional and demographic spending patterns through statistical charts, a choropleth map, and a Power BI dashboard

## Dataset

- **Source:** [Medical Expenditure Panel Survey (MEPS) 2022 Full-Year Consolidated Data File, HC-243](https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-243)
- **File used:** `h243.csv`
- **Sample size:** ~22,236 respondents after filtering invalid region and age codes; ~20,705–22,236 used across individual models depending on missing-data handling
- **Key variables:** `TOTEXP22` (total expenditure), `AGE22X`, `SEX`, `RACEV1X`, `REGION22`, `POVCAT22`, `INSCOV22`, `EDUCYR`, `MARRY22X`, and six `*DX` chronic condition flags

> **Note:** The raw MEPS data file is not included in this repository due to size and AHRQ's data use terms. It can be downloaded directly from the [AHRQ MEPS website](https://meps.ahrq.gov/mepsweb/).

## Methodology

1. **Data Cleaning** – Removed invalid MEPS codes for region and age; handled missing values across predictors
2. **Feature Engineering** – Created a binary high-expenditure outcome (median split, with a top-10%-spender variant also engineered), a multimorbidity count from six chronic disease flags, age bins, and education buckets
3. **Descriptive Statistics** – Summary tables for the full sample and by gender, region, and insurance status
4. **Hypothesis Testing** – Independent-samples t-test comparing multimorbidity between high- and low-expenditure groups
5. **Logistic Regression** – Full-sample model and male/female subgroup models, with odds ratios and 95% confidence intervals
6. **LASSO Logistic Regression** – Regularized model with cross-validated regularization strength, used for feature selection and out-of-sample evaluation
7. **Visualization** – Spending-by-age line chart, high-cost probability by multimorbidity, regional choropleth map, LASSO coefficient plot, ROC curve, and confusion matrix

## Key Findings

- **Multimorbidity is the dominant driver of cost:** Respondents with more chronic conditions had significantly higher odds of being high-cost (OR ≈ 3.83, 95% CI 3.51–4.18 in the core logistic model), and the difference in multimorbidity between high- and low-expenditure groups was highly significant (t = 58.25, p < 0.001)
- **Age, sex, and socioeconomic status also matter:** Each additional year of age increased the odds of high spending (OR ≈ 1.02), women had higher odds than men (OR ≈ 1.53), and higher poverty category and more years of education were both modestly associated with higher odds
- **Regional differences exist:** The Northeast had the highest rate of high-expenditure individuals (55.2%), followed by the Midwest (54.3%), West (50.2%), and South (45.5%)
- **LASSO model performance:** Using multimorbidity, age, sex, poverty category, and education as predictors, the regularized model achieved 70% accuracy and an AUC-ROC of 0.75 on the held-out test set, with multimorbidity and age carrying the largest standardized coefficients

## Power BI Dashboard

`MEPS_DASHBOARD.pbix` provides an interactive view of the same dataset, allowing exploration of:
- Healthcare expenditure trends by age, gender, and region
- Chronic condition prevalence and its relationship to spending
- Insurance coverage breakdowns and poverty category comparisons

To open the dashboard, download `MEPS_DASHBOARD.pbix` and open it in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows only).

## Repository Structure
├── MEPS_notebook.ipynb      # Full Python analysis: cleaning, modeling, visualization

├── MEPS_DASHBOARD.pbix      # Power BI interactive dashboard

└── README.md                # Project documentation
## Tools and Libraries

- **Python:** pandas, numpy, statsmodels, scikit-learn, matplotlib, plotly, scipy
- **Statistical methods:** logistic regression, LASSO-regularized logistic regression, independent t-test, odds ratio/relative risk estimation
- **Visualization:** Power BI

## How to Run

1. Download the MEPS HC-243 data file (`h243.csv`) from AHRQ and place it in the project directory
2. Install dependencies:
   pip install pandas numpy matplotlib statsmodels plotly scikit-learn scipy

   3. Open and run `MEPS_notebook.ipynb` in Jupyter Notebook or JupyterLab
4. Open `MEPS_DASHBOARD.pbix` in Power BI Desktop to explore the dashboard

## Author

Sushmitha — M.S. Analytics & Artificial Intelligence, Northeastern University

## Data Citation

Agency for Healthcare Research and Quality (AHRQ). Medical Expenditure Panel Survey, 2022 Full-Year Consolidated Data File, HC-243. https://meps.ahrq.gov/
