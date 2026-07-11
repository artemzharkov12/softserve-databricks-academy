Global News & Crypto Market Correlation Pipeline
Author: Artem Zharkov

📌 Project Description
This project is a Data Engineering pipeline designed to collect, process, and analyze the correlation between global news events (GDELT v2.0 database) and cryptocurrency market behavior. The primary goal of the pipeline is to prepare cleaned, structured data marts to identify patterns between global information sentiment and asset price movements.

🏗 Architecture & Technologies
The project implements a classic Medallion Architecture (Landing -> Bronze -> Silver -> Gold).

Technology Stack:

Compute Engine: Apache Spark (PySpark)

Platform: Azure Databricks

Storage: Azure Data Lake Storage Gen2 (ADLS Gen2)

Data Governance & Security: Unity Catalog (Managed Tables, External Volumes)

Data Formats: Delta Lake, Parquet, CSV/TSV

🚀 Current Implementation Status
1. Infrastructure Setup (Databricks + Azure)
Configured External Locations for secure Databricks access to Azure containers.

Created the dbr_dev catalog and artemzharkov10_bronze schema.

Created Unity Catalog Volumes (e.g., gdelt_history) to interact directly with raw files in the Data Lake, bypassing the local cluster file system (DBFS).

2. Landing Layer (Raw Data Ingestion)
File: 01_landing/01a_historical_landing_gdelt

Implemented a script to parse masterfilelist.txt and batch download historical GDELT data.

Optimization: ZIP archive downloading and extraction are performed In-Memory on the cluster. Raw bytes are written directly to the Azure Volume without saving temporary files to the hard drive, effectively bypassing strict permissions on Shared clusters.

3. Bronze Layer (Structured Raw Data)
File: 02_bronze/02a_bronze_gdelt

Configured a Batch process to read raw files (headerless, tab-separated) using PySpark.

Applied strict Schema Enforcement using the official 61-column GDELT v2.0 schema to instantly assign business names and cast data types.

The output is saved in Delta Lake format as a Managed Table (gdelt_history_bronze) within Unity Catalog.

📊 Data Structure: GDELT v2.0 Events (Bronze Layer)
The source GDELT datasets do not contain headers. In the Bronze layer, the official 61-column schema is enforced to structure the dataset into logical blocks:

Identifiers & Time: GlobalEventID, SqlDate, MonthYear, FractionDate.

Actors (1 & 2): Detailed information about the initiator and receiver of the action, including country codes (Actor1CountryCode), organization types (Actor1Type1Code), and ethno-religious attributes.

Event Classification (CAMEO): EventCode, EventBaseCode, IsRootEvent (identifies the primary event).

Impact Metrics (Critical for Analysis):

GoldsteinScale: Assessment of the event's impact on global stability.

AvgTone: The overall sentiment of the news (negative to positive).

NumMentions, NumArticles: Popularity and media reach of the event.

Geolocation: Coordinates (Lat, Long) and specific regions of the actors and the action itself.

Metadata: SourceUrl (direct link to the original news article).