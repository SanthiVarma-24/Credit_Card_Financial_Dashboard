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
AgeGroup = SWITCH(
    TRUE(),
        cust_detail[customer_age]<30,"20-30",
        and(cust_detail[customer_age]>=30, cust_detail[customer_age] < 40), "30-40",
        and(cust_detail[customer_age]>=40, cust_detail[customer_age] < 50), "40-50",
        and(cust_detail[customer_age]>=50, cust_detail[customer_age] < 60), "50-60",
        cust_detail[customer_age]>=60, "60+",
        "unknown"
)

IncomeGroup = SWITCH(
     TRUE(),
     cust_detail[income] < 35000, "Low",
     and(cust_detail[income] >=35000, cust_detail[income] <70000), "Medium",
     cust_detail[income] >70000, "High",
     "unknown"
     )

Revenue = cc_detail[annual_fees] + cc_detail[total_trans_amt] + cc_detail[interest_earned]

current_week_revenue = CALCULATE(
     sum(cc_detail[Revenue]),
        FILTER(
            all(cc_detail),
                cc_detail[week_num2]=max(cc_detail[week_num2])))

previous_week_revenue = CALCULATE(
     sum(cc_detail[Revenue]),
        FILTER(
            all(cc_detail),
                cc_detail[week_num2]=max(cc_detail[week_num2])-1))

wow_revenue = DIVIDE([current_week_revenue] - [previous_week_revenue],[previous_week_revenue],0)

Top Contributing Segments:
