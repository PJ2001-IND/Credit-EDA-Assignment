# 🏦 Credit Risk — Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat-square&logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualisation-4C72B0?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)

> A comprehensive Exploratory Data Analysis on real-world **credit loan application data** to uncover patterns of loan default risk — helping financial institutions make smarter, data-driven lending decisions while minimising bad debt and avoiding rejection of creditworthy applicants.

---

## 📌 Problem Statement

Banks and lending institutions face two critical risks when evaluating loan applications:

1. **Approving loans for applicants likely to default** — leading to financial loss
2. **Rejecting applications from creditworthy customers** — leading to missed business

This project uses EDA to identify the **key drivers of loan default** across applicant demographics, financial history, and previous credit behaviour — providing a data foundation for building a robust credit risk model.

---

## 🎯 Objective

- Perform deep EDA on both current and previous loan application data
- Identify patterns that differentiate **defaulters** from **non-defaulters**
- Handle missing values, outliers, and data imbalance appropriately
- Extract actionable business insights about high-risk applicant profiles
- Build a clean, analysis-ready dataset for downstream credit risk modelling

---

## 📂 Dataset

| File | Description |
|---|---|
| `application_data.csv` | Current loan application data — applicant demographics, income, employment, loan amount, and repayment history |
| `previous_application.csv` | Historical loan applications by the same clients — previous loan amounts, status, and credit behaviour |
| `columns_description.csv` | Data dictionary describing all features across both datasets |

### Key Feature Categories in `application_data.csv`:
- **Demographics**: Age, gender, family status, number of children, education, occupation
- **Financial**: Income, loan amount, annuity, credit amount, goods price
- **Employment**: Employment type, years employed, years in current job
- **Credit Bureau**: Number of previous enquiries, days since last overdue, credit history length
- **Target Variable**: `TARGET` — 1 = Payment difficulties (defaulter), 0 = All payments on time

---

## 🔬 Analysis Pipeline

```
application_data.csv + previous_application.csv
              │
              ▼
Data Overview & Quality Check
              │   ├── Shape, dtypes, null percentages
              │   ├── Columns with >40% missing values → dropped/imputed
              │   └── Duplicate check
              │
              ▼
Univariate Analysis
              │   ├── TARGET distribution (imbalance check)
              │   ├── Income, loan amount, age distributions
              │   └── Categorical variable frequency plots
              │
              ▼
Bivariate Analysis
              │   ├── Default rate by income bracket
              │   ├── Default rate by employment type
              │   ├── Default rate by education level
              │   ├── Loan amount vs income ratio for defaulters
              │   └── Gender, age group, and family status vs default
              │
              ▼
Previous Application Analysis
              │   ├── Merge with current applications on client ID
              │   ├── Previous approval/refusal rates for defaulters
              │   └── Previous loan purpose vs current default patterns
              │
              ▼
Correlation & Outlier Analysis
              │   ├── Correlation heatmap of numerical features
              │   ├── Outlier detection (IQR / box plots)
              │   └── Key risk indicator identification
              │
              ▼
Business Insights & Risk Profiles
```

---

## 💡 Key Insights

- **Imbalanced target**: Only ~8% of applicants are defaulters — raw accuracy would be misleading; any downstream model must account for this imbalance
- **Income matters, but not alone**: Low-income applicants default more, but high loan-to-income ratios in any bracket are a stronger risk signal
- **Employment type is highly predictive**: Unemployed applicants and those on maternity leave show significantly higher default rates
- **Previous application history**: Clients previously refused by the bank are more likely to default if approved in the current cycle
- **Age effect**: Younger applicants (20–30) show higher default rates; risk decreases steadily with age
- **Education correlation**: Applicants with lower secondary education default at a higher rate than graduates

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core programming language |
| Pandas | Data loading, cleaning, and analysis |
| NumPy | Numerical operations |
| Matplotlib | Custom visualisations |
| Seaborn | Statistical plots and heatmaps |
| Jupyter Notebook | Interactive analysis environment |

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
jupyter notebook "CREDIT EDA ASSIGNMENT SOLUTION.ipynb"
```

---

## 📁 Project Structure

```
📦 Credit-EDA-Assignment
 ┣ 📓 CREDIT EDA ASSIGNMENT SOLUTION.ipynb   # Full EDA notebook
 ┣ 📄 application_data.csv                   # Current loan application dataset
 ┣ 📄 previous_application.csv               # Historical application dataset
 ┣ 📄 columns_description.csv                # Data dictionary for all features
 ┗ 📄 README.md                              # Project documentation
```

---

## 🔭 Future Scope

- Build a **credit risk classification model** (Logistic Regression, Random Forest, XGBoost) using the insights from this EDA as feature selection guidance
- Apply **SMOTE** or class weighting to handle the 92:8 target imbalance
- Create an interactive **risk dashboard** using Streamlit or Power BI for loan officers
- Incorporate **bureau data** (external credit scores) as additional features for improved prediction

---

## 👤 Author

**Praasuk Jain**
- GitHub: [@PJ2001-IND](https://github.com/PJ2001-IND)
- LinkedIn: [praasuk-jain](https://www.linkedin.com/in/praasuk-jain-425b6b1a3/)

---

## 📄 License

This project is licensed under the MIT License.

---

> ⭐ If you found this project useful, consider giving it a star!
