# Super Store Analysis
Analysis of retail sales trends and drivers using Excel, SQL, and Tableau 

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

### Sample SQL Queries

#### Discount Band Analysis
This query groups transactions into discount bands and calculates sales, shipping cost, discount amount, profit, and profit margin by year.

```sql

WITH discount_band_analysis AS (
  SELECT
    Year AS year,
    ROUND(SUM(Sales), 2) AS sales,
    ROUND(SUM(`Shipping Cost`), 2) AS shipping_cost,
    ROUND(SUM(Discount * Sales), 2) AS discount_amount,
    ROUND(SUM(Profit), 2) AS profit,
    CASE
      WHEN Discount = 0 THEN '0'
      WHEN Discount BETWEEN 0.01 AND 0.10 THEN '0.01 to 0.10'
      WHEN Discount BETWEEN 0.11 AND 0.20 THEN '0.11 to 0.20'
      WHEN Discount BETWEEN 0.21 AND 0.30 THEN '0.21 to 0.30'
      WHEN Discount BETWEEN 0.31 AND 0.40 THEN '0.31 to 0.40'
      ELSE '0.41 to 0.50'
    END AS discount_band
  FROM `portfolio-financial-data.finance_portfolio.superstore_data`
  GROUP BY year, discount_band
)

SELECT
  *,
  ROUND((profit / sales) * 100, 2) AS profit_margin
FROM discount_band_analysis
ORDER BY year, profit DESC;

```

#### Sub-Category Profit Analysis
This query evaluates sub-category performance by category and year, including sales, discount amount, shipping cost, profit, profit margin, and profit rank within each category.

```sql

WITH subcategory_profit_analysis AS (
  SELECT
    Category AS category,
    `Sub-Category` AS sub_category,
    Year AS year,
    ROUND(SUM(Sales), 2) AS sales,
    ROUND(SUM(Discount * Sales), 2) AS discount_amount,
    ROUND(SUM(`Shipping Cost`), 2) AS shipping_cost,
    ROUND(SUM(Profit), 2) AS profit
  FROM `portfolio-financial-data.finance_portfolio.superstore_data`
  GROUP BY category, sub_category, year
)

SELECT
  *,
  ROUND((profit / sales) * 100, 2) AS profit_margin,
  RANK() OVER (
    PARTITION BY year, category
    ORDER BY profit DESC
  ) AS profit_rank
FROM subcategory_profit_analysis
ORDER BY year, category, profit_rank;

```
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

![Dashboard Preview](https://github.com/user-attachments/assets/283cc169-c873-4d2c-b318-41c53bfbb872)

- Tableau Dashboard: https://public.tableau.com/views/Portfolio-asj_twb_3/Dashboard1

## Key Takeaways

- Profit margins remained stable (~12%–14%), indicating profitability is driven more by sales volume than margin expansion.

- Higher discount levels consistently reduced profitability, making discounting a key lever to optimize.

- Top-performing sub-categories contribute disproportionately to profit, highlighting clear areas for focus.

- Lower discount bands (0%–10%) generated the strongest profit outcomes.

- Customer segments and shipping modes show varying profitability, reflecting differences in behavior and cost efficiency.

- Shipping costs and discount strategy are the primary drivers impacting overall profit performance.
