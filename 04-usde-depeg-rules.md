# Ethena USDe Depeg Resolution Rules

## Market Question
**Will Ethena's USDe stablecoin depeg before January 31, 2026, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Depeg
A depeg event occurs when **ALL** of the following conditions are met:

1. **Price Threshold**: USDe trades at a price **outside the range of $0.95 to $1.05** (i.e., greater than 5% deviation from $1.00 peg)
2. **Duration**: The price remains outside this range for a **continuous period of at least 6 hours**
3. **Volume Threshold**: During the depeg period, there is at least **$1,000,000 USD in trading volume** across measured exchanges
4. **Data Source Verification**: The depeg is confirmed by at least **2 out of 12** designated price oracle sources

### Primary Data Sources (Price Oracles)

The following sources shall be used for price determination (if available):

**Aggregators:**
1. **CoinGecko API** - USDe/USD pricing data
2. **CoinMarketCap API** - USDe/USD pricing data

**Decentralized Exchanges:**
3. **Curve Finance** - USDe/USDC, USDe/USDT, and USDe/DAI pool pricing
4. **Uniswap V3** - USDe/USDC and USDe/USDT pool TWAP (Time-Weighted Average Price)
5. **Manifest DEX** - USDe pricing data

**Centralized Exchanges:**
6. **Binance** - USDe/USD pricing data
7. **MEXC** - USDe/USD pricing data
8. **Bullish** - USDe/USD pricing data
9. **Hotcoin** - USDe/USD pricing data
10. **Biconomy** - USDe/USD pricing data
11. **CoinUp** - USDe/USD pricing data

**On-Chain Oracles:**
12. **Chainlink Oracle** - USDe/USD price feed (if available)

### Timing Specification
- **Market Start**: January 4, 2025, 00:00:00 UTC
- **End Time**: Market closes at January 31, 2026, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The 6-hour continuous depeg period must **begin and end** within the market timeframe

## Edge Cases and Special Circumstances

### 1. Flash Crashes and Manipulation
- **Wick events** (price spikes lasting less than 5 minutes on a single exchange) do NOT count as depegs
- If a depeg is caused by a **confirmed exploit, hack, or smart contract vulnerability** affecting USDe or its primary liquidity pools, it SHALL count as a depeg
- If a depeg is caused by **market manipulation** that is later proven and reversed (e.g., exchange rollback), voters should evaluate whether the manipulation was economically significant

### 2. Exchange-Specific Issues
- If a depeg occurs on **only one exchange** due to that exchange's technical issues (e.g., deposit/withdrawal suspension, exchange hack not affecting USDe contract), it does NOT count unless 2+ oracle sources confirm the depeg
- If **multiple major exchanges** (2+) simultaneously show depeg due to their own technical issues (not USDe-related), this does NOT count as a legitimate depeg

### 3. Liquidity Events
- **Low liquidity conditions**: If total USDe liquidity across all major DEXs falls below $10M, price deviations during this period require additional scrutiny
- **Circuit breakers**: If exchanges implement trading halts or circuit breakers, the time during the halt does NOT count toward the 6-hour continuous period

### 4. Smart Contract Events

#### Oracle Failures
- If **ALL price oracles simultaneously fail** or show obviously erroneous data (e.g., $0.00 or $1,000,000.00), voters should use the last known reliable price before failure
- If oracles disagree significantly (>10% variance), use the median value of available oracles

#### USDe Contract Changes
- If Ethena Labs **deploys a new USDe contract** (e.g., USDe v2) and initiates a migration:
  - The old USDe contract price is tracked until migration completes or old token liquidity becomes negligible (<$1M)
  - The new contract is tracked from deployment
  - A depeg in EITHER version counts as a depeg event

#### Upgrades and Pauses
- If the USDe contract is **paused** by admin functions, this is considered a depeg event if it lasts 6+ hours and trading cannot occur
- If the contract is **upgraded** and the upgrade causes price disruption, this counts as a depeg if criteria are met

### 5. Staked USDe (sUSDe) Considerations
- **sUSDe price deviations** do NOT count unless they directly cause USDe to depeg
- If sUSDe/USDe redemption is broken or delayed, evaluate whether this causes USDe itself to depeg based on USDe/USD price

### 6. Collateral and Backing Issues
- If Ethena's **Reserve Fund** is depleted or backing falls below 100%, but USDe maintains its peg on markets, this does NOT count as a depeg
- If **backing concerns** cause a market depeg that meets all criteria, it DOES count

### 7. Regulatory and Legal Events
- If USDe is **delisted** from exchanges due to regulatory action, evaluate remaining exchanges for price
- If Ethena Labs **ceases operations** but USDe contract remains functional, track the market price
- If regulatory action **freezes the smart contract**, this is treated as a depeg event if it lasts 6+ hours

### 8. Network and Infrastructure Issues

#### Ethereum Network Issues
- If Ethereum experiences a **major outage, hardfork, or chain split**, use the chain that Ethena Labs officially recognizes as canonical
- If Ethereum is **unreachable** for 6+ hours preventing USDe transfers, this is NOT automatically a depeg unless price data shows depeg

#### Multi-chain Deployments
- If USDe is **bridged to other chains** (e.g., Arbitrum, Optimism), only the **Ethereum mainnet** USDe price is used for resolution unless >70% of liquidity migrates to another chain

### 9. Market Closure Scenarios
- If **all major exchanges** simultaneously delist or suspend USDe trading, and no price can be determined for 6+ hours, this SHALL be considered a depeg event
- If trading volume falls to **zero** for 6+ hours while price shows depeg, this counts as a depeg

### 10. Data Source Unavailability
- If 2+ primary data sources are **unavailable** at the time of resolution, voters should:
  1. Use historical blockchain data and DEX trades
  2. Reference archived price data from reliable sources
  3. Consult Ethena Labs' official communications
  4. Use good-faith judgment based on available evidence

### 11. Time Zone and Calendar Issues
- All times are in **UTC**
- The deadline of "January 31, 2026, 11:59 PM" means **23:59:59 UTC on January 31, 2026**
- Any depeg event must **start** before this deadline; if it starts at 23:55 UTC and continues into February, it still counts

### 12. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize the **spirit of the market** (did USDe meaningfully lose its peg?)
2. Consider **economic impact** (were users/protocols materially affected?)
3. Evaluate **duration and severity** (was it brief and minor, or prolonged and severe?)
4. Look for **consensus** among Ethena Labs, major exchanges, and DeFi protocols
5. Vote based on **available evidence** and good-faith interpretation

## Resolution Process

### Required Evidence
Voters should provide or verify:
- Screenshots or API data from at least 2 price oracle sources
- Timestamps showing the start and end of the depeg period
- Evidence of trading volume during the period
- Blockchain transaction data if relevant
- Official statements from Ethena Labs (if any)

### Burden of Proof
- The burden of proof for a **"YES"** vote (depeg occurred) requires clear evidence meeting ALL criteria
- In cases of **ambiguity or missing data**, voters should default to **"NO"** (no depeg)

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by February 7, 2026)
- If disputes arise, allow additional time for evidence gathering and discussion

## Definitions

- **USDe**: Ethena's synthetic dollar stablecoin as deployed on Ethereum mainnet at the official contract address (0x4c9EDD5852cd905f086C759E8383e09bff1E68B3)
- **Depeg**: Price deviation beyond the specified threshold for the specified duration with confirmed volume
- **Continuous Period**: An unbroken timeframe; if price returns to peg range even briefly, the timer resets
- **Trading Volume**: Cumulative notional USD value of trades across measured exchanges during the depeg period
- **Major Exchanges**: Exchanges ranked in the top 30 by volume on CoinGecko or CoinMarketCap
- **Price Oracle**: An API or on-chain data source providing reliable USDe/USD pricing information

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. Ethena Labs makes fundamental changes to USDe that require rule updates
3. Technical changes (blockchain upgrades, etc.) require clarification

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** (depeg occurred), confirm:
- USDe price was below $0.95 OR above $1.05
- Price remained outside range for 6+ continuous hours
- At least $1M trading volume during depeg period
- At least 2 out of 12 oracle sources confirm the depeg
- The depeg period began before January 31, 2026, 23:59:59 UTC
- The depeg was not solely due to data errors or single-exchange issues

To vote **NO** (no depeg occurred), confirm:
- No qualifying depeg event occurred during the market period
- Any price deviations were too brief, too small, or lacked sufficient volume
- Available evidence does not meet the required threshold

---

**Last Updated**: January 4, 2025
**Version**: 1.0
