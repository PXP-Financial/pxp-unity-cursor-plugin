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

## Input checklist

Confirm or ask for:

- standalone or integrated 3DS
- browser or native app flow
- whether SCA is expected to apply
- callback URLs for fingerprinting and challenge completion
- whether exemptions are in scope
- whether the transaction is an initial card-on-file setup

## Decision rules

- If the user uses PXP for payment processing too, prefer integrated 3DS unless there is a reason to separate concerns.
- If `threeDSecureSupported` is false, explain the non-3DS fallback and liability implications.
- If the response reaches `PendingCustomerChallenge`, model the full challenge path and callback handling.
- If `AuthenticationRejected`, stop the authorisation path.
- If `AuthenticationFailed` or `AuthenticationError`, surface retry or fallback behavior explicitly and mention liability shift loss.
- If both `LVP` and `TRA` are available in integrated flows, prefer `TRA` unless the business has a reason not to.

## Response template

Use this structure:

1. 3DS mode and assumptions
2. Pre-initiation and fingerprinting steps
3. Frictionless branch
4. Challenge branch
5. Failure and exemption handling
6. Authorisation handoff

## Example prompts

- `Design an integrated PXP 3DS flow for a browser checkout`
- `Explain every possible PXP 3DS state and what my backend should do`
- `Show me a challenge flow with fingerprinting and callback handling`
- `Help me decide when to use an exemption versus a full challenge`

## Guardrails

- Do not reduce 3DS to a single success or failure boolean.
- Make the return path, challenge completion, or webhook update explicit.
- If docs are incomplete for a code example, provide the flow shape and note the missing endpoint details clearly.
- Treat `AuthenticationRejected` as a hard stop for authorisation.
- Treat `AuthenticationFailed` and `AuthenticationError` as no-liability-shift outcomes unless the user explicitly chooses a fallback path.
