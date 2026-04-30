---
name: implement-pxp-checkout
description: Choose and implement the right PXP checkout mode. Use when the user needs help deciding between Components, Drop-in, and Links, or when implementing Web, Android, or iOS checkout experiences.
---

# Implement PXP Checkout

## Decision guide

Use the documented checkout positioning:

- `Components`: maximum control over layout, fields, and styling
- `Drop-in`: fastest embedded checkout with a pre-built UI
- `Links`: hosted payment pages for web and shareable payment collection

## Platform hints

- Components and Drop-in are positioned across Web, Android, and iOS.
- Links are web-oriented. Mobile devices can open links, but Links is not positioned as a native Android or iOS SDK flow.

## Workflow

1. Ask whether the merchant needs embedded checkout or a hosted payment page.
2. Ask how much design control is required.
3. Ask how quickly the team needs to go live.
4. Recommend one primary checkout mode and optionally a secondary option.
5. Generate only the integration slice for the selected mode.

## Input checklist

Confirm or ask for:

- target platform: Web, Android, or iOS
- embedded checkout or hosted payment page
- desired go-live speed
- required branding and layout control
- required payment methods
- whether recurring or MIT behavior is needed

## Decision tree

- If the merchant needs a hosted page they can share, recommend `Links`.
- If the merchant needs an embedded experience and wants the fastest path, recommend `Drop-in`.
- If the merchant needs embedded checkout and strong control over layout and styling, recommend `Components`.
- If the platform is Android or iOS, do not position `Links` as a native SDK solution.
- If the answer is not obvious, provide one primary option and one fallback with the trade-off spelled out.

## Output template

1. Recommended checkout product
2. Why it fits this merchant
3. Platform support assumptions
4. Integration sequence
5. Open questions around branding, payment methods, and recurring payments

## Example prompts

- `Help me choose between PXP Components and Drop-in for a React checkout`
- `Recommend the right PXP checkout mode for an Android app`
- `We need a hosted payment page with minimal build effort. What should we use?`
- `Design a branded embedded checkout with room for later recurring payments`

## Guardrails

- Do not recommend Links as a native mobile SDK path.
- Prefer Components when the user needs full control over field placement.
- Prefer Drop-in when speed matters more than layout freedom.
