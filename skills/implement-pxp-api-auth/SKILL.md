---
name: implement-pxp-api-auth
description: Implement authenticated requests to PXP service APIs. Use when the user needs help shaping PXP-UST1 or HMAC-based requests, choosing sandbox versus production base URLs, or handling request identifiers and client headers.
---

# Implement PXP API Auth

## Use this skill for

- authenticated API client setup
- request-signing guidance
- sandbox versus production environment selection
- shared HTTP client design across PXP services

## Known API reference patterns

- Many PXP service APIs use environment-specific base URLs under `https://api-services.pxp.io/api/v1` and `https://api-services.test.pxp.io/api/v1`.
- Several service APIs document `PXP-UST1` authentication with a header of the form:
  `PXP-UST1 {tokenId}:{timestamp}:{hmac}`
- Some APIs also require request metadata headers such as:
  - `X-Request-Id`
  - `X-Client-Id`

## Input checklist

Confirm or ask for:

- target service API
- sandbox or production environment
- token ID and signing inputs source
- whether a shared HTTP client already exists
- whether request IDs and client IDs need to be generated or injected

## Decision rules

- If multiple PXP services are being integrated, centralize auth and request-header generation in one shared client layer.
- If the docs for a specific service mention extra headers, treat those as service-specific requirements rather than assuming all services are identical.
- If exact signature construction is not fully documented on the current page, preserve the documented format and mark the missing details clearly.

## Response template

1. Environment setup
2. Required headers
3. Signing strategy
4. Client structure
5. Example request shape
6. Open questions

## Example prompts

- `Create a shared Node.js HTTP client for PXP-UST1 authenticated requests`
- `Explain how to structure Authorization, X-Request-Id, and X-Client-Id for PXP APIs`
- `Show me how to separate sandbox and production configuration for PXP`

## Guardrails

- Do not invent undocumented signature inputs.
- Keep credentials and signing secrets out of source files.
- Prefer one reusable auth layer over per-endpoint copy-paste logic.
