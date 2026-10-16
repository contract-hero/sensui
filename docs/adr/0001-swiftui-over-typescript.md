---
status: accepted
---

# SwiftUI for the desktop app instead of a TypeScript shell

sensui is a macOS-only companion whose pitch is the most pleasant native experience for Sui developers. The team's default stack is TypeScript, and Tauri 2 or Electron would have kept it, but both wrap a WebView and neither feels native on macOS. We chose SwiftUI with a macOS 15 deployment target, App Sandbox off, and no App Store distribution for the hackathon PoC.

## Consequences

- Container orchestration shells out to `docker compose` through `Process`, because Swift has no mature Docker SDK (see ADR-0002).
- All Sui operations shell out to the suiup-managed `sui` binary; the app has no in-process Sui SDK.
