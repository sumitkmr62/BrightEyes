### `docs/business-requirements.md`

# BrightEyes Business Requirements

## 1. Business context

BrightEyes is a fictional eyewear retailer operating 170 stores across India, with approximately 5–7 employees per store. Its headquarters is in Gurugram.

Incentive calculations currently depend on business information and rules that are scattered across the organization. The project centralizes the inputs, rules, calculations, and outputs.

## 2. Business objective

Build a repeatable system that calculates employee incentives and distributes employee statements and related reports by email every week.

The design should support additional business processes without requiring a complete redesign.

## 3. Stakeholders

| Stakeholder | Expected need |
|---|---|
| Store employees | Receive their incentive statements |
| Store and area leadership | Receive relevant incentive information and reports |
| Business/operations teams | Maintain source data and approve business rules |
| Finance | Reconcile calculated incentives and payment-related totals |
| Data engineering | Operate ingestion, transformation, calculation, and distribution pipelines |

## 4. Functional requirements

### Source data

- Accept business files in agreed formats, initially including CSV and Excel.
- Support employee, sales, attendance, target, and incentive-rule data.
- Validate required columns, data types, key fields, and business constraints.
- Preserve enough metadata to trace processed records to their source files.

### Processing and calculation

- Standardize source data before it is used in calculations.
- Apply approved incentive rules consistently.
- Support calculation by employee and incentive period.
- Retain calculation results and reconciliation information.
- Identify invalid, missing, or conflicting input data rather than silently treating it as valid.

### Reporting and distribution

- Generate an individual incentive statement in PDF format.
- Generate summary and reconciliation reports for authorized stakeholders.
- Distribute outputs by email on a weekly schedule.
- Record generation and delivery outcomes.

### Operations

- Schedule and monitor the workflow using Airflow.
- Record pipeline runs, failures, and retry outcomes.
- Support safe reruns without unintended duplicate calculations or emails.

## 5. Non-functional requirements

- **Correctness:** calculation results must follow approved business rules.
- **Traceability:** results must be traceable to inputs, processing runs, and rule versions.
- **Reliability:** failures must be visible and recoverable.
- **Maintainability:** code and business rules must be modular and version-controlled.
- **Confidentiality:** employee information and credentials must not be exposed in GitHub.
- **Extensibility:** new source types and business processes should be addable through modular components.

## 6. Initial assumptions

- Development uses synthetic data.
- The first end-to-end workflow covers incentive calculation and PDF distribution.
- SQL Server is the relational warehouse and calculation platform.
- Parquet is used for file-based raw and processed datasets.
- Airflow orchestrates the weekly pipeline.

## 7. Decisions still required

- Exact source file layouts and delivery conventions.
- Incentive components, formulas, thresholds, caps, and eligibility rules.
- Definition of the incentive period and weekly processing window.
- Treatment of corrections, late-arriving data, and recalculations.
- Email recipient hierarchy and delivery rules.
- Approval process for changes to business rules.
- Required retention period for source files, PDFs, and audit history.