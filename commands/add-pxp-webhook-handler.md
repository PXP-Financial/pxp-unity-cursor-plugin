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
   - signature verification placeholder if the exact scheme is not documented yet
   - logging and event mapping
   - idempotent processing notes
4. Add test scaffolding only if the project already has a nearby testing pattern.

## Constraints

- Do not assume unsigned callbacks are safe.
- Clearly mark any placeholder verification logic.
- Prefer returning quickly and processing asynchronously if the surrounding architecture supports it.
