# 🚀 Data Engineering Journey | SoftServe & Databricks Academy

Welcome to my central repository for the **Databricks Data Engineering Academy**. 
This workspace documents my progress, projects, and hands-on laboratory work focused on building scalable, resilient, and secure data pipelines using the Apache Spark ecosystem and Delta Lake.

**Author:** Artem Zharkov
**Focus:** Data Engineering, ETL/ELT pipelines, Cloud Architecture, BI Analytics.

---

## 🛠️ Core Tech Stack
* **Compute & Orchestration:** Databricks, Apache Spark (PySpark & Spark SQL)
* **Storage & Formats:** Delta Lake, Unity Catalog, Parquet
* **Architecture:** Medallion Data Architecture (Bronze ➔ Silver ➔ Gold)
* **Tools & Analytics:** Databricks AI/BI Dashboards, REST APIs, Git Integration

---

## 🗺️ Academy Roadmap & Lab Tracker

Below is the chronological roadmap of the laboratory works completed during the academy. Each folder contains the respective notebooks, data configurations, and a detailed local `README.md` with technical specifics.

### ✅ [Lab 01: ETL Basics & BI Dashboards](./lab_01_basics)
**Status:** Completed
* **Objective:** Build an end-to-end data pipeline to analyze the Polish real estate market and its correlation with currency exchange rates.
* **Key Implementations:**
  * **API Ingestion:** Automated data extraction from Kaggle (House Prices) and NBP (National Bank of Poland).
  * **Security:** Implemented a fail-fast secret management system using Databricks Volumes for API tokens.
  * **Data Processing (Medallion):** * `Bronze`: Raw data ingestion.
    * `Silver`: Data cleansing, deduplication, and dynamic null-imputation.
    * `Gold`: Tidy Data transformations using optimized `F.broadcast` cross-joins for multi-currency analysis.
  * **Performance:** Applied Delta Lake `OPTIMIZE` and `ZORDER BY` for efficient data skipping.
* **Results:** A fully re-runnable ETL pipeline and an interactive Databricks Dashboard visualizing the "new-build premium" trend and city-level ROI for foreign investors.

### ✅ [Lab 02: Batch Data Pipeline & Medallion Architecture Setup](./lab_02_medallion)
**Status:** Completed
* **Objective:** Build an automated, secure batch ingestion and transformation pipeline to correlate global news events (GDELT) with financial market volatility (Crypto, Commodities) using PySpark and Unity Catalog.
* **Key Implementations:**
  * **Medallion Architecture:** Developed Landing, Bronze, and Silver layers with Delta Lake.
  * **Security & Governance:** Integrated Azure Key Vault via Databricks Secret Scopes. Set up Unity Catalog schemas and volumes.
  * **Data Quality & Lineage:** Implemented idempotency checks for API downloads, injected hidden UC metadata (`_metadata.file_path`) into the Bronze layer, and used regex for feature engineering in Silver.
  * **Orchestration:** Built an automated DAG using Databricks Workflows with strict task dependencies.
  * **Legacy Access:** Configured OAuth 2.0 direct storage access via Service Principal credentials (`abfss://`).
* **Results:** A robust, automated batch pipeline capable of safely ingesting and cleaning historical market and news data, fully prepared for Gold layer analytics or ML modeling.

### ⏳ Lab 03: [Topic Name to be added]
**Status:** Planned
* **Objective:** [TBA]
* **Key Implementations:** [TBA]
* **Results:** [TBA]

---

## 💡 How to Navigate
To explore the code and specific implementations, click on the links in the Roadmap above to visit each lab's dedicated folder. Every completed lab contains its own detailed documentation regarding setup, architecture, and business logic.