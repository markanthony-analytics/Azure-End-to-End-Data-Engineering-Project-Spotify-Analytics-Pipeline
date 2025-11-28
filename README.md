# Azure-End-to-End-Data-Engineering-Project-Spotify-Analytics-Pipeline

## 📌 Project Overview

This project demonstrates a full end-to-end modern data engineering pipeline on Azure using Spotify streaming data.
The goal is to ingest raw files from Azure Storage, perform data cleaning & transformations using Spark in Azure Databricks, and create curated analytics tables for downstream reporting & trend insights.

The solution mirrors how data engineering pipelines are built in real-world cloud environments—scalable, fault-tolerant, and analytics-ready.

## 🎯 Project Objectives
| Goal                                                          | Description                                                      |
| ------------------------------------------------------------- | ---------------------------------------------------------------- |
| ✔ Ingest raw Spotify dataset into Azure Data Lake (ADLS Gen2) | CSV/JSON ingestion using structured landing zones                |
| ✔ Build scalable ETL pipelines with PySpark on Databricks     | Schema enforcement, transformations, partitioning, Delta support |
| ✔ Store processed data in Delta Lake format                   | Time travel enabled, optimized for analytics workloads           |
| ✔ Analyze Spotify artist, album & track trends                | Most streamed artists, tempo patterns, popularity metrics        |
| ✔ Enable BI consumption (Power BI)                            | Curated layer available for dashboarding                         |

## 🏗️ Project Architecture
                ┌─────────────────────────────┐
                │  Spotify Source Dataset      │
                └───────────────┬─────────────┘
                                │
                                ▼
                     Raw Zone (Bronze)
              Azure Data Lake Storage Gen2
                                │
                                ▼
                   Databricks ETL Processing
            PySpark Cleaning, Joins, Validation
                                │
                                ▼
                 Refined Zone (Silver)
              Delta Lake Structured Tables
                                │
                                ▼
                 Curated Zone (Gold)
         Analytics-Optimized Fact + Dimension Tables
                                │
                                ▼
                        Power BI Reporting
              Dashboards & Trend Visual Insights
## 🧩 Solution Breakdown
| Layer             | Technology                    | Output                                |
| ----------------- | ----------------------------- | ------------------------------------- |
| **Storage**       | ADLS Gen2                     | Raw → Refined → Curated               |
| **ETL Compute**   | Azure Databricks + PySpark    | Transformations, cleansing, merges    |
| **Lake Format**   | Delta Lake                    | ACID, schema enforcement, time travel |
| **Orchestration** | (Optional) Azure Data Factory | Scheduling & monitoring               |
| **Consumption**   | Power BI / Databricks SQL     | Data insights, dashboards             |

## 📂 Repository Structure
spotify_azure_project/
│
├── data/
│   ├── raw/             # Initial uploaded data (CSV/JSON)
│   ├── refined/         # Cleaned + structured Delta tables
│   └── curated/         # Analysis-ready datasets
│
├── notebooks/
│   ├── 01_ingestion_raw.ipynb
│   ├── 02_transformation_refined.ipynb
│   └── 03_curated_tables.ipynb
│
├── src/
│   ├── utils/           # Reusable helper functions (schema, IO)
│   ├── pipeline_raw.py
│   ├── pipeline_refined.py
│   └── pipeline_curated.py
│
└── README.md

## 🔧 Key Features
| Feature                                       | Description                                       |
| --------------------------------------------- | ------------------------------------------------- |
| 🚀 Auto-load files into ADLS using Databricks | scalable ingestion patterns                       |
| 🧪 Data validation + schema enforcement       | clean, consistent datasets                        |
| 📊 Curated fact tables for BI                 | tracks, artists, popularity metrics               |
| ⚡ Delta optimization                          | Z-ORDER, Caching, Auto-Optimize                   |
| 📉 Power BI report layer                      | ranking charts, popularity trends, tempo analysis |

## 🧪 Sample Transformation (PySpark)
from pyspark.sql.functions import col, lower, to_date

df_cleaned = (
    df_raw
    .withColumn("track_name", lower(col("track_name")))
    .withColumn("release_date", to_date(col("release_date"), "yyyy-MM-dd"))
    .filter(col("popularity") > 40)
)

## 📊 Sample Insights Generated
| Metric                   | Result               |
| ------------------------ | -------------------- |
| 🎧 Most streamed artist  | Drake                |
| 🔥 Most popular genre    | Hip-Hop / Pop Fusion |
| ⏱ Avg track duration     | ~3m 10s              |
| 📈 Strongest correlation | Tempo vs Popularity  |

## 🏁 Conclusion

This repository provides a realistic, industry-standard cloud data pipeline for Spotify analytics using Azure.
It showcases storage, ETL processing, Delta Lake architecture & analytical consumption—just like enterprise implementations.
