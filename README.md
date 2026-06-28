# Enterprise-Data-Pipeline-Portfolio
# World Bank Sovereign Macroeconomic ETL Pipeline

An end-to-end data pipeline built in Databricks that extracts, cleans, and structures key macroeconomic indicators for 12 global economies from 2000 to the present. 

*Designed with enterprise-grade compliance frameworks and defense-sector data integrity principles to ensure auditable, mission-critical downstream consumption.*

## 📁 Repository Structure & Data Provenance
* `worldbank_data/raw/`: **Immutable Ingestion Layer** holding pristine API snapshots. Serves as a regulatory audit trail (SOX compliance) and guarantees strict chain-of-custody/data provenance.
* `worldbank_data/processed/`: **Silver Layer** containing deterministic, cleaned data ready for production-level analytical downstream consumption or predictive modeling.

## 🛠️ Phase 1: Ingestion & Data Quality Engineering

### 1. Contextual Imputation Strategy
Raw global macroeconomic data frequently suffers from irregular reporting windows, market latency, and varying release gaps across nations. To resolve this without introducing statistical bias, this pipeline implements a **Chronological Group-By Forward-Fill (`ffill`)** partitioned by country context. 

* **Corporate Use-Case:** Mitigates reporting lag in multi-national corporate portfolios.
* **Defense/GovTech Use-Case:** Models data resilience by handling intermittent signal/telemetry drops or asynchronous reporting schedules in disjointed environments.

### 2. Algorithmic Quality Flags (Data SLAs & Mission Readiness)
To protect downstream analytics, BI dashboards, or machine learning models from silent data degradation, a custom validation column was engineered:
* `is_complete_record`: A binary flag (`1` or `0`) evaluating core tracking pillars (GDP growth, debt-to-gdp, inflation, and unemployment). A value of `1` indicates a fully intact data matrix for that specific country-year, enforcing a strict Data SLA (Corporate) and establishing automated data-trust verification for mission-readiness (Defense).

## 💻 Tech Stack
* **Platform:** Databricks (Serverless Elastic Compute)
* **Languages & Tools:** Python (Pandas), PySpark, and Spark Temporary Views.