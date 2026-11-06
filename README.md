# Credit Risk Analysis: SQL to Power BI

An end-to-end analysis of loan default risk. The raw credit risk dataset is cleaned and queried with SQL, then visualised in an interactive Power BI dashboard.

## Dataset

`data/credit_risk_dataset.csv`: 32,581 loan records with 12 columns.

| Column | Description |
|---|---|
| person_age | Borrower age |
| person_income | Annual income |
| person_home_ownership | RENT / OWN / MORTGAGE / OTHER |
| person_emp_length | Employment length (years) |
| loan_intent | Purpose of the loan (personal, education, medical, etc.) |
| loan_grade | Loan grade (A to G) |
| loan_amnt | Loan amount |
| loan_int_rate | Interest rate (%) |
| loan_status | 1 = default, 0 = non-default |
| loan_percent_income | Loan amount as a share of income |
| cb_person_default_on_file | Previous default on file (Y/N) |
| cb_person_cred_hist_length | Credit history length (years) |

About 21.8% of loans in the raw data are defaults.

### Data quality issues found
- Missing values: `person_emp_length` (895) and `loan_int_rate` (3,116)
- Outliers: ages up to 144, employment length up to 123 years, income up to 6,000,000

## Workflow

1. **Load** the CSV into MySQL
2. **Clean** the data with SQL (handle nulls and unrealistic values)
3. **Analyse** with SQL queries (default rate by grade, home ownership, loan intent, interest rate)
4. **Visualise** in Power BI (`powerbi/sql_to_powerbi.pbix`)

## Dashboard

The Power BI report includes:
- KPI cards: Total Loans, Total Defaults, Default Rate %, Total Loan Amount, Avg Loan Amount, Avg Income
- Default rate by loan grade, home ownership and interest rate
- Loan distribution by home ownership
- Slicers for loan grade, loan intent and home ownership

<!-- Add a dashboard screenshot here: ![Dashboard](images/dashboard.png) -->
   ![Credit Risk Dashboard](dashboard.png)
   *Dashboard built on a 170-row sample extracted with SQL from the full dataset.*<img width="1443" height="809" alt="dashboard png" src="https://github.com/user-attachments/assets/095f9bb9-1307-4e5e-9f0d-46ab834c13a3" />


## Repository structure

```
├── data/        raw dataset (CSV)
├── sql/         cleaning and analysis queries
├── powerbi/     Power BI report (.pbix)
└── README.md
```

## Tools
MySQL, Power BI Desktop

## Key insights
-   - Default rate rises as loan grade worsens, from 0.37 (grade A) to 0.82 (grade E).
   - Renters have the highest default rate (0.64); homeowners the lowest (0.22).
   - Renters make up most of the loans in the dataset (111 of 170).
   - Very high interest-rate buckets show 100% default, but each has very few loans.
