---
name: implement-pxp-webhooks
description: Implement secure PXP webhook consumers. Use when the user needs help validating webhook signatures, handling retries and duplicates, processing event categories, or mapping webhook payloads into internal systems.
---

# Implement PXP Webhooks

## Webhook contract

PXP documents these webhook headers:

- `X-Request-Id`
- `X-Signature-Timestamp`
- `X-Signature`

To validate a webhook:

1. Concatenate `requestId + signatureTimestamp + rawBody`
2. Convert that string to UTF-8 bytes
3. Compute the HMAC using the configured HMAC key
4. Base64 encode the result and compare it with `X-Signature`

## Event categories

- `Authentication`
- `Token`
- `Transaction`
- `Reporting`

## Known webhook concerns

- PXP retries failed deliveries
- duplicate events must be handled safely
- the latest event data should win when duplicates arrive with updated timestamps
- failed deliveries may be retried rapidly after the initial attempt

## Workflow

1. Preserve raw request bodies if the framework needs that for signature validation.
2. Verify the signature before parsing or processing business logic.
3. Route by `eventCategory` and event type.
4. De-duplicate on stable event identifiers when available.
5. Return quickly and process downstream work asynchronously when practical.

## Event examples to plan for

- `challenge-completed`
- `transaction-authorised`
- `transaction-cancelled`
- `transaction-captured`
- PayPal transaction lifecycle events
- `scheduled-report-generated`
- scheme token lifecycle events

## Duplicate handling hints

- The docs call out `eventCode` and `systemTransactionId` as key duplicate signals in transaction webhook processing.
- Keep the latest event payload when timestamps differ across duplicates.

## Guardrails

- Do not lose the raw body before HMAC verification.
- Do not trust unsigned or unverifiable requests.
- Make retries and duplicate handling first-class parts of the implementation.
