---
name: add-pxp-webhook-handler
description: Add a PXP Unity webhook or callback handler to the current project.
---

# Add PXP Webhook Handler

Add a webhook endpoint or callback handler suitable for the current stack.

## Steps

1. Inspect the current application routing style.
2. Ask the user for any required verification or signature details if they are not already known.
3. Generate:
   - the route or controller
   - request validation
   - signature verification using PXP's documented HMAC inputs when possible
   - logging and event mapping
   - idempotent processing and duplicate handling
4. Add test scaffolding only if the project already has a nearby testing pattern.

## PXP webhook details

Use these documented headers when implementing verification:

- `X-Request-Id`
- `X-Signature-Timestamp`
- `X-Signature`

Use the raw request body and calculate the signature over:

`requestId + signatureTimestamp + rawBody`

Then compare the Base64 encoded HMAC result with `X-Signature`.

PXP retries failed webhook deliveries, so the handler should be safe when the same event is delivered more than once.

## Constraints

- Do not assume unsigned callbacks are safe.
- Clearly mark any placeholder verification logic.
- Prefer returning quickly and processing asynchronously if the surrounding architecture supports it.
- Preserve access to the raw request body if the framework requires that for HMAC validation.
