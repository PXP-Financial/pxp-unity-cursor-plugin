---
name: implement-pxp-reference-services
description: Implement smaller or auxiliary PXP service APIs. Use when the user needs help with BIN lookup, DCC rate checks, programmatic Links creation, or choosing between auxiliary PXP service APIs for a broader integration.
---

# Implement PXP Reference Services

## Scope

Use this skill for smaller API-reference-driven services that support the main payment flow.

## Covered services

- BIN lookup
- DCC rate
- Links API

## What each service is for

- BIN lookup: identify card metadata such as issuer, card type, and funding source
- DCC rate: retrieve exchange-rate information for Dynamic Currency Conversion scenarios
- Links API: create secure payment links programmatically with configurable payment behaviors

## Input checklist

Confirm or ask for:

- which auxiliary service is needed
- where in the customer journey it should run
- whether the output feeds UI decisions, payment orchestration, or ops workflows
- whether the service is one-off, per-transaction, or batch-like

## Decision rules

- If the merchant needs card metadata before deeper payment handling, use BIN lookup.
- If the merchant needs currency-conversion logic or pricing support, use DCC rate.
- If the merchant needs hosted payment collection created by backend systems, use the Links API.
- If the service changes the checkout experience directly, explain where it fits relative to checkout, transactions, and webhooks.

## Response template

1. Service choice
2. Why it fits the use case
3. Request timing in the wider flow
4. Output handling
5. Security and operational notes
6. Open questions

## Example prompts

- `Show me where BIN lookup belongs in a PXP checkout flow`
- `Design a backend flow that creates a payment link with the PXP Links API`
- `Explain how DCC rate retrieval should fit into a payment experience`

## Guardrails

- Do not invent rate, token, or link configuration fields without a documented source.
- Keep auxiliary services tied to the wider user journey rather than treating them as isolated APIs.
