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
3. Model the challenge path, completion handling, and any webhook or callback updates.
4. Call out exemptions and exception paths separately from the happy path.
5. Keep the payment step and authentication step linked, but not conflated.

## What to surface

- authentication lifecycle states
- issuer challenge handling
- exemption usage
- timeout and failure branches
- post-authentication handoff into transaction processing

## Guardrails

- Do not reduce 3DS to a single success or failure boolean.
- Make the return path, challenge completion, or webhook update explicit.
- If docs are incomplete for a code example, provide the flow shape and note the missing endpoint details clearly.
