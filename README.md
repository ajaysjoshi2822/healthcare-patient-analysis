# healthcare-patient-analysis
Analysis of patient trends and readmission drivers using Excel, SQL, and Tableau 

# Superstore Sales and Profitability Dashboard

## Overview  
This project analyzes sales and profitability using a retail Superstore dataset. The objective was to identify key drivers of profit across products, discount strategies, and customer segments, and present the findings through an interactive Tableau dashboard.

## Objectives  
- Identify which products and categories drive the most profit  
- Analyze the impact of discounting on profitability  
- Evaluate customer segments and shipping methods  
- Build a clear and interactive dashboard for business decision-making  

## Dataset  
- Source: Superstore dataset (Kaggle)  
- Includes order-level data such as products, customers, shipping details, and financial metrics (sales, profit, discount, shipping cost)  

## Data Processing (SQL)  
Data was transformed in BigQuery using SQL.

### Key Transformations  
- Aggregated data by category, sub-category, segment, ship mode, and discount bands  
- Created calculated metrics:  
  - Profit Margin = Profit / Sales  
  - Discount Amount = Discount * Sales  
  - Shipping Cost Ratio = Shipping Cost / Sales  

## Dashboard Structure (Tableau)  

### Product Performance  
- Profit by Category  
- Profit by Sub-Category  
Provides visibility into which products contribute most to overall profitability  

### Discount Impact  
- Profit Margin by Discount Band  
Highlights how different discount levels affect profitability  

### Customer and Shipping Analysis  
- Profitability by Segment and Ship Mode  
Evaluates differences in customer behavior and operational efficiency  

### KPI Summary  
- Total Sales  
- Total Profit  
- Profit Margin  

## Key Insights  
- Profit margins are relatively consistent, indicating performance is driven primarily by sales volume  
- Certain sub-categories significantly outperform others, highlighting opportunities for optimization  
- Higher discount levels are associated with lower profit margins  
- Customer segments and shipping methods exhibit different profitability patterns  

## Tools Used  
- SQL (BigQuery)  
- Tableau  

## What This Project Demonstrates  
- Data cleaning and transformation using SQL  
- Development of business-relevant metrics  
- Dashboard design and visualization best practices  
- Ability to translate data into actionable insights  

## Dashboard Preview  
(Add screenshot here)

## Links  
- Tableau Dashboard: (add link)  
