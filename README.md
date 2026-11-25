# Retail Banking: Trend Forecasting and Customer Analysis

A data science project on retail banking data. I cleaned and explored the data, built features for a loan prediction model, and forecast customer transaction activity for the next 6 months.

I completed this as part of a mentor-led internship project.

## What this project covers

1. **EDA and data cleaning** (`01_eda_and_data_cleaning.ipynb`)
2. **Feature engineering, pre-processing and forecasting** (`02_feature_engineering_and_forecasting.ipynb`)

## The data

- **Customers:** 5,000 customers with 10 columns (age, region, preferred channel, balance, products held, digital adoption score, credit card, loan taken).
- **Transactions:** 24,000 rows. This is the monthly transaction count for 1,000 customers, from January 2022 to December 2023.

The data files are not included in this repository. To run the notebooks, put `retail_banking_customers.csv` and `retail_banking_transactions.csv` in the same folder as the notebooks.

## Notebook 1: EDA and data cleaning

- Checked both files for missing values, duplicates and invalid values. None were found.
- Checked that the customer and transaction tables join correctly on customer ID.
- Found that only 1,000 of the 5,000 customers have transaction history. I did not fill the other 4,000 with zeros, because the file does not say they had no activity.
- Kept 4 months with zero transactions, because there was no proof they were errors.
- Made histograms, boxplots, a monthly trend chart and a correlation heatmap.

**Findings:** Average monthly transactions rise and fall in a wave, with a peak in May 2022 and a low in December 2022. The correlations between the customer features are all close to zero.

## Notebook 2: Features, split and forecast

- Created features such as transactions per product, balance per product and a flag for high-balance customers with low activity.
- Encoded region and channel with one-hot encoding. Scaled the numeric columns with StandardScaler.
- Chose `loan_taken` as the target. About 20% of customers have a loan, so the classes are imbalanced.
- Split the data 80/20 with stratification. The scaler was fitted on the training data only, to avoid data leakage.
- The 10 original columns became 23 input features plus the target.
- Forecast the next 6 months of average transactions per customer with an ARIMA(2,0,0) model. On the last 6 known months, the average error was 0.44 transactions per customer.

**Findings:** The model expects activity to keep falling until about April 2024, and then recover. 274 customers have a high balance but low activity, and the bank could try to re-engage them.

## Limitations

- The link between the features and `loan_taken` is very weak, so a loan prediction model may not be very accurate.
- The forecast uses only 24 months of data. Python showed a convergence warning for the final model.
- Account opening dates are not in the data, so customer tenure could not be calculated.

## Tools

Python, pandas, NumPy, matplotlib, seaborn, scikit-learn, statsmodels, Jupyter Notebook

## Repository structure

````
notebooks/
  01_eda_and_data_cleaning.ipynb
  02_feature_engineering_and_forecasting.ipynb
README.md
````
