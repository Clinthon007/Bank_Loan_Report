# Bank_Loan_Report
---
## Project Overview
A Report to monitor and assess our bank's lending activities and performance which aims to provide insights into key loan-related metrics and their changes over time.

### Data Source

Financial Loan: The primary dataset used for this analysis is the "financial_loan.csv" file, containing detailed information about each loan made by the bank. [ DataSet ](https://drive.google.com/drive/folders/1nVYJrAVvUegJjX9vChxWCW61TzBQ49td)

### Tools Used
- **Microsoft SQL Server**
- **Tableau Desktop** - For Creating Report
    - Links to the Financial_Loan Project and other Tableau_Public Dashboards:

        [SUMMARY_DashBoard](https://public.tableau.com/app/profile/chidera.clinton/viz/SUMMARYDshbrd1/SUMMARY)
      
        [Overview_DashBoard](https://public.tableau.com/app/profile/chidera.clinton/viz/Loan_OVERVIEW/OVERVIEW)
      
        [Details_DashBoard](https://public.tableau.com/app/profile/chidera.clinton/viz/Loan_DETAILS/DETAILS)
      
        [OTHER_DashBoards](https://public.tableau.com/app/profile/chidera.clinton/vizzes)
          

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

The following would be considered along:

   a) Loan By Monthly Trends

   b) Loan By States

   c) Loans By Employee Length
   
   d) Loan By Purpose

   e) Loans by Home Ownership


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
 This a loan or debt given to borrowers whom at the end of a specified period could not meet up with repayment of the debt, either because they cannot afford to repay or they may have died or something else. These borrowers tend to incur more debt over such period in this scenerio since such debt does not favour/profit them. All Bad Debts are generally calculated using the "Charged Off" column/field.
 
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

---

a) Loan Applications By Monthly Trends

![Total_Loan_Apps By_Month](https://github.com/user-attachments/assets/121e5a19-d597-4160-89ef-948bd16861e5)


The graph illustrates a clear upward trend in loan applications throughout the year. The number of applications starts relatively low in January and steadily increases, culminating in a peak in December.

Specific Observations:

**January to April**: The initial months show a gradual increase in loan applications, with a slight dip in February.

**April to July**: A more pronounced upward trajectory is evident, indicating a growing demand for loans during this period.

**July to December**: The trend continues its upward momentum, with a particularly sharp rise from October to December, suggesting a potential surge in loan applications towards the end of the year.

Without additional context, it's challenging to pinpoint the exact reasons behind these trends. However, some potential factors could include:

   - *Seasonality*: Certain months might naturally witness higher loan application volumes due to seasonal factors like tax refunds, year-end bonuses, or holiday spending.

   - _Economic Conditions_: Fluctuations in economic indicators like GDP growth, interest rates, or employment rates could influence borrowing decisions.

   - _Marketing and Promotions_: Targeted marketing campaigns or special loan offers during specific months might drive application numbers.

   ---

b) i. Loan Applications By States

![Tot_Loan_Apps_By_State](https://github.com/user-attachments/assets/16ff3f7a-7525-438b-8edd-185744e56966)


- The map visually depicts the number of loan applications across different states in the USA.
- The numbers associated with each state represent the total loan applications within that state.
- There's a clear variation in loan application numbers across states, indicating disparities in demand or accessibility to loans.

Key Insights:

**California Dominates**:** California** stands out with the highest number of loan applications (6,894), significantly surpassing other states. This could be attributed to its large population, diverse economy, and high cost of living, potentially driving a higher demand for loans.

**Regional Disparities**: The Northeast and West Coast states generally exhibit higher loan application numbers compared to the Midwest and South. This could be influenced by factors such as population density, economic activity, and cost of living.

**States with Lower Applications**: Several states, particularly in the Midwest and South, have relatively lower loan application figures. This could be due to various reasons, including smaller populations, lower income levels, or different economic structures.

**ii. Total Funded Amount by States**

![Tot_Fnd_Amt_by_State](https://github.com/user-attachments/assets/e0fe1ee6-a788-4310-95c5-d5f7ed08677a)


Key Observations

**Wide Variation**: There's a significant disparity in the numerical values across states, suggesting substantial differences in the total funded amount.

Regional Trends:

**West Coast**: **California**(78,484,125) stands out with the highest value, indicating a potentially larger pool of funds in that region.

**Northeast**: States like **New York**(42,077,050) and **Pennsylvania**(15,826,525) exhibit relatively high values, suggesting significant funding in this area.

**Midwest and South**: These regions generally show lower values, implying potentially lower levels of funding compared to the coasts.

**Potential Outliers**: Some states with exceptionally low values (e.g., Wyoming, Vermont) might warrant further investigation to understand the reasons behind the discrepancy.

**iii**. **Total Amount Received By States**

![Tot_Amt_Rcvd_by_State](https://github.com/user-attachments/assets/7dfc8100-f99a-401f-afb1-393f51261d8d)


**Wide Variation**: There is a significant disparity in the numerical values across states, suggesting substantial differences in the total amount received.

**Dominant States**: **California**(83,901,234) stands out with the highest value, followed by **New York**(46,108,181), and **Texas**(34,392,715). These states consistently appear as economic powerhouses in various contexts.

**Regional Trends**: The Northeast and West Coast states generally have higher values, while the Midwest and South tend to have lower figures.

**Potential Outliers**: Some states with exceptionally low values might require further investigation to understand the reasons behind the discrepancy.

---

c) **i. Loan Applications By Employee Length**

![Loan_Apps_by_Emp_length](https://github.com/user-attachments/assets/a319edca-c033-4d71-a526-5d048f98c7c8)

Key Findings:

- **Inverse Relationship**: There seems to be an inverse relationship between employee length and the number of loan applications. Employees with longer tenures tend to apply for loans less frequently than those with shorter tenures.
 
- **High Application Rate for New Employees:** The category of employees with less than one year of employment has the second-highest number of loan applications, suggesting a potential correlation between new hires and financial needs.
 
- **Decreasing Trend**: As employee tenure increases, the number of loan applications generally decreases, with a steeper decline in the earlier years of employment.

- **Dominant Group**: Employees with over 10 years of tenure constitute the largest group of loan applicants.



**ii. Total Funded Amount**

![Funded_Amount_by_Emp_Length](https://github.com/user-attachments/assets/8c770bf9-cb10-4216-bb21-09f5e76e455e)

Key Findings:

**Dominant Group**: Employees with over 10 years of tenure have the highest total funded amount, significantly surpassing other groups. This suggests that longer-tenured employees have access to or are granted larger funding compared to their counterparts.

**Decreasing Trend**: As employee tenure decreases, the total funded amount generally decreases. This indicates a potential correlation between employee experience and the size of funding received.

**Notable Exceptions**: There are some exceptions to the general trend. For instance, employees with 2 years of experience have a higher total funded amount than those with 3 or 4 years of experience. This might indicate specific factors influencing funding decisions for employees in this tenure range.


**iii. Total Amount Received**

![Amount_Received_by_Emp_Length](https://github.com/user-attachments/assets/338d9e3f-2c65-4cd6-9bb0-bad3ca2002b8)

Key Findings:

**Dominant Group**: Employees with over 10 years of tenure have the highest total amount received, significantly surpassing other groups. This suggests that longer-tenured employees have access to or are granted larger amounts compared to their counterparts.

**Decreasing Trend**: As employee tenure decreases, the total amount received generally decreases. This indicates a potential correlation between employee experience and the size of the amount received.

**Notable Exceptions**: There are some exceptions to the general trend. For instance, employees with 2 years of experience have a higher total amount received than those with 3 or 4 years of experience. This might indicate specific factors influencing the amount received for employees in this tenure range.

Possible Interpretations:

**Experience and Trust**: Longer-tenured employees might have established trust and a proven track record, leading to higher levels of funds allocated to them.

**Career Progression**: Employees with more experience often hold higher positions or have greater responsibilities, which could correlate with larger amounts received.

**Project Scope**: The nature of projects undertaken by employees with different tenure lengths might vary in terms of scale and complexity, influencing the required amount.

**Funding Criteria**: There could be specific criteria or policies in place that favor employees with longer tenure when it comes to funding decisions.

---

d) **i. Loan Applications By Purpose**

![Loan_Apps_by_Purpose](https://github.com/user-attachments/assets/b7cb041d-0d2d-4a78-8031-9d4d634f6dd9)

Key Observations:

  - **Debt Consolidation Dominates**: Debt consolidation is the most common loan purpose, accounting for $18.21K in applications. This suggests that many people are seeking loans to manage existing debts.

  - **Credit Card Debt**: Credit card debt is the second most popular reason for seeking loans, with $5.00K in applications. This aligns with the high prevalence of credit card usage and potential difficulties 
      in managing repayments.
  - **Home Improvement and Other Purposes**: Home improvement and "other" purposes each account for a significant portion of loan applications, with $2.88K and $2.88K, respectively. This indicates a range of 
     needs beyond debt consolidation and credit card debt.

  - **Major Purchases and Small Business**: Major purchases and small business loans each represent a sizable portion of applications, with $1.78K each. This suggests a demand for financing for both personal and 
      entrepreneurial endeavors.

  - **Car Loans and Other Purposes**: Car loans, weddings, medical expenses, moving, and home purchases together account for a smaller but still significant portion of loan applications, with a combined total of 
     $2.21K. This highlights the diverse reasons why people seek loans.

  - **Educational and Renewable Energy Loans**: These categories have the lowest number of applications, with $0.09K each, indicating a limited demand for loans in these areas.
      Overall, the data reveals that debt consolidation and credit card debt are the primary drivers of loan applications, followed by home improvement, major purchases, and small business needs.
      While other categories exist, they represent a smaller portion of the total loan applications.


**ii. Loan Funded Amount by Purpose**

![Funded_Amount_by_Purpose](https://github.com/user-attachments/assets/60432b07-a50e-4d84-ae7f-365c1644dbda)

Key Findings:

  - **Debt Consolidation Dominates**: Debt consolidation represents the largest portion of the total funded amount, totaling $232,459.68K. This indicates a significant demand for loans to consolidate existing debts.

  - **Credit Card Debt**: Following closely behind, credit card debt accounts for $58,885.18K in funded amounts. This highlights the substantial financial burden carried by individuals due to credit card debt.
   
  - **Home Improvement and Other**: These categories show significant funding with $31,155.75K each, indicating a substantial investment in home improvement projects and other unspecified purposes.

  - **Small Business and Major Purchases**: Small business and major purchases have received considerable funding, totaling $17,251.60K and $9,225.80K respectively. This suggests a strong focus on supporting entrepreneurial ventures and consumer spending.
  
  - **Remaining Categories**: The remaining categories (car, wedding, medical, house, moving, educational, vacation, renewable energy) collectively represent a smaller portion of the total funded amount


**iii. Loan Amount Received by Purpose**

![Amount_Received_by_Purpose](https://github.com/user-attachments/assets/93afeaf9-d0e1-4007-9b10-4a50656619fd)

**Debt Consolidation Dominates**: The most significant amount received is for debt consolidation, totaling $253,801.87K. This indicates a substantial demand for loans to consolidate existing debts.

**Credit Card Debt**: Following closely behind, credit card debt accounts for $65,214.08K in received funds. This highlights the considerable financial burden carried by individuals due to credit card debt.

**Home Improvement and Other**: These categories show substantial amounts received with $33,289.68K each, indicating significant investment in home improvement projects and other unspecified purposes.

**Small Business and Major Purchases**: Small business and major purchases have received considerable funding, totaling $18,676.93K and $10,266.86K respectively. This suggests a strong focus on supporting entrepreneurial ventures and consumer spending.

**Remaining Categories**: The remaining categories (car, wedding, medical, house, moving, educational, vacation, renewable energy) collectively represent a smaller portion of the total amount received.

---

e) **i. Loan Applications by Home Ownership**

![Tot_Loan_Apps_by_Home_Owned](https://github.com/user-attachments/assets/e1d2652a-1e0e-4ef6-8c72-ff8a3ac4db97)

Key Findings:

**Renters Dominate**: The most significant number of loan applications comes from individuals who rent their homes, with a total of **18,439** applications.

**Homeowners with Mortgages Follow**: The second-largest group of loan applicants consists of homeowners with mortgages, accounting for **17,198** applications.

**Homeowners Without Mortgages (Own)**: This category represents a significantly smaller portion of loan applicants, with only **2,838** applications.



**ii. Funded Amount By Home Ownership**

![Tot_Fnd_Amt_by_Home_Owned](https://github.com/user-attachments/assets/0e1ab471-2907-4448-b9cc-ccc5197c33ff)

**Mortgage Dominate**: The most significant number of loan funded by the bank to individuals using Mortgage, with a total of sum of $219,329,150.

**Renters Follow**: The second-largest group of loan funded consists of homeowners with Rents, accounting for the sum of $185,768,475.

**Homeowners Without Mortgages (Own)**: This category represents a significantly smaller portion of loan funded by the bank, with the sum of $29,597,675.


**iii. Amount Received By Home Ownership**

![Tot_Amt_Rcvd_by_Home_Owned](https://github.com/user-attachments/assets/b2b0c783-d2fa-4242-bc97-32bf73b15700)

**Mortgage** again has the highest sum returned by individuals totally with the sum of $238,474,438

**Renters** follow with the huge sum of $201,823,056

**Own** comes up last as usual with the sum of $31,729,129

Generally, it's seen that areas where more loan were put into or funded still had the highest number of return due to different circumstances like number of applicants. Therefore, their profit margin varies in accordance to amount funded with regards to applicants.

---

