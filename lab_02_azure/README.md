# 🌍 Global News & Crypto Market Correlation Pipeline
**Author:** Artem Zharkov

## 📌 Project Description
This project is a Data Engineering pipeline designed to collect, process, and analyze the correlation between global news events (GDELT v2.0 database) and financial market behavior (Cryptocurrencies and Commodities). The primary goal of the pipeline is to prepare cleaned, structured data marts to identify patterns between global information sentiment and asset price movements.

## 🏗 Architecture & Technologies
The project implements a classic **Medallion Architecture** (Landing ➔ Bronze ➔ Silver ➔ Gold).

**Technology Stack:**
* **Compute Engine:** Apache Spark (PySpark)
* **Platform & Orchestration:** Azure Databricks, Databricks Workflows
* **Storage:** Azure Data Lake Storage Gen2 (ADLS Gen2)
* **Data Governance:** Unity Catalog (Managed/External Tables, Volumes)
* **Security:** Azure Key Vault, Databricks Secret Scopes, OAuth 2.0 (Service Principals)
* **Data Formats:** Delta Lake, Parquet, CSV/TSV

---

## 🚀 Current Implementation Status (Stage 2 Completed)

### 1. Infrastructure & Security
* Configured Unity Catalog External Locations for secure access to Azure containers.
* Created the `dbr_dev` catalog and localized schemas (`bronze`, `silver`).
* Eliminated hardcoded credentials by integrating **Azure Key Vault** with Databricks Secret Scopes (`dbutils.secrets.get`).
* Demonstrated **Legacy Access** capabilities by configuring Spark to read directly from ADLS using OAuth 2.0 (`abfss://`) and Service Principal keys.

### 2. Landing Layer (Raw Data Ingestion)
* **News Data (GDELT):** Implemented a script to parse `masterfilelist.txt` and batch download historical GDELT data. ZIP extraction is performed in-memory, writing bytes directly to the Azure Volume to bypass DBFS limitations.
* **Financial Data:** Automated fetching of daily market data (Bitcoin, Gold, Oil) via the `yfinance` library, parsing multi-index dataframes into clean CSVs.
* **Idempotency:** Implemented strict file existence checks (`os.path.exists`) to prevent redundant downloads and save compute/network resources.

### 3. Bronze Layer (Structured Raw Data)
* Configured Batch processes to read raw files using PySpark and save them in **Delta Lake** format.
* **Schema Enforcement:** Applied the official 61-column GDELT v2.0 schema on read to instantly assign business names and cast data types.
* **Data Lineage:** Automatically injected Unity Catalog metadata (`_metadata.file_path`), `ingest_timestamp`, and `load_date` as physical columns to track data provenance.

### 4. Silver Layer (Cleansing & Transformation)
* Filtered out corrupt or empty records (e.g., dropping rows with `null` in critical date or price columns).
* Applied strict data casting (converting string dates to `TimestampType`, and prices to `DoubleType`).
* **Feature Engineering:** Utilized Regex (`regexp_extract`) to dynamically extract the asset type (e.g., BITCOIN, GOLD) directly from the source filenames.

### 5. Automation & Orchestration
* Integrated all individual notebooks into a fully automated Directed Acyclic Graph (DAG) using **Databricks Workflows**.
* Configured strict task dependencies (Bronze runs only if Landing succeeds) and optimized costs by running the pipeline on a Shared All-Purpose cluster.

---

## 📊 Data Structure: GDELT v2.0 Events (Bronze Layer)
The source datasets do not contain headers. In the Bronze layer, the schema is enforced to structure the dataset into logical blocks:
* **Identifiers & Time:** `GlobalEventID`, `SqlDate`, `MonthYear`, `FractionDate`.
* **Actors (1 & 2):** Detailed information about the initiator and receiver of the action, including country codes and organization types.
* **Event Classification (CAMEO):** `EventCode`, `EventBaseCode`, `IsRootEvent`.
* **Impact Metrics (Critical for Analysis):**
  * `GoldsteinScale`: Assessment of the event's impact on global stability.
  * `AvgTone`: The overall sentiment of the news (negative to positive).
  * `NumMentions`, `NumArticles`: Popularity and media reach.
* **Geolocation & Metadata:** Coordinates, specific regions, and `SourceUrl`.