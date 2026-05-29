# 📊 Sales Analytics Project

A complete end-to-end data analysis project built entirely from scratch on a real data warehouse. This project covers everything from raw database exploration to advanced analytics and reporting — using only SQL Server.

---

## 🗂️ Project Structure

```
sales-analytics/
│
├── 1_exploratory_data_analysis/
│   ├── 01_database_exploration.sql
│   ├── 02_dimensions_exploration.sql
│   ├── 03_date_exploration.sql
│   ├── 04_measures_exploration.sql
│   ├── 05_magnitude.sql
│   └── 06_ranking.sql
│
├── 2_advanced_analytics/
│   ├── 01_change_over_time.sql
│   ├── 02_cumulative_analysis.sql
│   ├── 03_performance_analysis.sql
│   ├── 04_part_to_whole.sql
│   ├── 05_data_segmentation.sql
│   └── 06_reporting.sql
│
└── 3_reports/
    ├── report_customers.sql
    └── report_products.sql
```

---

## 🗄️ Data Model

The project is built on a **star schema** in the `gold` layer of a data warehouse:

| Table | Type | Description |
|-------|------|-------------|
| `gold.fact_sales` | Fact | Order transactions with sales amount, quantity, and price |
| `gold.dim_customer` | Dimension | Customer details including demographics and location |
| `gold.dim_products` | Dimension | Product details including category, subcategory, and cost |

> Sales are calculated as: `sales_amount = quantity × price`

---

## 🔍 Part 1 — Exploratory Data Analysis

### Database & Dimensions Exploration
- Explored all tables and columns using `INFORMATION_SCHEMA`
- Validated row counts across all three tables
- Checked referential integrity between fact and dimension tables
- Verified data quality — nulls, duplicates, negative values, and date logic
- Explored distributions across country, gender, marital status, category, subcategory, and product line

### Date Exploration
- Identified the full date range of the dataset
- Checked for impossible dates (shipping before order, due before shipping)

### Measures Exploration
- Calculated total, average, min, and max for `sales_amount`, `price`, and `quantity`
- Performed a skew ratio analysis to detect outliers in sales distribution
- Counted total distinct orders

### Magnitude
- Ranked total sales and customer counts by country, gender, category, and subcategory

### Ranking
- Identified top and bottom 5 products by revenue
- Ranked top 10 customers by revenue using `ROW_NUMBER()`
- Found the 3 customers with the fewest orders

---

## 📈 Part 2 — Advanced Analytics

### Change Over Time
- Yearly trends: total sales, orders, customers, and quantity
- Seasonality view: which month performs best regardless of year
- Monthly trend view: how sales evolved month by month over time using `DATETRUNC`

### Cumulative Analysis
- Running total of sales over time using `SUM() OVER()`
- Moving average of price over time using `AVG() OVER(ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)`

### Performance Analysis
- Compared each product's and customer's sales against the overall average
- Year-over-year performance analysis using `LAG()` to identify improving and declining products

### Part-to-Whole
- Percentage contribution to total sales by category, subcategory, and country
- Percentage contribution by quantity and price per category

### Data Segmentation
- **Products by cost range**: Below 100 / 100–500 / 500–1000 / Above 1000
- **Products by sales performance**: High Performer / Mid Range / Low Performer
- **Customers by spending behavior**: VIP / Regular / New (based on lifespan and total spending)
- **Customers by order frequency**: Frequent / Occasional / Rare

---

## 📋 Part 3 — Reports (Views)

### `gold.report_customers`
A consolidated customer-level VIEW that includes:
- Full name and age group segmentation (20s, 30s, 40s, 50+)
- Customer segment (VIP / Regular / New)
- Total orders, spending, quantity, and products
- KPIs: recency, average order value, average monthly spend

### `gold.report_products`
A consolidated product-level VIEW that includes:
- Category, subcategory, and cost
- Product segment (High Performer / Mid Range / Low Performer)
- Total orders, sales, quantity, and unique customers
- KPIs: recency, average order revenue, average monthly revenue

---

## 🛠️ Tools & Technologies

- **Database**: SQL Server
- **Language**: T-SQL
- **Concepts**: Star schema, data warehousing, window functions, CTEs, views

---

## 💡 Key Findings

- Sales data is **right-skewed** with a skew ratio of 6 — a small number of high-value orders pull the average up significantly
- The majority of orders have a quantity of 1, meaning `total_sales ≈ total_price`
- Customer segmentation reveals a clear split between VIP, Regular, and New customers based on spending behavior and tenure
- Product performance varies significantly across categories, with clear high and low performers identifiable through segmentation

---

## 👤 About This Project

This project was built entirely from scratch without tutorials as part of a personal data analytics portfolio. It follows a structured analytical workflow from raw exploration through to production-ready reporting views — the same workflow used in real data analyst roles.
