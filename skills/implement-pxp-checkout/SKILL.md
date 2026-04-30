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

## Output template

1. Recommended checkout product
2. Why it fits this merchant
3. Platform support assumptions
4. Integration sequence
5. Open questions around branding, payment methods, and recurring payments

## Guardrails

- Do not recommend Links as a native mobile SDK path.
- Prefer Components when the user needs full control over field placement.
- Prefer Drop-in when speed matters more than layout freedom.
