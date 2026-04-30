---
name: create-pxp-client
description: Create a minimal PXP Unity API client for the current project and stack.
---

# Create PXP Client

Create a minimal, production-leaning client for the current codebase to talk to PXP Unity.

## Steps

1. Detect the project's main language and HTTP stack.
2. Ask for any missing required information:
   - auth mechanism
   - sandbox or production target
   - base URL
   - required headers
   - target API surface such as Transactions, 3DS, Token Vault, or Sessions
3. Generate:
   - environment variable names
   - a small API client module
   - one example request for the selected PXP product
   - one example error mapping strategy
4. Keep the implementation framework-native and easy for integrators to read.

## PXP transaction defaults

If the user is integrating transactions, ask for or preserve these concepts explicitly:

- `entryType`
- `fundingType`
- `intent`

The documented intents include:

- `Authorisation`
- `EstimatedAuthorisation`
- `Purchase`
- `Payout`
- `Refund`
- `Verification`

## API reference hints

Across the PXP service APIs, preserve these setup concerns when relevant:

- separate sandbox and production base URLs
- service-specific auth headers such as `Authorization`
- correlation headers such as `X-Request-Id`
- service-specific client identifiers such as `X-Client-Id` where documented

## Constraints

- Do not fabricate undocumented endpoints.
- Use placeholders when the docs or user input do not provide concrete values.
- Keep secrets out of source files.
- Reflect documented transaction states and provider response fields when modeling responses.
