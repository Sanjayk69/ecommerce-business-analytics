# E-Commerce Sales Analytics

## Project Overview

An end-to-end e-commerce analytics project focused on understanding sales performance, order trends, product-category performance, and pricing/volume dynamics.

The project uses Python for data profiling and validation, SQLite/SQL for relational analysis and analytical dataset creation, and Power BI for interactive business intelligence reporting.

### Analytical Workflow

**Python → Data Validation → SQLite/SQL → KPI Development → Power BI → Business Insights**

---

## Business Problem

E-commerce businesses need to understand how sales performance changes over time, which product categories contribute the most value, and how sales volume and pricing interact.

This project answers questions such as:

- How has product sales value changed over time?
- Is observed growth driven by order volume, average order value, or both?
- Which product categories contribute the most product sales value?
- Which categories combine high sales volume with higher or lower prices?
- Which category segments represent the largest share of observed product sales value?
- What data-quality considerations should be addressed before reporting results?

---

## Dataset

The dataset contains e-commerce transactional and reference data across multiple relational tables, including:

- Customers
- Orders
- Order Items
- Order Payments
- Order Reviews
- Products
- Sellers
- Geolocation
- Product Category Translation

Key dataset scale:

- ~99K orders
- ~113K order-item records
- ~33K products
- ~3K sellers
- ~1M geolocation records

The analysis uses **January 2017 through August 2018** as the primary reporting period. Partial boundary periods were excluded from the main dashboard to improve month-to-month comparability.

---

## Data Preparation & Validation

Python was used to profile the source tables and validate the relational structure before analytical work.

Key validation checks included:

- Row counts and table-level profiling
- Primary-key uniqueness
- Composite order-item grain validation
- Duplicate detection
- Missing-value assessment
- Referential integrity between orders, order items, products, sellers, payments, and reviews
- Identification of orders without order-item records
- Identification of multiple payment and review records per order

The order-item grain was validated at:

`(order_id, order_item_id)`

This was important because an order can contain multiple products/items, while `product_id` is not unique within the order-item table.

The validated data was then loaded into SQLite for SQL-based analysis.

---

## SQL Analysis

The SQL workflow is organized into four stages:

| File | Purpose |
|---|---|
| `01_schema.sql` | Defines the SQLite analytical schema and table structure |
| `02_data_quality.sql` | Performs data-quality and relational validation checks |
| `03_business_analysis.sql` | Performs business-oriented sales and category analysis |
| `04_powerbi_dataset.sql` | Creates analytical datasets used by Power BI |

The SQL analysis focuses on:

- Monthly sales performance
- Order volume
- Items sold
- Average order value
- Month-over-month growth
- Product-category performance
- Category revenue contribution
- Average item price
- Sales-volume analysis
- Category segmentation

---

## KPI Framework

The dashboard uses the following core KPIs:

### Product Sales Value

Product merchandise value calculated from the `order_items.price` field.

> This metric represents product sales value and excludes freight.

### Orders

Number of orders represented in the monthly analytical dataset.

### Items Sold

Total quantity of order items sold.

### Average Order Value

```text
AOV = Product Sales Value / Orders
```

### Revenue Growth

```text
Revenue Growth % =
(Current Month Product Sales Value - Previous Month Product Sales Value)
 / Previous Month Product Sales Value
```

### Items per Order

```text
Items per Order = Items Sold / Orders
```

---

## Power BI Dashboard

The Power BI dashboard contains three pages.

### 1. Executive Sales Overview

Provides a high-level view of:

- Product sales value
- Order volume
- Items sold
- Average order value
- Monthly product sales trends
- Monthly growth
- Top product categories
- Category price-versus-volume relationships

### 2. Category Performance Analysis

Analyzes product categories using:

- Product sales value
- Items sold
- Average item price
- Category segmentation

Categories are segmented using volume and price characteristics to identify:

- High Volume / High Price
- High Volume / Low Price
- Low Volume / High Price
- Low Volume / Low Price

### 3. Business Insights & Key Findings

Summarizes the major analytical findings and provides context around:

- Observed sales growth
- Category concentration
- Volume-versus-price dynamics
- Potential assortment and pricing opportunities
- Analytical limitations

---

## Key Findings

### 1. Observed sales growth was primarily associated with higher order volume

Between January 2017 and August 2018:

- Product sales value increased **610.4%**
- Orders increased **700.0%**
- Average order value decreased **13.1%**

This indicates that the observed expansion in product sales value coincided with substantially higher order volume rather than an increase in average order value.

This is an observed relationship, not a causal conclusion.

### 2. Product sales value was concentrated in high-volume categories

The largest product categories included:

1. Health & Beauty — approximately **$1.26M**
2. Watches & Gifts — approximately **$1.20M**
3. Bed, Bath & Table — approximately **$1.04M**
4. Sports & Leisure — approximately **$0.99M**
5. Computers & Accessories — approximately **$0.91M**

High-volume category segments represented approximately **93.7%** of product sales value during the analyzed period.

### 3. Volume and price jointly influence category performance

Category performance was not determined by price alone.

Lower-priced categories can generate substantial product sales value when supported by high unit volume, while higher-priced categories can contribute less when demand volume is relatively limited.

The underlying relationship can be expressed as:

```text
Product Sales Value = Items Sold × Average Item Price
```

### 4. High-price / low-volume categories warrant further investigation

High-price / low-volume categories represented approximately **5.0%** of product sales value.

These categories could be investigated further for:

- Demand and conversion
- Product assortment
- Pricing strategy
- Customer behavior
- Inventory availability
- Category-specific marketing performance

These are analytical opportunities for further investigation rather than confirmed causes of lower volume.

---

## Analytical Limitations

Several limitations were considered when interpreting the results:

- The primary dashboard period is limited to **January 2017 through August 2018** because of incomplete boundary periods in the source data.
- Product sales value is based on `order_items.price` and **does not include freight**.
- Product sales value should therefore not be interpreted as accounting revenue or net revenue.
- Category-level relationships describe observed patterns and should not be interpreted as causal effects.
- Some product categories required translation or fallback handling because the category translation table does not contain every source category.
- Multiple payment and review records can exist for a single order, so these tables require careful aggregation when joined to order-level analysis.

---

## Repository Structure

```text
ecommerce-sales-analytics/
│
├── data/
│
├── python/
│   ├── 01_data_profiling.ipynb
│   └── 02_load_sqlite.ipynb
│
├── sql/
│   ├── 01_schema.sql
│   ├── 02_data_quality.sql
│   ├── 03_business_analysis.sql
│   └── 04_powerbi_dataset.sql
│
├── powerbi/
│   ├── ecommerce_sales_dashboard.pbix
│   └── screenshots/
│       ├── page1_executive_overview.png
│       ├── page2_category_analysis.png
│       └── page3_business_insights.png
│
├── outputs/
│
└── README.md
```

---

## Tools & Technologies

**Programming & Analysis**
- Python
- Pandas
- NumPy
- Jupyter Notebook

**SQL & Data**
- SQL
- SQLite
- Relational Data Modeling
- Data Validation
- Data Quality Analysis
- ETL/Data Transformation

**Business Intelligence**
- Microsoft Power BI
- DAX
- Data Modeling
- KPI Development
- Dashboard Design
- Data Visualization

**Analytical Techniques**
- Exploratory Data Analysis
- Trend Analysis
- Category Segmentation
- Price-Volume Analysis
- KPI Analysis
- Business Insight Development

---

## Project Outcomes

This project demonstrates an end-to-end Data Analyst workflow:

1. **Profile and understand raw data with Python**
2. **Validate relational structure and data quality**
3. **Load and analyze relational data using SQLite and SQL**
4. **Create reusable analytical datasets**
5. **Define business KPIs**
6. **Build interactive Power BI dashboards**
7. **Translate analytical results into business findings**
8. **Document analytical limitations and assumptions**

The project emphasizes practical Data Analyst skills across **SQL, Python, data quality, relational data modeling, KPI development, Power BI, and business analysis**.
