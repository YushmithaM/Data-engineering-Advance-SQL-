## Data Engineering & Advanced SQL

A hands-on project exploring Data Warehousing techniques, ETL pipelines, and Advanced SQL — built to understand how raw business data becomes analysis-ready insight for data science and BI.

## Objectives
1. Building the Data Warehouse

## What is a Data Warehouse?
A Data Warehouse is a centralized repository where large volumes of data from multiple sources are cleaned, structured, and organized for analysis and reporting — as opposed to operational databases, which are optimized for daily transactions.

## Why do we need one?

Consider a wholesale organization that supplies goods on a day-to-day basis. To track profit margins and improve profitability, the CEO needs reliable data to analyze trends and forecast demand. However, with a huge stock turnover, raw transactional data is too large and messy to analyze directly.

To solve this, the organization hires:

A Data Engineer, who builds pipelines to extract, clean, transform, and organize the raw data into a structured, query-ready warehouse.
A BI Analyst, who uses this curated data to generate reports, dashboards, and insights for decision-making.

## 🏗️ Total Architecture

This project follows the **Medallion Architecture** pattern, which organizes data into three progressive layers — **Bronze**, **Silver**, and **Gold** — as it flows from raw source systems to business-ready insights.

![Data Warehouse Architecture](docs/architecture/datawarehouse_diagram.png)

### 1. Source Layer
Raw data originates from two operational systems:
| Source | Format | Interface |
|---|---|---|
| **CRM** | CSV files | Folders and files |
| **ERP** | CSV files | Folders and files |

These are the systems the business uses day-to-day — they aren't optimized for analytics, only for transactions.

### 2. Data Warehouse Layer (Bronze → Silver → Gold)

**🥉 Bronze Layer — Raw Zone**
- **Objective:** Store raw, unprocessed data exactly as received from source
- **Objects:** Tables
- **Load Type:** Batch Processing, Full Load (Truncate & Insert)
- No transformations happen here — it's a landing zone that preserves the original data for traceability and reprocessing.

**🥈 Silver Layer — Cleansed Zone**
- **Objective:** Clean and transform the raw data into a consistent, trustworthy format
- **Objects:** Tables
- **Load Type:** Full Load
- **Transformations:**
  - Data cleaning
  - Data normalization
  - Data standardization
  - Derived columns
  - Data enrichment

**🥇 Gold Layer — Business/Curated Zone**
- **Objective:** Deliver business-ready, query-optimized data
- **Objects:** Views
- **Load Type:** No load (transformation-only layer)
- **Transformations:**
  - Data integration (joining across sources)
  - Aggregations
  - Business logic

### 3. Consumption Layer
The Gold layer feeds directly into how the business actually uses the data:
- **BI & Reports** — dashboards (e.g., Power BI)
- **Ad-hoc SQL** — analysts querying directly for exploratory analysis
- **Machine Learning** — curated data feeding predictive models

### Why this layered approach?
Each layer has a single responsibility, which makes the pipeline easier to debug, reprocess, and scale:
- **Bronze** = "What did we receive?" (audit trail)
- **Silver** = "What can we trust?" (clean, validated data)
- **Gold** = "What does the business need?" (ready-to-consume insights)

This separation means a BI analyst never touches messy raw data, and a bug in transformation logic can be traced back to a specific layer instead of the entire pipeline.
                  
