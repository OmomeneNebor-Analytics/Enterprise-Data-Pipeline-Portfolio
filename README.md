# Enterprise-Data-Pipeline-Portfolio
# World Bank Sovereign Macroeconomic ETL Pipeline

An end-to-end data pipeline built in Databricks that extracts, cleans, and structures key macroeconomic indicators for 12 global economies from 2000 to the present.

## 📁 Repository Structure
* `worldbank_data/raw/`: Ingestion Layer holding pristine, immutable API snapshots.
* `worldbank_data/processed/`: Silver Layer containing cleaned data ready for analytical downstream consumption.

## 🛠️ Phase 1: Ingestion & Data Quality

### 1. Contextual Imputation Strategy
Raw global macroeconomic data frequently suffers from irregular reporting windows and release gaps across different nations. To resolve this without introducing statistical bias, this pipeline implements a **Chronological Group-By Forward-Fill (`ffill`)** partitioned by country context. This carries the last known valid metric forward over time.

### 2. Algorithmic Quality Flags
To protect downstream analytics, dashboards, or machine learning models from incomplete records, a custom validation column was engineered:
* `is_complete_record`: A binary flag (`1` or `0`) evaluating core tracking pillars (GDP growth, debt-to-gdp, inflation, and unemployment). A value of `1` indicates a fully intact data matrix for that specific country-year.

## 💻 Tech Stack
* **Platform:** Databricks (Serverless Compute)
* **Languages & Tools:** Python (Pandas), PySpark, and Spark Temporary Views.