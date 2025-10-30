# Loan Approval Analysis Project

## Overview
This project analyzes loan approval patterns across different lenders and develops a matching model to optimize revenue by better pairing customers with lenders. The analysis includes exploratory data analysis (EDA), random forest classifiers to predict approval likelihood, and a revenue optimization model.

## Project Structure
```
├── data/               # Data files
├── notebooks/         # Jupyter notebooks
│   └── analysis.ipynb # Main analysis notebook
├── src/              # Source code
└── requirements.txt  # Project dependencies
```

## Key Features
- Exploratory Data Analysis of loan approval patterns
- Feature importance analysis using Random Forest
- Lender-specific approval prediction models
- Revenue optimization through customer-lender matching

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd rv_interview
```

2. Create and activate a virtual environment (optional but recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

3. Install the required packages:
```bash
pip install -r requirements.txt
```

## Usage
The main analysis is contained in `notebooks/analysis.ipynb`. Open this notebook to view the complete analysis and results.

## Results
- Identified key features affecting loan approval
- Developed separate models for each lender's approval patterns
- Potential revenue increase through optimized matching

## Author
Letao (Julietta) Zhu