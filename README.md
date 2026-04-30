# PXP Unity Cursor Plugin

`pxp-unity` is the official Cursor plugin for integrators building against the [PXP developer hub](https://developer.pxp.io/) and the PXP Unity gateway.

It is designed to help developers start faster inside Cursor with reusable skills, commands, and agent prompts for common PXP payment integration work.

## Product coverage

This plugin now guides developers across the main PXP Unity surfaces:

- Transactions
- 3D Secure
- Token Vault
- Checkout, including Components, Drop-in, and Links
- Merchant webhooks
- Risk screening
- Reporting
- Sessions
- Wallet token decryption
- Additional services such as BIN lookup and DCC discovery
- Programmatic Links API patterns

## What this plugin includes

- Skills for bootstrapping a new integration and shaping a payment flow
- Product-specific skills for transactions, 3DS, tokenisation, checkout, webhooks, reporting, and risk screening
- Reference-oriented skills for API auth, Sessions, Wallets, and smaller service APIs
- Commands that help Cursor generate integration code and webhook handling
- A PXP-focused agent profile for implementation planning and review
- A marketplace-ready plugin manifest and logo

## What this plugin does not include yet

- A dedicated PXP MCP server
- Embedded API specs or official SDK code
- Production credentials or account-specific configuration

This version focuses on making Cursor useful for integrators immediately without shipping a non-functional MCP dependency.

## Recommended integrator workflows

After installing the plugin, an integrator can ask Cursor to:

- "Bootstrap a Node.js client for the PXP Unity transactions API"
- "Design a checkout and 3DS flow for my app using PXP"
- "Choose between Components, Drop-in, and Links for this checkout"
- "Create a webhook endpoint for payment status updates"
- "Verify PXP webhook signatures with HMAC headers"
- "Compare token vault and direct card capture approaches for this project"
- "Plan risk screening before authorisation"
- "Handle reporting webhooks and scheduled report downloads"
- "Review my PXP integration for missing edge cases"

## Files

```text
pxp-unity/
├── .cursor-plugin/plugin.json
├── agents/pxp-integration-architect.md
├── assets/logo.svg
├── commands/
│   ├── create-pxp-client.md
│   └── add-pxp-webhook-handler.md
├── skills/
│   ├── bootstrap-pxp-integration/SKILL.md
│   ├── design-pxp-payments-flow/SKILL.md
│   ├── implement-pxp-3ds/SKILL.md
│   ├── implement-pxp-api-auth/SKILL.md
│   ├── implement-pxp-checkout/SKILL.md
│   ├── implement-pxp-reporting/SKILL.md
│   ├── implement-pxp-reference-services/SKILL.md
│   ├── implement-pxp-risk-screening/SKILL.md
│   ├── implement-pxp-sessions/SKILL.md
│   ├── implement-pxp-token-vault/SKILL.md
│   ├── implement-pxp-transactions/SKILL.md
│   ├── implement-pxp-wallets/SKILL.md
│   └── implement-pxp-webhooks/SKILL.md
└── README.md
```

## Integration guidance encoded from PXP docs

- Transactions support e-commerce, MOTO, and in-store flows through one API surface.
- Transaction intents include `Authorisation`, `EstimatedAuthorisation`, `Purchase`, `Payout`, `Refund`, and `Verification`.
- Transaction states include `Authorised`, `Captured`, `Cancelled`, `Error`, and `Refused`.
- 3DS can be used in standalone or integrated mode and should be modeled as a stateful authentication flow.
- 3DS states include `PendingClientData`, `PendingCustomerChallenge`, `AuthenticationSuccessful`, `AuthenticationFailed`, `AuthenticationRejected`, and `AuthenticationError`.
- 3DS fingerprinting is optional but recommended, and the docs call out a 10-second completion window for the 3DS method callback.
- 3DS challenge handling requires posting `creq` to the ACS and waiting for `cres`, with challenge window sizes from compact mobile windows to full screen native flows.
- Integrated 3DS can carry the `authenticationId` directly into transaction authorisation.
- Exemptions are not generic: integrated flows evaluate `LVP` and `TRA`, only one exemption should be applied at a time, and initial card-on-file setup flows should be treated differently.
- Token Vault supports both gateway tokens and scheme tokens, with webhook events for token lifecycle changes.
- Checkout should be chosen by channel and control needs:
  - `Components` for maximum layout and styling control
  - `Drop-in` for the fastest embedded integration
  - `Links` for hosted payment pages and no-code or low-code collection
- Links are web-oriented; Android and iOS can open links, but the docs do not position Links as native SDK support.
- Webhook validation uses `X-Request-Id`, `X-Signature-Timestamp`, and `X-Signature`, with an HMAC over `requestId + timestamp + rawBody`.
- PXP retries failed webhook deliveries up to 10 more times after the first failed attempt, and integrators must handle duplicates safely.
- Duplicate webhook events should be reconciled carefully; the docs note matching identifiers and recommend using the latest event details.
- Risk screening supports both standalone and integrated modes, with pre-authorisation and post-authorisation assessment flows.
- Reporting is portal-oriented today, including saved queries, scheduled reports, CSV export, and webhook notifications for scheduled report generation.
- CSV report exports are capped at 10,000 transactions.
- The API reference surfaces also cover Sessions, Wallet token decryption, BIN lookup, DCC rate, Merchant webhooks, and programmatic Links creation.
- Several service APIs document environment-specific base URLs and HMAC-style authentication requirements such as `PXP-UST1`, request IDs, and client identifiers.

## Suggested starter prompts

- `/bootstrap-pxp-integration build the smallest Node.js transaction client for sandbox use`
- `/implement-pxp-transactions create a purchase flow with explicit state handling`
- `/implement-pxp-3ds design an integrated 3DS flow and explain all state branches`
- `/implement-pxp-checkout help me choose between Components, Drop-in, and Links`
- `/implement-pxp-token-vault design a recurring billing flow using gateway tokens first`
- `/implement-pxp-webhooks create a secure webhook consumer with HMAC validation and duplicate handling`
- `/implement-pxp-risk-screening place risk screening into my payment orchestration`
- `/implement-pxp-reporting plan scheduled report downloads and internal reconciliation`
- `/implement-pxp-api-auth explain how to shape authenticated PXP API requests`
- `/implement-pxp-sessions design a secure payment-details collection flow`
- `/implement-pxp-wallets plan backend wallet token decryption`
- `/implement-pxp-reference-services compare BIN lookup, DCC, and Links API use cases`

## Quick start

After installing the plugin in Cursor:

1. Open a project where you want to build a PXP integration.
2. Ask Cursor one focused question tied to your target flow.
3. Let Cursor generate the smallest useful implementation slice first.
4. Iterate from there with follow-up prompts for webhooks, 3DS, tokens, or reporting.

Suggested first prompts:

- `Build a minimal Express client for PXP Transactions sandbox testing`
- `Help me choose between PXP Components, Drop-in, and Links`
- `Create a secure PXP webhook handler with HMAC validation`
- `Design a recurring billing flow using PXP Token Vault`
- `Plan integrated 3DS with fallback behavior and error handling`

## Support

If you find a bug, docs gap, or integration issue:

- open a GitHub issue in this repository
- include the relevant PXP product area and stack
- include sanitized request or response examples where possible

For platform and account-specific support, use the normal PXP support and onboarding channels.

## Maintenance and limitations

- This plugin is maintained as an open-source integration aid for PXP Unity users.
- It provides guided skills, commands, and workflow help inside Cursor.
- It does not yet ship a live MCP-backed PXP documentation search service.
- Where the public docs do not expose exact endpoint details, the plugin intentionally uses placeholders rather than inventing API behavior.

## Local testing

To test locally, place or symlink this folder into your local Cursor plugins directory:

```bash
~/.cursor/plugins/local/pxp-unity
```

Then reload Cursor and verify the plugin components appear in the marketplace and skills UI.

## Publishing

Marketplace plugins are reviewed manually by Cursor.

Before submission:

1. Publish this plugin from the official repository: <https://github.com/PXP-Financial/pxp-unity-cursor-plugin>
2. Add any missing product-specific content you want reviewers and integrators to see.
3. Submit the repository at <https://cursor.com/marketplace/publish>.

## Next recommended improvements

- Add a real PXP documentation MCP server or searchable docs layer
- Add example commands for Node.js, .NET, Java, and PHP server integrations
