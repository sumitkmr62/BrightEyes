# BrightEyes Data Engineering Project

## Project overview

BrightEyes is a fictional eyewear retailer with 170 stores across India and approximately 5–7 employees per store. Its headquarters is in Gurugram.

The project builds a centralized data engineering system to calculate employee incentives, produce incentive statements as PDFs, and distribute statements and related reports by email on a weekly schedule.

The system is designed to support additional business processes later.

## Objectives

- Centralize incentive inputs and calculation logic.
- Build repeatable, testable data ingestion and transformation pipelines.
- Preserve calculation results and supporting audit information.
- Generate employee incentive statements and management reports.
- Automate execution, monitoring, and failure recovery.
- Keep the implementation modular so new business processes can be added.

## Technology stack

| Area | Technology |
|---|---|
| Development environment | Local, `E:\BrightEyes` |
| Version control | Git and GitHub |
| Relational database | SQL Server |
| File processing | Python, PySpark, Spark SQL |
| File formats | CSV, Excel, Parquet, JSON, XML |
| Orchestration | Apache Airflow |
| Employee statements | PDF generation with Python |
| Distribution | Email automation |

Exact software versions and package dependencies will be recorded when the environment is configured.

## High-level data flow

1. Receive source files for sales, attendance, employee information, targets, and incentive rules.
2. Ingest files and validate their structure and contents.
3. Use PySpark to clean, standardize, and transform file-based data.
4. Store raw and processed datasets in Parquet.
5. Load validated datasets into SQL Server.
6. Apply incentive business rules in SQL Server.
7. Generate incentive PDFs and reconciliation reports.
8. Distribute outputs by email.
9. Use Airflow to schedule, coordinate, monitor, and retry pipeline tasks.

## Repository structure

BrightEyes/
├── docs/
├── data/
│   ├── source/
│   ├── raw/
│   ├── processed/
│   └── samples/
├── src/
│   └── brighteyes/
├── sql/
│   ├── database/
│   ├── schemas/
│   ├── tables/
│   ├── procedures/
│   └── seed/
├── airflow/
│   └── dags/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── data_quality/
├── scripts/
├── .gitignore
├── README.md
└── requirements.txt