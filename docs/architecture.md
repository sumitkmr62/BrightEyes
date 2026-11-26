# BrightEyes Project Architecture

## 1. Architecture scope

The initial implementation is local-first. Development and pipeline execution take place under `E:\BrightEyes`. GitHub is the required remote repository for version control.

## 2. Logical architecture

Business source files
        |
        v
Python ingestion and validation
        |
        v
Raw Parquet datasets
        |
        v
PySpark transformations
        |
        v
Processed Parquet datasets
        |
        v
SQL Server staging and warehouse tables
        |
        v
SQL Server incentive calculations and audit
        |
        v
Python PDF generation and email distribution