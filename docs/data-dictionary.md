# BrightEyes Data Dictionary

## 1. Purpose

This document defines the planned source and warehouse data concepts. Field names and types are provisional until the source layouts and SQL Server model are agreed.

Use consistent identifiers and date formats across files. Sensitive employee data must be handled only in local, controlled datasets and must not be committed to GitHub.

## 2. Initial business entities

| Entity | Purpose | Candidate identifier |
|---|---|---|
| Employee | Employee identity and employment attributes | `employee_id` |
| Store | Store identity and location attributes | `store_id` |
| Sales | Sales transactions or summarized sales | `sales_record_id` |
| Attendance | Employee attendance by date or period | `attendance_record_id` |
| Target | Assigned target by employee, store, metric, and period | `target_id` |
| Incentive policy | Approved rules applicable to a role or period | `policy_id` |
| Incentive result | Calculated incentive by employee and period | `incentive_result_id` |
| Pipeline run | Execution and processing metadata | `run_id` |

## 3. Candidate field definitions

### Employee

| Field | Meaning | Notes |
|---|---|---|
| `employee_id` | Unique employee identifier | Required business key |
| `employee_name` | Employee display name | Sensitive personal information |
| `store_id` | Store assignment | Relationship to Store |
| `role` | Employee role or designation | Controlled values to be defined |
| `employment_status` | Employment status | Values to be defined |
| `effective_start_date` | Start of record validity | Supports historical changes |
| `effective_end_date` | End of record validity | Nullable for current record |

### Store

| Field | Meaning | Notes |
|---|---|---|
| `store_id` | Unique store identifier | Required business key |
| `store_name` | Store display name |  |
| `city` | Store city |  |
| `state` | Store state |  |
| `region` | Business region | Hierarchy to be defined |
| `effective_start_date` | Start of record validity |  |
| `effective_end_date` | End of record validity | Nullable for current record |

### Sales

| Field | Meaning | Notes |
|---|---|---|
| `sales_record_id` | Unique source record identifier | Source key or generated key |
| `transaction_date` | Date of sale | Required for period assignment |
| `employee_id` | Employee attributed to sale | Attribution rules to be defined |
| `store_id` | Store where sale occurred |  |
| `net_sales_amount` | Net sales amount | Definition and currency to be confirmed |
| `quantity` | Quantity sold | Optional, subject to source data |

### Attendance

| Field | Meaning | Notes |
|---|---|---|
| `attendance_record_id` | Unique attendance record identifier |  |
| `employee_id` | Employee identifier |  |
| `attendance_date` | Date of attendance record |  |
| `attendance_status` | Attendance classification | Values and eligibility impact to be defined |
| `worked_hours` | Recorded hours worked | Required only if policy uses hours |

### Target

| Field | Meaning | Notes |
|---|---|---|
| `target_id` | Unique target record identifier |  |
| `employee_id` | Employee target assignment | Nullable if target is store-level |
| `store_id` | Store target assignment | Nullable if target is employee-level |
| `metric_code` | Metric being targeted | Controlled values to be defined |
| `target_period` | Period to which target applies | Format to be agreed |
| `target_value` | Assigned target value | Units depend on metric |

### Incentive result

| Field | Meaning | Notes |
|---|---|---|
| `incentive_result_id` | Unique result identifier |  |
| `employee_id` | Employee receiving result |  |
| `incentive_period` | Period being calculated | Definition to be approved |
| `policy_id` | Applicable policy identifier |  |
| `rule_version` | Rule version used | Required for traceability |
| `calculated_amount` | Calculated incentive amount | Currency and precision to be confirmed |
| `calculation_status` | Calculation state | Controlled values to be defined |
| `run_id` | Pipeline run that produced result | Links to run metadata |

## 4. Pipeline metadata

Candidate metadata fields include:

- `run_id`
- `source_file_name`
- `source_system`
- `source_period`
- `ingestion_timestamp`
- `record_count`
- `validation_status`
- `load_status`

Exact field types, nullability, keys, and constraints will be finalized in the SQL Server model and source file specifications.