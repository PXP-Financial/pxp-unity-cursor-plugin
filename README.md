# PXP Unity Cursor Plugin

`pxp-unity` is the official Cursor plugin starter for integrators building against the [PXP developer hub](https://developer.pxp.io/) and the PXP Unity gateway.

It is designed to help developers start faster inside Cursor with reusable skills, commands, and agent prompts for common payment integration work.

## What this plugin includes

- Skills for bootstrapping a new integration and shaping a payment flow
- Commands that help Cursor generate integration code and webhook handling
- A PXP-focused agent profile for implementation planning and review
- A marketplace-ready plugin manifest and logo

## What this plugin does not include yet

- A dedicated PXP MCP server
- Embedded API specs or official SDK code
- Production credentials or account-specific configuration

The first version focuses on making Cursor useful for integrators immediately without shipping a non-functional MCP dependency.

## Recommended integrator workflows

After installing the plugin, an integrator can ask Cursor to:

- "Bootstrap a Node.js client for the PXP Unity transactions API"
- "Design a checkout and 3DS flow for my app using PXP"
- "Create a webhook endpoint for payment status updates"
- "Compare token vault and direct card capture approaches for this project"
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
│   └── design-pxp-payments-flow/SKILL.md
└── README.md
```

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
- Add more product-specific skills for Transactions, 3DS, Checkout, and Token Vault
- Add example commands for Node.js, .NET, Java, and PHP server integrations
