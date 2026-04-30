---
name: implement-pxp-reporting
description: Implement PXP reporting workflows. Use when the user needs help creating transaction reports, scheduling recurring reports, exporting CSVs, or handling reporting webhook notifications.
---

# Implement PXP Reporting

## Use this skill for

- ad-hoc report generation
- scheduled report workflows
- CSV export and downstream ingestion
- reporting webhook handling
- reconciliation-oriented integration planning

## Workflow

1. Ask whether the use case is ad-hoc reporting or scheduled reporting.
2. Determine who consumes the result: humans, internal systems, or both.
3. Model how generated reports are retrieved, downloaded, stored, and processed.
4. If webhooks are involved, route reporting events through the shared webhook handling path.

## Reporting integration advice

- Keep report generation concerns separate from payment initiation logic.
- Plan for asynchronous processing and delayed availability.
- If the business needs reconciliation, map report fields to internal settlement or finance concepts explicitly.

## Guardrails

- Do not assume reporting is real-time.
- Prefer repeatable scheduled workflows over manual one-off steps when the user needs ongoing reconciliation.
