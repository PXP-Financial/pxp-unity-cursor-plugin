---
name: implement-pxp-transactions
description: Implement PXP Unity transactions for e-commerce, MOTO, or in-store payments. Use when the user needs help initiating or modifying transactions, choosing intents, or handling transaction states and provider responses.
---

# Implement PXP Transactions

## Use this skill for

- e-commerce card payments
- MOTO flows
- in-store transaction planning
- authorisation, purchase, refund, payout, or verification flows
- transaction state and provider response handling

## PXP transaction model

When creating or reviewing a transaction flow, make these fields explicit:

- `entryType`
- `fundingType`
- `intent`

Supported documented intents:

- `Authorisation`
- `EstimatedAuthorisation`
- `Purchase`
- `Payout`
- `Refund`
- `Verification`

Documented states to model:

- `Authorised`
- `Captured`
- `Cancelled`
- `Error`
- `Refused`

## Workflow

1. Confirm whether the flow is e-commerce, MOTO, or in-store.
2. Identify the intent and whether later modification is required.
3. Generate the thinnest useful client or service layer.
4. Map response handling around transaction state and provider response data.
5. Add webhook or polling expectations if downstream status updates matter.

## Guardrails

- Do not invent unsupported payment methods or hidden states.
- Treat `providerResponse` as valuable reconciliation and troubleshooting data.
- If recurring payments are discussed, ask whether gateway tokens or scheme tokens should be introduced.
