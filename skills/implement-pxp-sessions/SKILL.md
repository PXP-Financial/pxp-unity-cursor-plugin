---
name: implement-pxp-sessions
description: Design and implement PXP Sessions flows. Use when the user needs help securely collecting payment details and initiating transactions through a session-based integration.
---

# Implement PXP Sessions

## Purpose

Use this skill when a merchant wants to collect payment details securely before initiating a transaction and needs a session-oriented integration approach.

## What to surface

- where payment details are collected
- how the session fits into checkout orchestration
- how the session hands off into transaction initiation
- what backend and frontend responsibilities should be

## Input checklist

Confirm or ask for:

- web or app integration channel
- who owns UI rendering and payment-detail collection
- whether the session leads into checkout components or direct transaction flow
- whether the merchant backend will create the session
- how session state should be stored or correlated internally

## Decision rules

- If the main goal is secure client-side payment-detail collection, consider Sessions early in the design.
- If the integration already has a clear checkout front end and backend orchestration, model Sessions as the boundary between sensitive data collection and transaction initiation.
- If exact endpoint details are missing from the current public page, explain the session role and keep code placeholders explicit.

## Response template

1. Session goal
2. Frontend and backend responsibilities
3. Session creation and use flow
4. Handoff into transaction processing
5. Security and state-handling notes
6. Open questions

## Example prompts

- `Design a PXP Sessions-based checkout flow for a web app`
- `Show me how a backend should create and use a PXP session before payment`
- `Explain when I should use Sessions instead of collecting payment details directly`

## Guardrails

- Do not claim exact session payload fields unless the docs provide them.
- Keep sensitive data collection boundaries explicit.
- Treat Sessions as part of a larger orchestration flow, not a full checkout design by themselves.
