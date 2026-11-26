# BrightEyes Incentive Business Rules

## 1. Status

This document is the controlled location for incentive calculation rules.

The rules below describe the initial calculation framework.

## 2. Calculation grain

The intended calculation grain is:

- One employee.
- One incentive period.
- One applicable incentive policy or rule set.

## 3. Proposed calculation sequence

1. Identify the employee and applicable incentive period.
2. Validate required employee, sales, attendance, target, and policy inputs.
3. Determine eligibility using approved rules.
4. Calculate achievement measures using approved definitions.
5. Apply approved thresholds, slabs, rates, caps, and adjustments.
6. Store the result with the applicable rule version and processing run.
7. Reconcile results and identify exceptions.
8. Generate the employee statement after the result is approved for distribution.

## 4. Rule management

Each approved rule set should have:

- A unique rule or policy identifier.
- An effective start date and, where applicable, an end date.
- A documented calculation definition.
- An approval status and approval reference.
- A version or change history.

A rule change must not silently alter previously finalized calculations. The system must be able to identify which rule version was used for a calculation.

## 5. Data and exception handling

- Missing required inputs must be flagged.
- Invalid or conflicting records must be quarantined or marked as exceptions.
- The system must not silently substitute zero for missing business values unless an approved rule explicitly requires it.
- Recalculations must retain the prior result or sufficient history to explain the change.
- Duplicate source records must be detected using agreed business keys.

## 6. Decisions to finalize

The business must define and approve:

- Incentive components and calculation formulas.
- Employee eligibility and attendance treatment.
- Sales attribution and store-level attribution.
- Target assignment and target proration.
- Thresholds, achievement slabs, payout rates, and caps.
- Treatment of returns, cancellations, corrections, and late data.
- Rounding and currency precision.
- Approval, finalization, and payment handoff rules.
- PDF content and distribution permissions.

No numerical payout rule should be implemented until its definition and test examples are approved.