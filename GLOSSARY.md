# sensui

A macOS desktop companion for building on Sui. It installs the Sui toolchain, runs a Localnet, and manages the networks and addresses a developer targets, alongside an agentic coding harness.

## Language

### Identity

**Address**:
A keypair-backed identity the user signs with, identified by its on-chain address.
_Avoid_: account, wallet, key

**Alias**:
The human-readable label of an Address.
_Avoid_: name, nickname, label

**Active**:
The one Address and the one Network that the CLI and the Harness use for the next command.
_Avoid_: current, selected, default

### Networks

**Network**:
A named RPC endpoint the user targets: local, devnet, testnet, or mainnet.
_Avoid_: env, environment, chain

**Localnet**:
The Network that runs on the user's Mac.
_Avoid_: local network, test validator

**Ephemeral**:
A Localnet state mode where every start begins from a fresh genesis.
_Avoid_: stateless, temporary, throwaway

**Persisted**:
A Localnet state mode where chain state survives a stop and start.
_Avoid_: stateful, saved, durable

### Tools

**Harness**:
An agentic coding tool the developer works in, such as Claude Code.
_Avoid_: agent, assistant, IDE

**Toolchain**:
The set of Sui binaries installed on the Mac and managed by suiup, such as sui and move-analyzer.
_Avoid_: tooling, tools, SDK
