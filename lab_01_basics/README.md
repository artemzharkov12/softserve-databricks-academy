# Polish Real Estate Market Analysis

## Project Overview
This project is an end-to-end Data Engineering pipeline built in **Databricks**. It ingests real estate data and live currency exchange rates to provide a multi-currency investment analysis for major Polish cities (Warsaw, Kraków, Poznań). 

The pipeline strictly follows the **Medallion Architecture** (Bronze, Silver, Gold) and leverages **Apache Spark** for distributed data processing and **Delta Lake** for ACID transactions and optimized storage.

## Architecture & Data Flow
1. **Raw Layer:** Data is downloaded via REST API from Kaggle (House Prices) and NBP (National Bank of Poland - EUR, USD, GBP rates). API credentials are securely managed via Databricks Volumes.
2. **Bronze Layer:** Raw CSV data is ingested into a Delta table with raw schema intact.
3. **Silver Layer:** Data cleansing (trim, initcap), datatype casting, deduplication, and handling of null values.
4. **Gold Layer:** Business-level aggregations. The data is transformed into a Tidy Data (Long) format using optimized `broadcast` Cross-Joins to enable instant multi-currency filtering on the BI side.

## Tech Stack & Features
* **Databricks & PySpark:** Distributed transformations, `Window` functions, and `groupBy` aggregations.
* **Delta Lake:** Features `.mode("overwrite")` for idempotency, and `OPTIMIZE ... ZORDER BY` for efficient Data Skipping.
* **AI/BI Dashboards:** Interactive visualization layer directly integrated into Databricks (Scatter plots for market density, Bar charts for city-level ROI).
* **Security:** Implemented a "fail-fast" security check using `try-except` and `dbutils.notebook.exit()` to prevent unauthorized API calls without the `secrets.json` volume file.

## Setup Requirements
To run this pipeline, a `secrets.json` file must be manually created in the user's Volume (`/Volumes/general/<username>/raw_data/secrets.json`) containing the Kaggle API token.