---
name: implement-pxp-3ds
description: Implement or design PXP 3D Secure flows. Use when the user needs help with PSD2 and SCA handling, standalone or integrated 3DS, challenge states, exemptions, or 3DS error handling.
---

# Implement PXP 3DS

## Scope

Use this skill when the integration needs cardholder authentication, PSD2 and SCA support, or liability-shift-aware payment design.

## Design steps

1. Decide whether the user needs standalone 3DS or integrated 3DS with payment processing.
2. Identify where the authentication lifecycle begins and which system owns state transitions.
3. Include optional but recommended fingerprinting using the provided fingerprint URL and data.
4. Model the challenge path, completion handling, and any webhook or callback updates.
5. Call out exemptions and exception paths separately from the happy path.
6. Keep the payment step and authentication step linked, but not conflated.

## What to surface

- `PendingClientData`
- `PendingCustomerChallenge`
- `AuthenticationSuccessful`
- `AuthenticationFailed`
- `AuthenticationRejected`
- `AuthenticationError`
- authentication lifecycle states
- issuer challenge handling
- exemption usage
- timeout and failure branches
- post-authentication handoff into transaction processing

## PXP-specific details

- Standalone and integrated flows both use pre-initiation, evaluation, authentication, and optional challenge handling.
- Fingerprinting improves frictionless outcomes and should be attempted when `threeDSecureFingerprintUrl` and `threeDSecureFingerprintData` are returned.
- If the fingerprint callback does not arrive within 10 seconds, continue the flow rather than blocking indefinitely.
- Challenge handling posts `creq` to the ACS and receives `cres` on the configured callback URL.
- `challengeWindowSize` should be chosen deliberately for mobile, desktop, or full-screen native experiences.
- In integrated flows, successful authentication can feed directly into transaction authorisation through `authenticationId`.
- Exemption handling differs between standalone and integrated flows. Integrated flows specifically evaluate `LVP` and `TRA`.
- Initial card-on-file setup flows should not be treated like generic exemption candidates.
- Issuer and scheme data requirements matter. The docs call out minimum fields for Mastercard and Visa that improve or enable compliant authentication flows.

## Guardrails

- Do not reduce 3DS to a single success or failure boolean.
- Make the return path, challenge completion, or webhook update explicit.
- If docs are incomplete for a code example, provide the flow shape and note the missing endpoint details clearly.
- Treat `AuthenticationRejected` as a hard stop for authorisation.
- Treat `AuthenticationFailed` and `AuthenticationError` as no-liability-shift outcomes unless the user explicitly chooses a fallback path.
