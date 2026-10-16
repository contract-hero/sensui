---
status: accepted
---

# `~/.sui/sui_config` is the single source of truth for Networks and Addresses

The app, the `sui` CLI, and the Harness (Claude Code) must agree on the Active Network and Active Address, or a developer switches in the app and the agent still publishes elsewhere. We rejected an app-owned keystore with export-on-demand because it creates two sources of truth. The app reads `client.yaml`, `sui.keystore`, and `sui.aliases` for display only. Every write, including create, import by private key or mnemonic, switch, and env changes, goes through `sui client` and `sui keytool`, so the app never races the CLI on its files.

## Consequences

- Switching Network or Address in the app changes what a running Claude Code session targets on its next command. This is intended.
- The app can only offer what the CLI can do. New CLI capabilities arrive for free; app-only features on keys are out of scope.
