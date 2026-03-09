SEC Regulatory Scrutiny & IPO Outcomes — IV Estimation

Causal inference project estimating the effect of SEC review intensity on IPO outcomes using instrumental variables (IV2SLS).

Overview
When a company files for an IPO, the SEC assigns a reviewer who may raise issues requiring amendments to the filing. But does stricter SEC scrutiny cause more amendments, or do problematic filings attract both more scrutiny and more amendments simultaneously (endogeneity)?
This project addresses that question using Two-Stage Least Squares (IV2SLS), instrumenting SEC reviewer strictness with a leave-one-out (LOO) measure that captures each reviewer's average behaviour on other filings — isolating exogenous variation in scrutiny intensity.
Research Question
Does stricter SEC review causally increase the number of IPO filing amendments and the probability of regulatory investigation?
Dataset

Source: SEC EDGAR IPO filing data (sec_reviewer_data.csv)
Observations: 62,988 firm-filing observations (after cleaning)
Key variables:

number_issues — endogenous variable (SEC issues raised per filing)
instrument_strictness_loo — leave-one-out reviewer strictness (instrument)
Outcomes: amendment (binary), number_amendments (count), investigation (binary)
Controls: log_float, IS_ACCEL_FILER, IS_IN_SP500, IS_IN_RUSSELL_2000, IS_IN_NASDAQ_COMPOSITE



Methodology
Identification strategy — Leave-One-Out Instrument:
For each filing assigned to reviewer r, the instrument is:
strictness_loo(r) = [sum of issues on other filings by r] / [count of other filings by r - 1]

Relevance: Reviewer's behaviour on other cases strongly predicts issues raised on this filing
Exclusion restriction: Reviewer's strictness on unrelated filings affects IPO outcomes only through the number of issues raised on this specific filing

Estimation (linearmodels.iv.IV2SLS, robust SE):
Stage 1:  number_issues = a + b * strictness_loo + c * Controls + e
Stage 2:  outcome       = a + d * number_issues_hat + c * Controls + e
Results
First Stage — Instrument Validity
DiagnosticValuePartial F-statistic5,994.9Partial R-squared0.0997Instrument coefficient0.966 (t = 77.4)
The instrument is extremely strong (F >> 10), ruling out weak instrument concerns.
Second Stage — IV Estimates
OutcomeCoefficient on number_issuesT-statP-valueamendment (binary)+0.013825.00.000number_amendments (count)+0.03128.40.000investigation (binary)-0.0004-3.00.003
Key finding: Each additional SEC issue raised causally increases the probability of filing an amendment by 1.4 percentage points and the expected number of amendments by 0.031. Stricter scrutiny slightly reduces the probability of a formal investigation, suggesting that early issue resolution substitutes for downstream enforcement.
Repository Structure
├── Group_2_Assignment_2.ipynb    # Full pipeline: data cleaning, LOO instrument, IV2SLS, diagnostics
├── sec_reviewer_data.csv         # SEC filing data (not included — proprietary)
└── README.md
Requirements
pandas
numpy
matplotlib
statsmodels
linearmodels
Install with:
bashpip install pandas numpy matplotlib statsmodels linearmodels
References

Angrist, J. D., & Pischke, J. S. (2009). Mostly Harmless Econometrics. Princeton University Press.

Author
Leonardo Trapani — Empirical Methods for Finance, Erasmus School of Economics, 2025
