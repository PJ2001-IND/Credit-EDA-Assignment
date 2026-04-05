# 💳 Credit EDA Case Study — Home Credit Default Risk

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-EDA-150458?style=flat-square&logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualisation-4C72B0?style=flat-square)
![License](https://img.shields.io/badge/License-Academic-lightgrey?style=flat-square)

> A comprehensive **Exploratory Data Analysis (EDA)** case study on Home Credit's loan application dataset — analysing **current and previous credit applications** to identify the patterns and risk indicators that distinguish loan defaulters from repayers. The analysis spans 24 figures across both univariate and bivariate analyses, Spearman correlation heatmaps, and a merged dataset study across two tables.

---

## 📌 Problem Statement

Loan providers face a significant challenge when assessing applicants with insufficient or no credit history — they risk either rejecting creditworthy applicants or approving those likely to default. Home Credit uses alternative data (income, employment, region, asset information) to make lending decisions. This case study applies EDA to:

- **Identify patterns that indicate a client's difficulty in repaying a loan**
- **Understand the driving variables that distinguish TARGET = 1 (defaulter) from TARGET = 0 (repayer)**
- **Analyse previous application behaviour to understand how past loan outcomes relate to current default risk**

The goal is to ensure that creditworthy applicants are not rejected and that risky applicants are correctly flagged.

---

## 🎯 Objectives

- Perform structured EDA on `application_data.csv` — the current loan application dataset
- Clean both datasets: drop high-null columns (>30% missing), fill remaining nulls, remove irrelevant flags
- Bin continuous variables (`AMT_INCOME_TOTAL`, `AMT_CREDIT`) into meaningful ranges for analysis
- Split the application data into **TARGET = 0** (repayers) and **TARGET = 1** (defaulters) and analyse separately
- Compute **Spearman correlation matrices** for both target groups independently
- Read and clean `previous_application.csv`, then **merge it with the application data** on `SK_ID_CURR`
- Produce 24 labelled figures covering income, credit, contract type, organisation type, education, and loan purpose

---

## 📂 Dataset

### 1. application_data.csv — Current Loan Applications

| Property | Detail |
|---|---|
| Source | Home Credit Group — loan application records |
| Records | ~307,511 applications |
| Features | 122 columns (original) |
| Target Variable | `TARGET` — 1: payment difficulties (defaulter), 0: repayer |
| Class Imbalance | TARGET = 0 significantly outnumbers TARGET = 1 (~11.4:1 ratio) |

### Key Features Used in Analysis

| Feature | Description |
|---|---|
| `TARGET` | Binary default indicator — 1: defaulter, 0: repayer |
| `SK_ID_CURR` | Unique application ID — used for merging |
| `CODE_GENDER` | Applicant gender (F / M / XNA → remapped to F) |
| `AMT_INCOME_TOTAL` | Total annual income (binned into `AMT_INCOME_RANGE`) |
| `AMT_CREDIT` | Loan credit amount (binned into `AMT_CREDIT_RANGE`) |
| `AMT_ANNUITY` | Loan annuity amount (null filled with median) |
| `NAME_CONTRACT_TYPE` | Cash loans vs Revolving loans |
| `NAME_INCOME_TYPE` | Working / Commercial associate / Pensioner / State servant / Unemployed |
| `NAME_EDUCATION_TYPE` | Education level of applicant |
| `NAME_FAMILY_STATUS` | Marital status |
| `ORGANIZATION_TYPE` | Employer organisation type (XNA rows dropped) |
| `DAYS_BIRTH` | Age in days (negative) |
| `DAYS_EMPLOYED` | Employment duration in days |

### 2. previous_application.csv — Previous Loan Applications

| Property | Detail |
|---|---|
| Source | Home Credit Group — historical loan applications |
| Records | ~1,670,214 previous applications |
| Features | 37 columns (after dropping >30% null columns) |
| Key Variable | `NAME_CASH_LOAN_PURPOSE` — purpose of previous loan (XNA and XAP rows dropped) |
| Merge Key | `SK_ID_CURR` — inner join with application_data |

### 3. columns_description.csv — Data Dictionary

| Property | Detail |
|---|---|
| Purpose | Describes all 122 columns in application_data and previous_application |
| Usage | Reference for feature understanding and analysis planning |

---

## 🔬 Methodology

```
application_data.csv (307,511 rows, 122 columns)
   │
   ▼
Data Cleaning — application_data
   │   ├── Drop columns with >30% null values
   │   ├── Fill AMT_ANNUITY nulls with median
   │   ├── Drop rows with >30% null values across columns
   │   ├── Drop unwanted flag columns:
   │   │     FLAG_MOBIL, FLAG_EMP_PHONE, FLAG_WORK_PHONE, FLAG_CONT_MOBILE,
   │   │     FLAG_PHONE, FLAG_EMAIL, CNT_FAM_MEMBERS, REGION_RATING_CLIENT,
   │   │     REGION_RATING_CLIENT_W_CITY, DAYS_LAST_PHONE_CHANGE,
   │   │     FLAG_DOCUMENT_2 through FLAG_DOCUMENT_21
   │   ├── Replace CODE_GENDER = 'XNA' with 'F'
   │   └── Drop rows where ORGANIZATION_TYPE = 'XNA'
   │
   ▼
Feature Engineering — application_data
   │   ├── Bin AMT_INCOME_TOTAL → AMT_INCOME_RANGE (21 bins: 0–25K to 500K+)
   │   └── Bin AMT_CREDIT → AMT_CREDIT_RANGE (17 bins: 0–150K to 900K+)
   │
   ▼
Target Split
   │   ├── target0_df1 → TARGET = 0 (repayers)
   │   └── target1_df1 → TARGET = 1 (defaulters)
   │
   ▼
Univariate Analysis (Figures 1–8)
   │   ├── FIG 1:  Income range distribution — TARGET 0 by gender
   │   ├── FIG 2:  Income type distribution — TARGET 0 by gender
   │   ├── FIG 3:  Contract type distribution — TARGET 0 by gender
   │   ├── FIG 4:  Organisation type distribution — TARGET 0
   │   ├── FIG 5:  Income range distribution — TARGET 1 by gender
   │   ├── FIG 6:  Income type distribution — TARGET 1 by gender
   │   ├── FIG 7:  Contract type distribution — TARGET 1 by gender
   │   └── FIG 8:  Organisation type distribution — TARGET 1
   │
   ▼
Correlation Analysis (Figures 9–10)
   │   ├── FIG 9:  Spearman correlation heatmap — TARGET 0 (RdYlGn palette)
   │   └── FIG 10: Spearman correlation heatmap — TARGET 1 (RdYlGn palette)
   │
   ▼
Numerical Bivariate Analysis (Figures 11–16)
   │   ├── FIG 11: AMT_INCOME_TOTAL distribution — TARGET 0 (boxplot, log scale)
   │   ├── FIG 12: AMT_CREDIT distribution — TARGET 0 (boxplot, log scale)
   │   ├── FIG 13: AMT_ANNUITY distribution — TARGET 0 (boxplot, log scale)
   │   ├── FIG 14: AMT_INCOME_TOTAL distribution — TARGET 1 (boxplot, log scale)
   │   ├── FIG 15: AMT_CREDIT distribution — TARGET 1 (boxplot, log scale)
   │   └── FIG 16: AMT_ANNUITY distribution — TARGET 1 (boxplot, log scale)
   │
   ▼
Multivariate Analysis (Figures 17–20)
   │   ├── FIG 17: Credit amount vs Education type (TARGET 0) hue: Family Status
   │   ├── FIG 18: Income amount vs Education type (TARGET 0) hue: Family Status
   │   ├── FIG 19: Credit amount vs Education type (TARGET 1) hue: Family Status
   │   └── FIG 20: Income amount vs Education type (TARGET 1) hue: Family Status
   │
   ▼
previous_application.csv (1,670,214 rows, 37 cleaned columns)
   │   ├── Drop columns with >30% null values
   │   └── Drop rows where NAME_CASH_LOAN_PURPOSE = 'XNA' or 'XAP'
   │
   ▼
Merge: application_data ⨝ previous_application (inner join on SK_ID_CURR)
   │   ├── Rename conflicting columns with _PREV suffix
   │   └── Drop remaining flag / timing columns
   │
   ▼
Merged Dataset Analysis (Figures 21–24)
       ├── FIG 21: Contract status distribution by loan purpose (log scale)
       ├── FIG 22: Loan purpose distribution by TARGET (log scale)
       ├── FIG 23: Previous credit amount vs loan purpose — hue: income type
       └── FIG 24: Previous credit amount vs housing type — hue: TARGET
```

---

## 📊 Key Analyses Performed

| Analysis Type | Figures | Focus |
|---|---|---|
| Univariate Categorical | FIG 1–8 | Income range, income type, contract type, organisation type — split by TARGET |
| Correlation (Spearman) | FIG 9–10 | Feature-level correlations within TARGET 0 and TARGET 1 groups separately |
| Univariate Numerical | FIG 11–16 | Income, credit, and annuity amount distributions — split by TARGET |
| Multivariate | FIG 17–20 | Credit & income vs education type — stratified by family status and TARGET |
| Merged Dataset | FIG 21–24 | Loan purpose, contract status, previous credit vs current default behaviour |

> 📝 *Refer to `CREDIT_EDA_ASSIGNMENT_SOLUTION.ipynb` for all 24 figures, full cleaning steps, Spearman correlation tables, and merged dataset analysis.*

---

## 💡 Key Insights

- **Imbalanced dataset** — TARGET = 0 (repayers) outnumber TARGET = 1 (defaulters) by ~11.4:1, requiring careful metric selection for any downstream modelling
- **Income type matters** — Working professionals dominate both groups, but the proportion of defaulters is higher among those in certain organisation types and income brackets
- **Cash loans are the dominant contract type** for both repayers and defaulters, though Revolving loans show different risk profiles
- **Higher credit amounts do not strongly predict default** — the distributions of AMT_CREDIT for TARGET 0 and TARGET 1 are broadly similar, pointing to behavioural rather than purely financial risk factors
- **Education and family status interact** — higher education levels correlate with larger credit amounts, but this does not uniformly reduce default risk
- **Previous loan purpose links to current default** — specific loan purposes (repairs, buying a garage, urgent needs) appear more frequently among merged records with TARGET = 1
- **Housing type** influences previous credit amounts, with house/apartment owners showing different credit patterns relative to rented or parental housing

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.8+ | Core programming language |
| Pandas | Data loading, cleaning, binning, merging, null handling |
| NumPy | Numerical operations and array masking for correlation |
| Matplotlib / Seaborn | 24-figure visualisation suite — countplots, boxplots, heatmaps, barplots, distplots |
| Jupyter Notebook | Interactive EDA development environment |

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the Notebook

```bash
# Clone the repository
git clone https://github.com/PJ2001-IND/Credit-EDA-Assignment.git

# Navigate to the project directory
cd Credit-EDA-Assignment

# Launch Jupyter Notebook
jupyter notebook CREDIT_EDA_ASSIGNMENT_SOLUTION.ipynb
```

> ⚠️ **Note:** `application_data.csv` (~158 MB) and `previous_application.csv` (~386 MB) are stored via **Git LFS**. Run `git lfs pull` after cloning to download the full datasets before running the notebook.

---

## 📁 Project Structure

```
📦 Credit-EDA-Assignment
 ┣ 📓 CREDIT_EDA_ASSIGNMENT_SOLUTION.ipynb   # Full EDA pipeline — 66 cells, 24 figures
 ┣ 📄 application_data.csv                   # Current loan applications (~307K records, 122 features)
 ┣ 📄 previous_application.csv               # Previous loan history (~1.67M records)
 ┣ 📄 columns_description.csv               # Data dictionary for all features
 ┣ 📄 requirements.txt                       # Python dependencies
 ┗ 📄 README.md                              # Project documentation
```

---

## 🔭 Future Scope

- Build a **credit default prediction model** using the cleaned merged dataset — Logistic Regression, Random Forest, or XGBoost with proper handling of the class imbalance (SMOTE / class weights)
- Apply **SHAP values** to interpret which features drive default risk at the individual applicant level
- Incorporate **Weight of Evidence (WoE) and Information Value (IV)** analysis for scorecard development
- Extend EDA to the `installments_payments.csv` and `bureau.csv` datasets from the full Home Credit challenge
- Deploy a **risk scoring API** using FastAPI that returns a default probability for a new applicant
- Build an interactive **Power BI / Tableau dashboard** for portfolio-level credit risk monitoring

---

## 👤 Author

**Praasuk Jain**
- GitHub: [@PJ2001-IND](https://github.com/PJ2001-IND)
- LinkedIn: [praasuk-jain](https://www.linkedin.com/in/praasuk-jain-425b6b1a3/)

---

> ⭐ If you found this project useful, consider giving it a star!
