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

## Input checklist

Confirm or ask for:

- stack and framework
- sandbox or production target
- `entryType`
- `fundingType`
- `intent`
- whether the flow is one-off or recurring
- whether downstream state updates come from polling or webhooks

## Decision rules

- If the goal is to reserve funds first, prefer `Authorisation`.
- If the goal is to take funds immediately after approval, prefer `Purchase`.
- If the amount is not final yet, evaluate `EstimatedAuthorisation`.
- If the goal is to validate a card without charging it, prefer `Verification`.
- If a later action depends on the initial transaction, call out the follow-up modification path explicitly.
- If recurring or stored credential behavior is mentioned, ask whether Token Vault should be part of the design.

## Response template

Use this structure:

1. Transaction goal
2. Required transaction fields
3. Proposed request flow
4. Expected states and how to handle them
5. Provider response fields worth storing
6. Open questions or placeholders

## Example prompts

- `Create a minimal Node.js purchase flow for PXP e-commerce card payments`
- `Design a MOTO authorisation flow and explain what state changes I should persist`
- `Show me how to model refund handling after a successful purchase`
- `Help me choose between Authorisation, Purchase, and Verification for this use case`

## Guardrails

- Do not invent unsupported payment methods or hidden states.
- Treat `providerResponse` as valuable reconciliation and troubleshooting data.
- If recurring payments are discussed, ask whether gateway tokens or scheme tokens should be introduced.
