---
status: accepted
---

# Localnet runs in containers via colima and docker compose, not native `sui start`

The documented default for a local network is a native `sui start --force-regenesis --with-faucet`, which needs no runtime. We run the Localnet in containers anyway: it isolates the Localnet from the host install, pins the exact release, gives Postgres for the indexer and GraphQL RPC without a host Postgres, and leaves room for several Localnets after the hackathon. The runtime is colima (Docker-socket compatible, free, installed via Homebrew), driven through a compose file the app writes and runs with `docker compose`.

## Considered options

- Native `sui start`: simplest, no isolation, needs host Postgres for indexer/GraphQL.
- Apple `container` (macOS 26): native, but young, arm64 only, no compose, would raise the deployment target.
- Docker Desktop: common, but licensed for larger companies and a heavy install.
- Docker Engine REST API from Swift: no CLI dependency, but needs swift-nio and hand-written multi-container wiring.

## Rules that follow

- Containers: official `mysten/sui-tools` plus a `postgres:16` sidecar. No custom image.
- The image tag is pinned to the host sui channel and release: `mysten/sui-tools:<channel>-v<version>-arm64` on Apple Silicon, the bare `<channel>-v<version>` tag on Intel (the bare tag is amd64 only; for example `testnet-v1.81.0-arm64`). When the host sui updates, a Persisted Localnet must be Reset before the new image starts.
- One Localnet at a time on fixed ports 9000 (RPC), 9123 (faucet), 9125 (GraphQL). If 9000 is bound, Start refuses and names the holder.

## Known risk

`sui start --with-indexer=<postgres url> --with-graphql` against a sidecar Postgres inside the official image is inferred from source, not tested. This is the first spike.
