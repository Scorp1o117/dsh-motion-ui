# DSH 0.2.1-rc.3 compatibility

Compared the complete official `dsh-v0.2.1-rc.2...dsh-v0.2.1-rc.3` source diff on 2026-10-24.

## Runtime changes

The release rebuilds navigation entry customization on region-owned pins and More menus: each navigation region (left sidebar, Conversation header, right sidebar guide) draws its own More button and menu around its actions slot, with shared rows (entries with pin buttons, Browse other plugins, Create your plugin) registered by `ui-entry-customization`. `ctx.layout.entryVisibility`, the plugin store, left-sidebar drag reordering, and `agentPresetNavigation` are removed; `ui-layout` and `ui-agent-preset` match release/dsh-0.2.1 again. New Session takes the blank-reuse path again, so an unsent draft survives session switches, and `DraftInitializationOptions` gains `whenDraftExists` (`replace` | `append` | `keep`). The DeepSeek API-key route now follows the official `/models` listing.

Motion UI does not use `ctx.layout.entryVisibility`, `agentPresetNavigation`, or the draft initialization options. The More menus live in the sidebar and conversation header slots outside the conversation document surface; the skin grammar continues to protect native component geometry generically, and the previously protected surfaces are untouched.

No changes were found in the Host tool registration APIs, Motion UI conversation/sidebar slots, or Desktop media forwarding. The existing authenticated Blob source for native Desktop playback remains necessary. Browser HTTP media playback remains direct.

## Adaptation

- Include DSH 0.2.1-rc.3 explicitly in compatibility and SDK peer ranges, retaining the previously supported releases.
- Pin development SDKs and resolve a clean dependency cohort against rc.3.
- Rebuild the client without changing tool contracts, rendering behavior, user settings, or model limits.

## Validation

- Full unit/integration test suite passed against the rebuilt package with development SDKs on rc.3.
- Packed package installed with the official DSH 0.2.1-rc.3 CLI into an isolated Web profile built from the shipped web template; configuration composition, service startup and authenticated HTTP 200 passed.
- Web profile boots with the plugin registered and no "did not activate" warnings.

Official release: https://github.com/deepseek-ai/deepseek-harness/releases/tag/dsh-v0.2.1-rc.3
