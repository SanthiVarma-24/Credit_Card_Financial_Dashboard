# Credit_Card_Financial_Dashboard
This project presents an end-to-end business intelligence pipeline for a Credit Card Financial Report, covering everything from database creation and data transformation to interactive Power BI dashboards with dynamic revenue insights.

📌 Project Overview

The objective of this project is to analyze the weekly financial and behavioral aspects of credit card users, including revenue generation, delinquency, and card activation trends. The data was ingested from a CSV, stored and transformed in PostgreSQL, then visualized in Power BI using DAX-powered KPIs and trend analysis.

🛠️ Tech Stack
Tool	Purpose
PostgreSQL	Database creation and data storage
Power BI	Dashboarding and business insights
DAX	Custom KPIs and time-based measures
SQL	Data cleaning & transformations
CSV	Raw data source

🧱 Project Workflow
1. 📂 Data Import and Database Setup: 
  Created a PostgreSQL database and table schema.
  Imported credit card transaction and customer data from CSV
2. 🧹 Data Cleaning & Transformation: 
  Removed nulls, duplicates, and standardized column types.
3. 📈 Power BI Dashboard & DAX Measures
  Imported the transformed data into Power BI and created custom DAX measures.

✅ DAX Measures:
age_group → age segmentation (18-25, 26-35, etc.)
income_group → income segmentation (Low, Medium, High)
Total Revenue = 
    SUM('Data'[Annual_Fee]) + 
    SUM('Data'[Transaction_Amount]) + 
    SUM('Data'[Interest_Earned])

Current Week Revenue = 
    CALCULATE([Total Revenue], WEEKNUM('Data'[Date]) = WEEKNUM(TODAY()))

Previous Week Revenue = 
    CALCULATE([Total Revenue], WEEKNUM('Data'[Date]) = WEEKNUM(TODAY()) - 1)

WoW Change % = 
    DIVIDE([Current Week Revenue] - [Previous Week Revenue], [Previous Week Revenue])

📊 Key Insights
💰 Revenue Insights

Total Revenue comprises:

Credit Card Annual Fees

Transaction Amounts

Interest Earned

Week-over-Week Growth: X% increase in revenue compared to previous week.

Top Contributing Segments:

Age group: 36-50

Income group: High Income

⚠️ Delinquent Accounts

Delinquency Rate: X% of accounts marked as delinquent.

These accounts contribute to a Y% loss in expected revenue.

Concentrated among:

Lower income groups

Age groups 18–25 and 50+

🟢 Card Activation Within 30 Days

Z% of new users activated their credit cards within 30 days of issuance.

Early activation is correlated with higher transaction volume and revenue.

Opportunity: Target late activators with onboarding campaigns.

🔁 Weekly Update Process
✅ Added Next Week's Data

A new CSV containing the next week’s data was ingested into PostgreSQL.

COPY credit_card_data
FROM '/path/to/credit_card_data_week2.csv'
DELIMITER ','
CSV HEADER;

🔄 Power BI Data Refresh
After data refresh:
  New week revenue metrics auto-updated
  WoW % change recalculated
  Trend lines reflected the additional data
  Ensured dynamic dashboard behavior by using relative date filtering and time intelligence functions in DAX.
