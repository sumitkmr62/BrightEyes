
# BrightEyes Source Data Contracts

## Scope

The first pipeline accepts five CSV datasets: stores, employees, sales, attendance, and targets.

All development records must be synthetic. Dates use ISO format (`YYYY-MM-DD`), and monetary values use decimal precision rather than floating-point types.

## 1. Stores

**File:** `stores.csv`
**Grain:** One row per store
**Primary key:** `store_id`

| Column | Type | Required | Meaning |
|---|---|---:|---|
| store_id | string | Yes | Stable store identifier |
| store_name | string | Yes | Store display name |
| city | string | Yes | City |
| state | string | Yes | State |
| region | string | No | Business region |

## 2. Employees

**File:** `employees.csv`
**Grain:** One row per employee for this initial snapshot
**Primary key:** `employee_id`
**Foreign key:** `store_id` references Stores

| Column | Type | Required | Meaning |
|---|---|---:|---|
| employee_id | string | Yes | Stable employee identifier |
| employee_name | string | Yes | Synthetic employee name |
| store_id | string | Yes | Assigned store |
| role | string | Yes | Employee role |
| employment_status | string | Yes | Employment status |

This initial version assumes one current store assignment per employee. Historical transfers are out of scope until specified.

## 3. Sales

**File:** `sales.csv`
**Grain:** One row per sales transaction
**Primary key:** `sales_record_id`
**Foreign keys:** `employee_id` references Employees; `store_id` references Stores

| Column | Type | Required | Meaning |
|---|---|---:|---|
| sales_record_id | string | Yes | Unique transaction identifier |
| transaction_date | date | Yes | Transaction date |
| employee_id | string | Yes | Employee attributed to the transaction |
| store_id | string | Yes | Store where the transaction occurred |
| net_sales_amount | decimal(12,2) | Yes | Synthetic net sales amount |
| transaction_status | string | Yes | Transaction status |

The meaning of net sales, returns, cancellations, and attribution must be confirmed before incentive calculations are implemented.

## 4. Attendance

**File:** `attendance.csv`
**Grain:** One row per employee per attendance date
**Primary key:** `attendance_record_id`
**Foreign key:** `employee_id` references Employees

| Column | Type | Required | Meaning |
|---|---|---:|---|
| attendance_record_id | string | Yes | Unique attendance record identifier |
| employee_id | string | Yes | Employee identifier |
| attendance_date | date | Yes | Attendance date |
| attendance_status | string | Yes | Source attendance classification |
| worked_hours | decimal(5,2) | No | Recorded hours worked |

Allowed attendance statuses and their incentive impact are not yet defined.

## 5. Targets

**File:** `targets.csv`
**Grain:** One row per employee, metric, and target period
**Primary key:** `target_id`
**Foreign key:** `employee_id` references Employees

| Column | Type | Required | Meaning |
|---|---|---:|---|
| target_id | string | Yes | Unique target identifier |
| employee_id | string | Yes | Employee receiving the target |
| metric_code | string | Yes | Targeted metric |
| period_start | date | Yes | First date of target period |
| period_end | date | Yes | Last date of target period |
| target_value | decimal(12,2) | Yes | Assigned target value |

The first synthetic dataset uses individual sales targets. Store-level targets and target proration are not included yet.

## Initial validation rules

- Required fields must not be null or blank.
- Primary keys must be unique within each file.
- Employee and store references must resolve.
- Dates must parse using the declared format.
- Amounts and targets must parse as decimals.
- Invalid records must be reported and excluded from downstream calculations.
- The pipeline must retain source filename and ingestion run metadata.