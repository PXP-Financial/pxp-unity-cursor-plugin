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

## Relevant webhook events

- scheme token created
- scheme token creation error
- scheme token card updated
- scheme token disabled

## Guardrails

- Avoid exposing raw card data beyond the narrowest documented path.
- Do not assume gateway tokens and scheme tokens are interchangeable.
- If recurring payments are required immediately, explain when gateway tokens can be available before scheme token provisioning completes.
