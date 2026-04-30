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

1. Ask whether the merchant wants standalone or integrated risk screening.
2. Ask whether screening should run before or after authorisation.
3. Identify which service owns the accept or reject decision.
4. Model the handoff between screening, payment orchestration, and final transaction processing.
5. Show how the result affects customer experience and operational workflows.

## Input checklist

Confirm or ask for:

- standalone or integrated deployment
- pre-authorisation or post-authorisation assessment
- which system owns the final decision
- whether capture, void, or manual review paths exist
- what customer experience is acceptable on risky transactions

## Decision tree

- If the merchant wants to block fraud before issuer processing, prefer pre-authorisation screening.
- If the merchant needs immediate issuer approval first, consider post-authorisation screening.
- If the payment stack is already centered on PXP orchestration, integrated mode is usually simpler.
- If the merchant wants screening independent of gateway processing, use standalone mode.

## Response template

1. Screening mode
2. Assessment timing
3. Decision ownership
4. Transaction orchestration impact
5. Customer and operations impact
6. Open questions

## Example prompts

- `Design a pre-authorisation risk screening flow for PXP`
- `Compare standalone and integrated PXP risk screening for this architecture`
- `Show me how post-authorisation screening changes capture and void behavior`
- `Explain how Omniscore should influence but not replace merchant decisioning`

## Assessment modes

- Pre-authorisation: assess risk before the issuer authorisation request is sent
- Post-authorisation: assess risk after issuer authorisation and decide whether to capture or void

## Integration modes

- Standalone: separate fraud screening integration, independent of payment gateway orchestration
- Integrated: screening is embedded into the PXP transaction lifecycle

## Guardrails

- Do not present Omniscore as the sole decision.
- Keep screening recommendations separate from the final merchant decision.
- Call out how false positives or manual review would affect the wider payment flow.
- Make it explicit whether post-authorisation screening leads to capture, hold, or void behavior.
