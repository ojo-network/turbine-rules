# Quick Market Sequential Resolution Process

## Overview

When multiple assets (BTC, ETH, SOL) have expired 15-minute quick markets, they are resolved **one at a time** using a single recycled bond. This document describes the sequential resolution lifecycle.

## Resolution Order

**BTC → ETH → SOL**

This order is the default and is configurable. Assets are processed in sequence — the next asset's resolution does not begin until the previous one has fully settled and the bond has been returned.

## Resolution Lifecycle (Per Asset)

Each asset resolution follows this cycle:

1. **Propose** — Submit the resolution assertion (YES or NO) to the UMA Optimistic Oracle with the $500 USDC bond
2. **Liveness (60 seconds)** — The assertion is open for dispute during the liveness window
3. **Settle** — If undisputed, the assertion is settled on-chain
4. **Bond returned** — The $500 USDC bond is returned to the proposer
5. **Next asset** — Proceed to the next asset in the queue

### Timing Example

If BTC, ETH, and SOL all expire at 14:00 UTC:

| Step | Time | Action |
|------|------|--------|
| 1 | 14:00 | Propose BTC resolution (bond locked) |
| 2 | 14:01 | BTC liveness expires, settle, bond returned |
| 3 | 14:01 | Propose ETH resolution (bond locked) |
| 4 | 14:02 | ETH liveness expires, settle, bond returned |
| 5 | 14:02 | Propose SOL resolution (bond locked) |
| 6 | 14:03 | SOL liveness expires, settle, bond returned |

All three assets resolve within ~3 minutes of expiration.

## Bond Management

- **Single bond**: One $500 USDC bond is used across all assets
- **Recycled sequentially**: The bond is returned after each settlement and reused for the next asset
- **No parallel resolution**: Only one assertion is active at a time to avoid requiring multiple bonds

## Failure Handling

### Single Resolution Failure
- If a resolution for one asset fails (e.g., transaction reverts, price source issue), **skip to the next asset**
- The failed asset is retried on the next resolution cycle
- Remaining assets in the queue are not blocked by the failure

### Disputed Assertion
- If an assertion is disputed during the 60-second liveness period, the bond is locked in the dispute process
- Resolution for remaining assets is **paused** until the dispute is resolved and the bond is recovered, OR a secondary bond is deployed
- Disputed markets resolve through UMA's standard DVM (Data Verification Mechanism) process

### Settlement Loop (Fallback)
- A background settlement loop runs continuously to catch any missed settlements
- If a market was proposed but not settled (e.g., due to gas issues or bot downtime), the settlement loop will settle it
- The loop checks for unsettled assertions and submits settlement transactions
- This ensures no market is left in a proposed-but-unsettled state

## Configuration

| Parameter | Value | Notes |
|-----------|-------|-------|
| Resolution order | BTC → ETH → SOL | Configurable |
| Liveness period | 60 seconds | Per assertion |
| Bond amount | $500 USDC | Single recycled bond |
| Max retry delay | Next 15-min cycle | Failed assets retry next cycle |
| Settlement loop interval | Continuous | Catches missed settlements |
