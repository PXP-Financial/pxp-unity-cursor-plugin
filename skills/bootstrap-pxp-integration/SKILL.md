---
name: bootstrap-pxp-integration
description: Bootstrap a new integration against the PXP Unity gateway. Use when a user wants to set up a first PXP project, create a payment client, identify required credentials, or generate a first end-to-end API flow.
---

# Bootstrap PXP Integration

## Goal

Help the user go from "I need to integrate PXP Unity" to a working project skeleton with clear assumptions, first API calls, and a safe implementation plan.

## Workflow

1. Confirm the target stack and runtime.
2. Ask which PXP product area is in scope:
   - Transactions
   - 3D Secure
   - Token Vault
   - Checkout
   - Risk screening
   - Reporting
   - Sessions or payment data collection
   - Additional services such as BIN lookup or DCC
3. Identify missing inputs before generating code:
   - environment or sandbox usage
   - base URL if provided by the user or docs
   - API credentials or authentication model
   - webhook URLs
   - idempotency or retry expectations
   - entry type, funding type, and intent for transactions
4. Use the PXP developer hub as the source of truth for product docs and endpoint guidance.
5. Generate a minimal implementation that is easy to extend, not a giant abstraction layer.

## Implementation defaults

- Prefer a thin API client over a large SDK.
- Keep secrets in environment variables.
- Separate transport, request models, and business flow logic.
- Add explicit error handling for gateway failures, validation failures, and timeout or retry scenarios.
- Make webhook verification and signature handling explicit when the product flow uses callbacks.
- If Checkout is in scope, choose intentionally between Components, Drop-in, and Links.
- If Tokens are in scope, distinguish gateway tokens from scheme tokens clearly.
- If 3DS is in scope, model the authentication state machine and callback path explicitly.

## Output shape

When asked to build or plan a new integration, structure the response as:

1. Assumptions
2. Required credentials and configuration
3. Minimal project structure
4. First request or transaction flow
5. Error handling and webhook notes
6. Next steps

## PXP references

Start with these docs and follow the most specific product page available:

- <https://developer.pxp.io/guides/get-started>
- <https://developer.pxp.io/apis>
- <https://developer.pxp.io/guides/transactions>
- <https://developer.pxp.io/guides/3ds>
- <https://developer.pxp.io/guides/token-vault>
- <https://developer.pxp.io/guides/checkout>
- <https://developer.pxp.io/guides/risk-screening>
- <https://developer.pxp.io/guides/reporting>
- <https://developer.pxp.io/guides/get-started/about-webhooks>
- <https://developer.pxp.io/guides/get-started/manage-webhooks>

## Guardrails

- Do not invent endpoint paths, credentials, or headers when the user has not provided them.
- If documentation details are missing, call out placeholders clearly.
- Avoid storing raw card data unless the documented flow explicitly requires it and the user asks for it.
- Prefer describing transaction states and webhook events using the names from the PXP docs.
