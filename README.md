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

### ⏳ Lab 02: [Topic Name to be added]
**Status:** Planned / In Progress
* **Objective:** [Short description of the goal will be added here]
* **Key Implementations:** [List of technical skills will be added here]
* **Results:** [TBA]

### ⏳ Lab 03: [Topic Name to be added]
**Status:** Planned
* **Objective:** [TBA]
* **Key Implementations:** [TBA]
* **Results:** [TBA]

---

## 💡 How to Navigate
To explore the code and specific implementations, click on the links in the Roadmap above to visit each lab's dedicated folder. Every completed lab contains its own detailed documentation regarding setup, architecture, and business logic.