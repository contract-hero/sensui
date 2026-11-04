# sensui

A native macOS companion for building on Sui. sensui takes care of the setup and the day-to-day workspace, so a Sui developer can spend the first hour on code instead of on install guides. It stays out of the way of the agentic coding Harness (such as Claude Code) that writes the code.

> **Status:** proof of concept for an internal hackathon. Implementation starts from spec [#1](https://github.com/contract-hero/sensui/issues/1). Most features below are planned, not built yet.

## What it does

- **Toolchain:** checks which prerequisites are missing (Xcode Command Line Tools, Homebrew, colima, docker CLI, suiup, sui, move-analyzer) and installs only those. It keeps `sui` and `move-analyzer` at the same version, and it shows updates and a health check.
- **Localnet:** starts a local Sui network in containers with one click. The network has a faucet, an indexer and GraphQL RPC, and it runs the same release as your host CLI. You can pick an Ephemeral (fresh genesis on each start) or a Persisted (state survives a restart) Localnet.
- **Networks and Addresses:** shows and switches the Active Network and the Active Address. It creates and imports Addresses, shows balances, and funds an Address on Localnet and devnet.
- **Harness:** installs [sui-pilot](https://github.com/contract-hero) into Claude Code. The Network and the Address you pick in sensui are the ones that Claude uses on its next command.

Every action is a visible CLI command that you could run yourself. sensui keeps no keys or networks of its own: `~/.sui/sui_config` is the single source of truth.

## Stack

- SwiftUI, macOS 15 or newer ([ADR-0001](docs/adr/0001-swiftui-over-typescript.md))
- Localnet through colima and `docker compose` ([ADR-0002](docs/adr/0002-localnet-in-containers-via-colima-and-compose.md))
- The sui CLI config as the source of truth ([ADR-0003](docs/adr/0003-sui-cli-config-as-single-source-of-truth.md))

## Docs

- [GLOSSARY.md](GLOSSARY.md): the project vocabulary (Address, Active, Localnet, Harness, Toolchain, and more)
- [docs/adr/](docs/adr/): architecture decisions
- [Issues](https://github.com/contract-hero/sensui/issues): the spec and its tickets
