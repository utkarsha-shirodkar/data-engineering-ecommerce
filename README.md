# E-commerce Analytics on Databricks

An end-to-end e-commerce analytics project built with Databricks notebooks. It organizes raw order and reference data into a medallion-style data warehouse and provides a dashboard export and example business questions for analysis.

## Project overview

The notebooks create an `ecommerce` catalog with `bronze`, `silver`, and `gold` schemas. They process product, customer, date, and order-item data through these layers to produce dimensional and fact tables for reporting.

```text
Raw CSV data
    |
    v
Bronze tables --> Silver tables --> Gold dimensions and fact tables --> BI / Genie analysis
```

## Repository contents

| Folder                                                   | Description                                                                           |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `0_data/ecomm-raw-data/`                                 | Source CSVs for brands, categories, customers, dates, products, and daily order items |
| `1_codes/project_ecommerce/1_setup/`                     | Notebook to create the `ecommerce` catalog and medallion schemas                      |
| `1_codes/project_ecommerce/2_medallion_processing_dim/`  | Bronze, silver, and gold processing notebooks for dimensions                          |
| `1_codes/project_ecommerce/3_medallion_processing_fact/` | Bronze, silver, and gold processing notebooks for order-item facts                    |
| `2_genie_exploration/`                                   | Suggested questions for Databricks Genie or other conversational analytics            |
| `3_dashboard/`                                           | Dashboard PDF export and a denormalized gold-view query                               |
| `resources/`                                             | Databricks and legacy architecture diagrams                                           |

## Technology

- Databricks notebooks
- Apache Spark / PySpark
- Databricks SQL
- Delta tables and a Bronze-Silver-Gold medallion architecture

## Getting started

This project is designed to run in a Databricks workspace with Spark compute and Unity Catalog access. It is not a standalone local application.

1. Upload or clone this project into your Databricks workspace.
2. Make the CSV files in `0_data/ecomm-raw-data/` available to the workspace, for example in a Unity Catalog volume.
3. Review the source paths used by the ingestion notebooks and update them to the location where you uploaded the data.
4. Run `1_codes/project_ecommerce/1_setup/setup_catalog.ipynb` to create the catalog and schemas.
5. Run the bronze, silver, and gold notebooks in order. Process both the dimension notebooks and the fact notebooks through each layer.
6. Use the gold tables with the dashboard and questions in `3_dashboard/` and `2_genie_exploration/`.

You may need permission to create catalogs, schemas, tables, and volumes in your Databricks environment. Adjust catalog, schema, and storage locations if your workspace uses different names or access policies.

## Data notes

The order-item data is organized into daily CSV files under `0_data/ecomm-raw-data/order_items/landing/`. The accompanying reference data includes brands, categories, customers, dates, and products. Confirm the date range and currency-conversion logic in the notebooks before using the resulting data for business decisions.

## Dashboard

The `3_dashboard/` folder contains a PDF export named `E-commerce BI.pdf` and the SQL used to create a denormalized gold view. The PDF is a reference/export; dashboard interactivity may require recreating or importing the dashboard in your Databricks workspace.
