# Bankrate Personal Loan Matching Analysis

## Background
Bankrate was founded in 1976 as Bank Rate Monitor, a print publisher for the banking industry. Our experience has fueled our reputation as the premier financial authority. When you visit Bankrate.com, the reviews, guides and educational content have been developed by leading personal finance experts. Bankrate’s product comparison tools, calculators and educational content help over 100 million consumers make smarter financial decisions each year. No matter where you are in your financial journey, Bankrate can help you reach your goals.

One area Bankrate specializes in is personal loans. Bankrate’s goal is to help match the best lending partner for each individual customer. To do that, we collect information about the customer to understand who would be the best fit. We want to maximize the likelihood someone will be approved for the loan at the best deal possible.

In this case, there are three lending partners (A, B, C). Each lender provides the same offer, but the payout per approval differs: A pays $250, B pays $350, and C pays $150. The dataset includes 100K customer applications with attributes intended to help match customers to lenders and increase approval rate and revenue per application.

## What This Analysis Does
The notebook focuses on three goals:
1. Explore variable relationships with approvability.
2. Compare lender approval behavior and rates.
3. Recommend lender matching to maximize expected revenue.

The full analysis is in `notebooks/analysis.ipynb`.

## How I Approached the Notebook (Step-by-Step)

### 1) Initial EDA
- Loaded the dataset from `data/loan_data.xlsx`.
- Verified unique customer count and checked missingness.
- Removed `Employment_Sector` due to missing values.
- Calculated current revenue based on actual approvals and lender payouts.
- Calculated and plotted approval rate by lender.

### 2) Feature Engineering
- Created two ratio features to reflect debt/income pressure:
  - `housing_ratio = Monthly_Housing_Payment / Monthly_Gross_Income`
  - `loan_income_ratio = Loan_Amount / Monthly_Gross_Income`
- One-hot encoded categorical columns (`Reason`, `Fico_Score_group`, `Employment_Status`).

### 3) Global Approval Model
- Trained a Random Forest classifier to predict approval (all lenders combined).
- Evaluated test accuracy and ranked feature importance.
- Key drivers across lenders: housing ratio, monthly gross income, FICO score, and loan income ratio.

### 4) Lender-Specific Models
- Trained separate Random Forest models for lenders A, B, and C.
- Compared feature importance rankings to identify differences in lender behavior.
- Noted that relative importance is meaningful within each model, not across models.

### 5) Distribution Checks by Lender
- Plotted distributions and confidence intervals for top features among approved loans.
- Observed no strong statistical differences in top features between lenders.
- Flagged potential future work (outliers or subgroup segmentation).

### 6) Revenue Optimization Simulation
- Split data 80/20 into train/test.
- Trained lender-specific models on the training set.
- Predicted approval probabilities for the test set per lender.
- Computed expected revenue per lender: `probability * payout`.
- Recommended the lender with the highest expected value for each test customer.
- Compared expected revenue of the optimized matching to current pairing and estimated revenue lift.

## Data Dictionary
- `User ID`: unique ID for the customer (string)
- `Application`: count of application (each row is 1 application) (int)
- `Reason`: purpose for requesting a loan (string)
- `Loan Amount`: loan value size (int)
- `FICO Score`: credit score (int)
- `FICO Score Group`: bucketed FICO categories (string)
- `Employment Status`: employment designation (string)
- `Employment Sector`: industry category (string)
- `Monthly Gross Income`: pre-tax income (int)
- `Monthly Housing Payment`: monthly housing cost (int)
- `Ever Bankrupt or Foreclose`: prior bankruptcy/foreclosure (bool)
- `Lender`: lending partner (string)
- `Approved`: whether approved (bool)
- `Bounty`: payout per approval (int)

## Project Structure
```
├── data/
│   └── comparison_df.xlsx
├── notebooks/
│   └── analysis.ipynb
├── pyproject.toml
├── uv.lock
├── .python-version
├── .gitignore
└── README.md
```

## How to Run
1. Install dependencies with uv:
```bash
uv sync
```

2. Open `notebooks/analysis.ipynb` and run all cells.

## Author
Letao (Julietta) Zhu
