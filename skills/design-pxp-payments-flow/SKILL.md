---
name: design-pxp-payments-flow
description: Design a PXP Unity payment flow for web, mobile, or backend services. Use when the user needs architecture help for checkout, 3DS, tokenization, status updates, retries, or webhook-driven payment orchestration.
---

# Design PXP Payments Flow

## Purpose

Turn product requirements into a concrete PXP Unity integration flow that engineers can implement safely.

## Use this skill for

- hosted or embedded checkout planning
- choosing between Components, Drop-in, and Links
- 3DS and authentication branching
- token vault decisions
- webhook and reconciliation design
- retry, idempotency, and failure-state planning
- mapping frontend and backend responsibilities

## Design process

1. Identify the channel:
   - web
   - mobile
   - server to server
   - in-store
2. Identify the payment responsibilities:
   - tokenization
   - authorization
   - capture
   - refund
   - status polling or webhook updates
   - risk screening
   - reporting or reconciliation
3. Map the actors and handoffs:
   - client application
   - merchant backend
   - PXP Unity
   - cardholder authentication step
4. Call out security-sensitive areas:
   - API secrets
   - client-visible tokens
   - raw card data handling
   - webhook verification
5. Produce a sequence the team can implement in order.

## PXP-specific design hints

- For embedded checkout with maximum control, prefer `Components`.
- For the fastest embedded integration, prefer `Drop-in`.
- For shareable hosted payment pages, prefer `Links`.
- Treat 3DS as a separate lifecycle with explicit state transitions and webhook or return-path handling.
- For transactions, capture the intent early because `Authorisation`, `Purchase`, `Refund`, `Payout`, and `Verification` imply different flows.
- Plan webhook-driven state updates for token events, transaction events, authentication events, and reporting events.
- If risk screening is enabled, show where screening happens relative to authorisation and who makes the final accept or reject decision.

## Response template

Use this structure:

### Integration goal

State the target business flow in one short paragraph.

### Proposed architecture

List the participating systems and what each one does.

### End-to-end sequence

Number the full request and response flow from user action through payment completion.

### Failure handling

Cover user cancellation, issuer challenge failure, timeout, duplicate submission, refusal, webhook delay, and duplicate webhook delivery.

### Open questions

List any missing doc details or business decisions that block a final implementation.

## Guardrails

- Prefer server-side control of sensitive payment steps where possible.
- Make idempotency and retry behavior explicit.
- If the user asks for sample code, generate only the slice needed for the chosen flow.
