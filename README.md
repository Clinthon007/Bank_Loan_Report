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
     - Current Month-to-Date loan applications (MTD)
     - Previous Month-to-Month (PMTD) to track changes.
  2. *Total Funded Amount* using:
       - Current Month-to-Date total funded amount (MTD)
       - Previous Month-to-Month (PMTD) to track metric changes
  3. *Total Amount Received* using:
      - Current Month-to-Date (MTD) to know our total amount received
      - Previous Month-to-Month (PMTD) to track metric changes
  4. *Average Interest Rate* Using:
      - Current Month-to-Date(MTD) to know our average Interest Rate
       - Previous Month-to-Month (PMTD) to track metric changes
  5. *Average Debt_to-Income_Ratio*(DTI): Evaluating the average DTI for our borrowers helps us 
     gauge their financial health. 
      - Current Month-to-Date (MTD) Average DTI
       - Previous Month-to-Month (PMTD) to track metric changes
- *Note: *Both Current and Previous Months calculations would help get the Month-over-Month (MoM) trends*
 
B) What are the Good Loan Vs Bad Loan?

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

---
### B. Good Loans Vs Bad Loans Issued
In order to evaluate the performance of the bank's lending activities and assess the quality of the loan, there is need to create a comprehensive report that distinguishes between **'Good Loans'** and **'Bad Loans'** based on specific loan status criteria *( Good Loans Applications Percentage; Good Loan Applications; Good Loan Funded Amount; Good Loan Total Received Amount; Bad Loan Application Percentage; Bad Loan Applications; Bad Loan Funded Amount; Bad Loan Total Received Amount)*

- ### Good Loans Issued (Good Debt)
 This is a debt given to borrowers who at the end of a specified period meet up with the return payment. It's seen as good debt because borrowers profit from it, at the same time are able to pay the bank back on time or specified time rate. All Good Loans are generally calculated using the "Fully Paid" and "Current" columns/fields.

i. Good Loan Percentage
```SQL
SELECT 
     (COUNT (CASE WHEN
             loan_status = 'Fully Paid'
          OR loan_status = 'Current'
             THEN id
             END) * 100) 
                /
      COUNT (id) AS Good_loan_percentage
FROM
    Bank_Loan_Data;
```
ii. Good Loan Appications
```SQL
SELECT
     COUNT (id) AS Good_loan_Applications
FROM
    Bank_Loan_Data
WHERE
    (loan_status = 'Fully Paid'
  OR loan_status = 'Current')
```
iii. Good Loan Funded Amount
```SQL
SELECT
     SUM (loan_amount) AS Good_loan_Funded_Amount
FROM
    Bank_Loan_Data
WHERE
    (loan_status = 'Fully Paid'
  OR loan_status = 'Current');
```
iv. Good Loan Total Amount Received
```SQL
SELECT
     SUM (total_payment) AS Good_Loan_Received_Amount
FROM
    Bank_Loan_Data
WHERE
     (loan_status = 'Fully Paid'
   OR loan_status = 'Current');
```
![Good_Loans_Issued](https://github.com/user-attachments/assets/9bece66f-b67b-4118-bc61-a543b4e8c5a6)

With the above, it's seen that the total percentage of loans that were given out by the bank to borrowers has high return/refund rate of **86%**. Meaning many borrowers met up with their payment and on time (Fully Paid), while some are still meeting up with theirs and also clearing their debts as suppossed to (Current). Also, many borrowers applied for good loans which is on a positive note or a good thing for the bank, and having amounted to **33.2k**.  Also, Good loans funded by the bank to borrowers was on a high note of **$370.2M**. Again, Amount repaid by borrowers were on a positive note as well, and amounting to **$435.8M** returned. Seeing all these, it's with pleasure that the bank has made a huge profit of **$65.6M** within that period.

---
- ### Bad Loans Issued (Bad Debt)
 This a loan or debt given to borrowers whom at the end of a specified period could not meet up with repayment of the debt, either because they cannot afford to repay or they may have died or something else. These borrowers tend to incur more debt over such period in this scenerio since such debt does not favour/profit him. All Bad Debts are generally calculated using the "Charged Off" column/field.
i. Bad Loan Percentage
```SQL
SELECT 
      (COUNT (CASE WHEN
       loan_status = 'Charged Off'
       THEN id
       END) * 100.0) 
            /
       COUNT (id) AS Bad_loan_percentage
FROM
    Bank_Loan_Data;
```

ii. Bad Loan Applications
```SQL
SELECT
     COUNT (id) AS Bad_Loan_Application
FROM
    Bank_Loan_Data
WHERE
     loan_status = 'Charged Off';
```

iii. Bad Loan Funded Amount
```SQL
SELECT
      SUM (loan_amount) AS Bad_Loan_Funded_Amount
FROM
    Bank_Loan_Data
WHERE
     loan_status = 'Charged Off';
```

iv. Bad Loans Amount Received
```SQL
SELECT
     SUM (total_payment) AS Bad_Loan_Amount_Received
FROM
    Bank_Loan_Data
WHERE
     loan_status = 'Charged Off';
```
![Bad_Loan_Issued](https://github.com/user-attachments/assets/89c04637-5574-43b3-994b-34286205eb4e)

With the above, it's seen that the total percentage of loans that were given out by the bank to borrowers has low return/refund rate of '**13%**'. Meaning, many borrowers failed to meet up with their payment and on time (Charged Off). Also, fewer borrowers applied for Bad loans as applied to that of the Good Loans which was on a positive note or a good thing for the bank, but this was on a negative/bad note of which the bank made no profit from, and having amounted to '**5.3k**' applicants.  Also, Bad loans funded by the bank to borrowers was on a low note of '**$65.5M**' due to number of applications as compared to the previous. Again, Amount repaid by borrowers were on a negative note as well, and amounting to '**$37.3M**' returned. Seeing all these, the bank were at a loss with the sum of '**$-28.2M**' within that period.
