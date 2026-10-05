# Data

## Source Data

The raw e-commerce dataset used in this project is not included in the GitHub repository.

The project uses the Olist Brazilian e-commerce dataset, containing relational tables for customers, orders, order items, payments, reviews, products, sellers, geolocation, and product-category translation.

The original files are stored locally under:

```text
data/raw/
```

They are excluded from version control because they are source data rather than project-generated analytical assets.

## Processed Data

The `processed/` directory contains the analytical datasets created for the Power BI dashboard:

- `monthly_performance.csv` — monthly product sales value, orders, items sold, AOV, items per order, and month-over-month growth.
- `category_performance.csv` — category-level product sales value, sales volume, average item price, and category segmentation.

These processed datasets are included because they represent outputs of the project's analytical workflow and are directly used for business intelligence reporting.

## Reproducing the Data Pipeline

The source data is profiled using:

```text
python/01_data_profiling.ipynb
```

The source tables are then loaded into SQLite using:

```text
python/02_load_sqlite.ipynb
```

The resulting SQLite database is used by the SQL scripts in the `sql/` directory to perform validation, business analysis, and creation of Power BI-ready analytical datasets.
