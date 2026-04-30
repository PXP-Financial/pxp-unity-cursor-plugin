---
name: implement-pxp-wallets
description: Implement PXP wallet token decryption flows. Use when the user needs help decrypting Apple Pay or Google Pay tokens on the backend, extracting payment data, or feeding decrypted wallet data into payment or fraud workflows.
---

# Implement PXP Wallets

## Use this skill for

- Apple Pay token decryption planning
- Google Pay token decryption planning
- backend wallet processing flows
- connecting wallet payloads to payment, fraud, or token-vault workflows

## Reference-backed use cases

The API reference positions wallet decryption for:

- transaction processing
- fraud detection and risk assessment
- compliance and audit handling
- custom payment workflows
- token vault integration
- 3DS-related processing context

## Input checklist

Confirm or ask for:

- Apple Pay or Google Pay
- backend language and framework
- what the decrypted payload is needed for
- whether the flow feeds a normal transaction, fraud check, or token-vault process
- what data should be persisted versus discarded

## Decision rules

- If the merchant only needs standard wallet processing through existing SDK flows, avoid overcomplicating with unnecessary backend decryption steps.
- If the merchant needs backend control, custom fraud logic, or custom routing, place wallet decryption early in the orchestration flow.
- If token reuse is required after decryption, connect the design to Token Vault rather than treating decrypted card data as long-term storage.

## Response template

1. Wallet flow goal
2. Decryption entry point
3. Downstream use of decrypted data
4. Storage and security boundaries
5. Integration with transactions, fraud, or tokens
6. Open questions

## Example prompts

- `Design a backend Apple Pay token decryption flow for PXP`
- `Show me how Google Pay token decryption feeds into transaction processing`
- `Explain when wallet decryption should connect to fraud checks or Token Vault`

## Guardrails

- Do not suggest storing decrypted card data longer than necessary.
- Do not invent wallet-specific fields that are not documented.
- Keep security boundaries and downstream data minimization explicit.
