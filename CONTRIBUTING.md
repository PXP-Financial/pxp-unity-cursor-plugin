# Contributing

Thanks for contributing to the `pxp-unity` Cursor plugin.

## What to contribute

Useful contributions include:

- better PXP integration skills
- clearer starter prompts
- stronger webhook, 3DS, token, or reporting guidance
- documentation fixes
- new examples for supported stacks

## Contribution guidelines

1. Keep changes accurate to the public PXP docs.
2. Prefer narrow, high-value additions over large speculative rewrites.
3. Do not invent undocumented endpoints, headers, or payload fields.
4. Keep security-sensitive guidance conservative.
5. Preserve the plugin's focus on helping Cursor users ship integrations faster.

## Repository expectations

- Update `README.md` if user-facing behavior changes.
- Update `CHANGELOG.md` for meaningful changes.
- Keep skill descriptions specific so Cursor can route them well.
- Avoid committing secrets, credentials, or proprietary customer data.

## Testing changes

Before opening a PR:

1. Validate that `.cursor-plugin/plugin.json` is still valid JSON.
2. Confirm new files are in the expected plugin directories.
3. Test the plugin locally in Cursor when possible.
4. Check that prompts and examples still match the current public docs.

## Pull requests

When opening a PR, include:

- the problem being solved
- the PXP product area affected
- any docs pages used as the source of truth
- any known limitations or follow-up work
