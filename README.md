# Bank_Loan_Report
---
## Project Overview
A Report to monitor and assess our bank's lending activities and performance which aims to provide insights into key loan-related metrics and their changes over time.

### Data Source
Financial Loan: The primary dataset used for this analysis is the "financial_loan.csv" file, containing detailed information about each loan made by the bank.

### Tools Used
- **Microsoft SQL Server**
- **Tableau Desktop** - For Creating Report

### Data Cleaning/Preparation
  In the initial data preparation phase, I performed the following tasks:
 - Data Loading and Inspection with the **MS SQLServer**
   - It was used to first import and edit the data
   - The "emp_title" had a VARCHAR(50) but was modified to VARCHAR(100) to contain more texts.
   - The "id" was ticked to be the *Primary Key*
   - Any/All fields having NVARCHAR were modified to VARCHAR
   - The "total_payment" had SMALLINT but was reset to INT to contain maximum values
   - The "loan_amount" was also set to INT

  ### Exploratory Data Analysis
EDA involved exploring the financial loan data to answer key questions, such as:

A) KPIs
  1. What's the *Total Loan Applications* using the following:
     - Month-to-Date loan applications (MTD)
     - Previous Month-to-Month (PMTD) to track changes.
  2. *Total Funded Amount* using:
       - Month-to-Date total funded amount (MTD)
       - Previous Month-to-Month (PMTD) to track metric changes
  3. *Total Amount Received* using:
      - Month-to-Date (MTD) to know our total amount received
      - Previous Month-to-Month (PMTD) to track metric changes
  4. *Average Interest Rate* Using:
      - Month-to-Date(MTD) to know our average Interest Rate
       - Previous Month-to-Month (PMTD) to track metric changes
  5. *Average Debt_to-Income_Ratio*(DTI): Evaluating the average DTI for our borrowers helps us 
     gauge their financial health. 
      - Month-to-Date (MTD) Average DTI
       - Previous Month-to-Month (PMTD) to track metric changes

B) What are the Good Loan Vs Bad Loan KPIs?

C) What is the Loan Status Overall?

### Data Analysis
As stated earlier, the analysis were done strictly using **MS SQL Server**. Below are the analysis:
1. **Total Loan Applications** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMDT)*
- Total Loan Applications
```SQL 
SELECT
      COUNT (id) AS Total_Application
FROM Bank_Loan_Data;
```
- Month-to-Date (MTD) Total Loan Applications
```SQL
SELECT
      COUNT (id) AS MTD_Total_loan_Applications
FROM Bank_Loan_Data
WHERE
    MONTH (issue_date) = 12
	AND YEAR (issue_date) = 2021;
```
- Previous Month-to-Month (PMTD)
```SQL
SELECT
      COUNT (id) AS PMTD_Total_Loan_Applications
FROM Bank_Loan_Data
WHERE
    MONTH (issue_date) = 11
	AND YEAR (issue_date) = 2021;
```
Image for All Loan Applications, gotten from Tableau.

![Total_loan_apps](https://github.com/user-attachments/assets/b6d0cdc5-6d71-4339-aa7d-389be47222fc)

---

2. **Total Funded Amount** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMDT)*
- Total Funded Amount
```SQL
SELECT SUM(loan_amount) loan_amount
FROM
    Bank_Loan_Data;
```
- Month-to-Date (MTD)
```SQL
SELECT
    SUM (loan_amount) AS MTD_Total_Funded_Amount
FROM
    Bank_Loan_Data
WHERE
    MONTH (issue_date) = 12
 AND YEAR (issue_date) = 2021;
```
- Previous Month-to-Date (PMTD)
```SQL
SELECT
      SUM (loan_amount) AS PMTD_Total_Funded_Amount
FROM
    Bank_Loan_Data
WHERE
    MONTH (issue_date) = 11
AND YEAR (issue_date) = 2021;
```
Image for All Funded Loans

![Total_Funded Amount](https://github.com/user-attachments/assets/8c79dd20-1452-41dd-87ae-05169261e398)

---
3.  **Total Amount Received** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMDT)*
- Total Amount Received
```SQL
SELECT
     SUM (total_payment) AS Total_Amount_Received
FROM
   Bank_Loan_Data;
```
- Month-to-Date (MTD)
```SQL
SELECT
     SUM (total_payment) AS MTD_Total_Amount_Received
FROM
    Bank_Loan_Data
WHERE
    MONTH (issue_date) = 12
AND YEAR (issue_date) = 2021;
```
- Previous Month-to-Date PMTD)
```SQL
SELECT
     SUM (total_payment) AS PMTD_Total_Amount_Received
FROM
    Bank_Loan_Data
WHERE
    MONTH (issue_date) = 11
AND YEAR (issue_date) = 2021;
```
Image For All Amount Received

![Total_Amount_Received](https://github.com/user-attachments/assets/49022554-78b9-4fe4-92ff-bc5a48399202)

---

4. **Average Interest Rate** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMDT)*
- Total Avg Int Rate
```SQL
Average Interest Rat
SELECT
     ROUND (AVG (int_rate), 4) * 100 AS Avg_Interest_Rate
FROM
    Bank_Loan_Data;
```
- Month-to-Date (MTD)
```SQL
SELECT
     ROUND (AVG (int_rate), 4) * 100 AS MTD_Avg_Interest_Rate
FROM
    Bank_Loan_Data
WHERE
    MONTH (issue_date) = 12
  AND YEAR (issue_date) = 2021;
``` 
- Previous Month-to-Date (PMTD)
```SQL
SELECT
     ROUND (AVG (int_rate), 4) * 100 AS PMTD_Avg_Interest_Rate
FROM
   Bank_Loan_Data
WHERE
    MONTH (issue_date) = 11
  AND YEAR (issue_date) = 2021;
```
Image for All Average Int Rates

![Avg_Int_Rate](https://github.com/user-attachments/assets/330e2bac-417e-434b-b509-7f8d6f8e8839)

---

5. **Average Debt-to-Income Ratio** with respect to *Month-to-Date (MTD)* and *Previous Month-to-Date (PMDT)*
- Average DTI
```SQL
SELECT
     ROUND (AVG (dti), 4) * 100 AS MTD_Avg_DTI
FROM
    Bank_Loan_Data;
```
- Month-to-Date (MTD)
```SQL
SELECT
      ROUND (AVG (dti), 4) * 100 AS MTD_Avg_DTI
FROM
    Bank_Loan_Data
WHERE
      MONTH (issue_date) = 12
  AND YEAR (issue_date) = 2021;
```
- Previous Month-to-Date (PMTD)
```SQL
SELECT
     ROUND (AVG (dti), 4) * 100 AS PMTD_Avg_DTI
FROM
    Bank_Loan_Data
WHERE
      MONTH (issue_date) = 11
  AND YEAR (issue_date) = 2021;
```
Image of All Avg DTIs

![Avg_DTIs](https://github.com/user-attachments/assets/2d8101f5-aaa2-4e92-90e7-9d721b2cc4a8)
