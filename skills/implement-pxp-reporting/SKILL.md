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
3. If scheduling is required, check whether the user has merchant group scope and a saved query to schedule from.
4. Model how generated reports are retrieved, downloaded, stored, and processed.
5. If webhooks are involved, route reporting events through the shared webhook handling path.

## Input checklist

Confirm or ask for:

- ad-hoc or scheduled reporting
- portal-driven or system-ingestion workflow
- recipient list and permissions model
- file format expectations
- reconciliation or finance use case
- whether webhook notifications are needed

## Decision rules

- If the need is repeatable operations, prefer scheduled reports over manual exports.
- If the consumer is another internal system, model ingestion and storage explicitly instead of stopping at CSV download.
- If the expected volume is high, call out the documented export limit and avoid assuming browser export is enough.
- If the workflow depends on report readiness events, include the reporting webhook path.

## Response template

1. Reporting goal
2. Query and scheduling setup
3. Delivery or ingestion path
4. Volume and format constraints
5. Reconciliation considerations
6. Open questions

## Example prompts

- `Plan a scheduled PXP reporting workflow for daily reconciliation`
- `Show me how to turn a saved query into an operational reporting process`
- `Design a reporting webhook consumer for scheduled report generation`
- `Explain the limits of browser export versus scheduled reporting`

## Reporting integration advice

- Keep report generation concerns separate from payment initiation logic.
- Plan for asynchronous processing and delayed availability.
- If the business needs reconciliation, map report fields to internal settlement or finance concepts explicitly.
- Exports are CSV-oriented and the docs cap direct export at 10,000 transactions.
- Scheduled reports are built from saved queries and can notify recipients or webhook consumers when ready.

## Guardrails

- Do not assume reporting is real-time.
- Prefer repeatable scheduled workflows over manual one-off steps when the user needs ongoing reconciliation.
- Do not design around unlimited browser exports when the documented export limit is lower.
