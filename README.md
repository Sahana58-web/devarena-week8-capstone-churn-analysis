# Customer Churn Analysis: Where Do We Lose Customers?

Week 8 Capstone Project - end-to-end business analysis

## Project overview
**Business question:** Where do we lose customers, how much monthly revenue is at risk, and what retention plan should the company implement?

**Dataset:** `customer_churn.csv` - 500 customers, 9 columns (Tenure, MonthlyCharges, TotalCharges, Contract, PaymentMethod, PaperlessBilling, SeniorCitizen, Churn).

## Key findings
- 53 of 500 customers left (10.6%); all had 11 months or less of tenure.
- All 35 first-year month-to-month customers left; 18 of 48 first-year customers on 1 or 2 year contracts left.
- Churned customers represent 6,878 in monthly charges (12.1% of revenue), about 82,500 over 12 months.
- Payment method, paperless billing and senior status show no clear link to churn.
- TotalCharges is inconsistent with Tenure x MonthlyCharges (6.4% of rows match), so it was excluded.

## Techniques used
1. Hypothesis tests (chi-square, Fisher exact, Mann-Whitney, Bonferroni correction)
2. Risk segmentation (Critical, High, Stable)
3. Prediction models (logistic regression, 5-fold cross-validation)
4. Scenario analysis and break-even (based on stated assumptions)

## Recommendation
Start an early-life retention programme for new customers, beginning with the Critical segment, run a 60-day pilot with a control group, and scale only if the break-even is met. Full 180-day plan in `reports/`.

## Setup
```bash
pip install -r requirements.txt
```
1. Put `customer_churn.csv` in `data/` (saved as `raw_data.csv`).
2. Open `capstone_analysis.ipynb` (Google Colab or Jupyter) and run all cells from top to bottom.
3. Figures are saved in `figures/`, cleaned data in `data/cleaned_data.csv`.

## Folder structure
```
README.md
capstone_analysis.ipynb
requirements.txt
data/            raw_data.csv, cleaned_data.csv
reports/         executive_summary.pdf, technical_report.pdf
presentation/    business_presentation.pptx
figures/         charts used in the reports
```

## Testing and validation
- Data quality checks: rows, missing values, duplicates, invalid values, outliers (IQR), TotalCharges consistency.
- Models validated with 5-fold stratified cross-validation; Model A (with Tenure) ROC-AUC 0.98 is likely optimistic, Model B (sign-up information only) 0.69.
- Multiple-test correction applied to the 3 hypothesis tests.

## Limitations
Small sample (53 churn events); Tenure may be recorded differently for leavers; no programme cost or effect data, so financial results are scenarios.
