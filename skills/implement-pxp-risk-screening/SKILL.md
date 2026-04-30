---
name: implement-pxp-risk-screening
description: Design PXP transaction risk screening flows. Use when the user needs help placing fraud screening before or after authorisation, interpreting Omniscore, or wiring screening decisions into payment orchestration.
---

# Implement PXP Risk Screening

## What this service does

PXP risk screening evaluates fraud risk before or after authorisation and returns a recommendation informed by Kount analysis and merchant-configured rules.

## Key concepts

- screening can be standalone or integrated into payment processing
- Kount returns an `Omniscore`
- the score informs decisioning, but merchant rules determine the final outcome

## Workflow

1. Ask whether screening should run before or after authorisation.
2. Identify which service owns the accept or reject decision.
3. Model the handoff between screening, payment orchestration, and final transaction processing.
4. Show how the result affects customer experience and operational workflows.

## Guardrails

- Do not present Omniscore as the sole decision.
- Keep screening recommendations separate from the final merchant decision.
- Call out how false positives or manual review would affect the wider payment flow.
