---
name: implement-pxp-token-vault
description: Implement PXP Token Vault flows. Use when the user needs help with gateway tokens, scheme tokens, cryptograms, browser tokenisation, recurring payments, or token lifecycle webhooks.
---

# Implement PXP Token Vault

## Token types

- `Gateway tokens`: merchant-scoped tokens for local payment ecosystem use and recurring billing
- `Scheme tokens`: network tokens that work across the broader payment ecosystem and support cryptographic verification

## Use this skill for

- recurring billing design
- stored credential flows
- browser-based tokenisation planning
- deciding between gateway tokens and scheme tokens
- handling token lifecycle webhooks

## Workflow

1. Ask whether the merchant needs local token reuse, scheme-level portability, or both.
2. If both are needed, explain the combined approach and why it helps.
3. Map token creation, storage, payment usage, and revocation or update handling.
4. If scheme tokens are involved, surface the webhook events that signal readiness or changes.

## Input checklist

Confirm or ask for:

- recurring billing or one-click payment use case
- gateway tokens, scheme tokens, or both
- browser tokenisation or backend tokenisation path
- need for cryptograms
- token lifecycle webhook handling expectations
- whether immediate payment use is required before scheme token readiness

## Decision rules

- If the user needs merchant-scoped recurring reuse quickly, start with gateway tokens.
- If the user needs broader ecosystem portability or network token advantages, evaluate scheme tokens.
- If the user needs both fast initial availability and longer-term portability, describe the combined approach.
- If the payment flow depends on token readiness events, include webhook handling in the plan.

## Response template

1. Token strategy
2. Creation flow
3. Storage and payment usage
4. Webhook events to consume
5. Security and PCI handling notes
6. Open questions

## Example prompts

- `Design a recurring billing flow using PXP gateway tokens`
- `Compare gateway tokens and scheme tokens for this subscription product`
- `Show me a combined token strategy for fast signup and long-term reuse`
- `Plan the webhook handling needed for scheme token lifecycle events`

## Relevant webhook events

- scheme token created
- scheme token creation error
- scheme token card updated
- scheme token disabled

## Guardrails

- Avoid exposing raw card data beyond the narrowest documented path.
- Do not assume gateway tokens and scheme tokens are interchangeable.
- If recurring payments are required immediately, explain when gateway tokens can be available before scheme token provisioning completes.
