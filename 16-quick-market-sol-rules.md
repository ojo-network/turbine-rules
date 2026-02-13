# SOL 15-Minute Quick Market Resolution Rules

## Market Question Format

**"Will SOL be higher than ${STRIKE_PRICE} at {END_TIME} UTC?"**

Markets are created every 15 minutes. Each market has a fixed strike price and expiration time.

## Resolution Criteria

- **YES** wins if the SOL/USD price is **strictly higher** than the strike price at the market's expiration time (`end_time`).
- **NO** wins if the SOL/USD price is **equal to or lower** than the strike price at expiration.

This is a single point-in-time price check at `end_time`. No TWAP (Time-Weighted Average Price) or averaging is used.

## Price Sources

### Primary Source
**Pyth Network SOL/USD Price Feed**
- Feed ID: SOL/USD on Pyth mainnet
- The price published closest to `end_time` is used

### Fallback Source
**Coinbase API**
- Endpoint: `https://api.coinbase.com/v2/exchange-rates?currency=SOL`
- The USD rate returned at or closest to `end_time` is used

### Source Selection Logic
1. Use Pyth Network SOL/USD price at `end_time`
2. If Pyth is unavailable, retry for up to **60 seconds**
3. If Pyth remains unavailable after 60 seconds, use Coinbase API
4. If both sources are unavailable, delay resolution and use the closest available price within **2 minutes** of `end_time`

## Timing

- Price is fetched at the exact market expiration time (`end_time`)
- Single point-in-time check — no averaging, no lookback window
- All times are in UTC

## Edge Cases

### Price Exactly Equals Strike Price
- **NO wins.** The price must be *strictly higher* than the strike for YES to win.

### Price Source Unavailable at Expiration
- Retry Pyth for up to 60 seconds after `end_time`
- If still unavailable, use Coinbase fallback
- If both unavailable, delay resolution until a price can be fetched; use the closest available price within 2 minutes of `end_time`

### Network Congestion / Delayed Blocks
- Use the price observation closest to `end_time` from the primary source
- If block delay exceeds 2 minutes, fall back to Coinbase

### Exchange Maintenance / Halted Trading
- Use whichever source (Pyth or Coinbase) is available
- If only one source is operational, that source is authoritative

### Flash Crashes / Wicks
- The single point-in-time price is used as-is
- No TWAP smoothing or outlier filtering is applied
- This is by design — markets resolve on the actual price at expiration

## Assertion Parameters

### Liveness Period
**60 seconds**

Quick markets use a shortened liveness period to enable fast resolution. Disputes can still be raised within this window.

### Bond
**$500 USDC**

A single $500 USDC bond is used per resolution and recycled sequentially across assets (see `17-quick-market-sequential-resolution.md` for details).
