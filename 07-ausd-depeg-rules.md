# Agora AUSD Depeg Resolution Rules

## Market Question
**Will Agora's AUSD stablecoin depeg before January 31, 2026, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Depeg
A depeg event occurs when **ALL** of the following conditions are met:

1. **Price Threshold**: AUSD trades at a price **outside the range of $0.95 to $1.05** (i.e., greater than 5% deviation from $1.00 peg)
2. **Duration**: The price remains outside this range for a **continuous period of at least 6 hours**
3. **Volume Threshold**: During the depeg period, there is at least **$1,000,000 USD in trading volume** across measured exchanges
4. **Data Source Verification**: The depeg is confirmed by at least **2 out of 10** designated price oracle sources

### Primary Data Sources (Price Oracles)

The following sources shall be used for price determination (if available):

**Aggregators:**
1. **CoinGecko API** - AUSD/USD pricing data
2. **CoinMarketCap API** - AUSD/USD pricing data

**Decentralized Exchanges (Avalanche):**
3. **Trader Joe** - AUSD/USDC and AUSD/USDT pool pricing
4. **BENQI** - AUSD pricing data
5. **Pharaoh Exchange** - AUSD pool pricing
6. **Dexalot** - AUSD/USD pricing data
7. **Wombat Exchange** - AUSD pool pricing

**Decentralized Exchanges (Ethereum):**
8. **Uniswap V3** - AUSD/USDC and AUSD/USDT pool TWAP (Time-Weighted Average Price)
9. **Curve Finance** - AUSD/USDC, AUSD/USDT pool pricing (if available)

**On-Chain Oracles:**
10. **Chainlink Oracle** - AUSD/USD price feed (if available)

### Timing Specification
- **Market Start**: January 6, 2025, 00:00:00 UTC
- **End Time**: Market closes at January 31, 2026, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The 6-hour continuous depeg period must **begin and end** within the market timeframe

## Edge Cases and Special Circumstances

### 1. Flash Crashes and Manipulation
- **Wick events** (price spikes lasting less than 5 minutes on a single exchange) do NOT count as depegs
- If a depeg is caused by a **confirmed exploit, hack, or smart contract vulnerability** affecting AUSD or its primary liquidity pools, it SHALL count as a depeg
- If a depeg is caused by **market manipulation** that is later proven and reversed (e.g., exchange rollback), voters should evaluate whether the manipulation was economically significant

### 2. Exchange-Specific Issues
- If a depeg occurs on **only one exchange** due to that exchange's technical issues (e.g., deposit/withdrawal suspension, exchange hack not affecting AUSD contract), it does NOT count unless 2+ oracle sources confirm the depeg
- If **multiple major exchanges** (2+) simultaneously show depeg due to their own technical issues (not AUSD-related), this does NOT count as a legitimate depeg

### 3. Liquidity Events
- **Low liquidity conditions**: If total AUSD liquidity across all major DEXs falls below $5M, price deviations during this period require additional scrutiny
- **Circuit breakers**: If exchanges implement trading halts or circuit breakers, the time during the halt does NOT count toward the 6-hour continuous period

### 4. Smart Contract Events

#### Oracle Failures
- If **ALL price oracles simultaneously fail** or show obviously erroneous data (e.g., $0.00 or $1,000,000.00), voters should use the last known reliable price before failure
- If oracles disagree significantly (>10% variance), use the median value of available oracles

#### AUSD Contract Changes
- If Agora **deploys a new AUSD contract** (e.g., AUSD v2) and initiates a migration:
  - The old AUSD contract price is tracked until migration completes or old token liquidity becomes negligible (<$1M)
  - The new contract is tracked from deployment
  - A depeg in EITHER version counts as a depeg event

#### Upgrades and Pauses
- If the AUSD contract is **paused** by admin functions, this is considered a depeg event if it lasts 6+ hours and trading cannot occur
- If the contract is **upgraded** and the upgrade causes price disruption, this counts as a depeg if criteria are met

### 5. Collateral and Backing Issues
- AUSD is backed by **cash, US Treasury bills, and overnight reverse repurchase agreements** managed by VanEck with custody by State Street
- If AUSD's **backing falls below 100%**, but AUSD maintains its peg on markets, this does NOT count as a depeg
- If **backing concerns** cause a market depeg that meets all criteria, it DOES count
- If reserve management issues arise but price remains stable, this does NOT count as a depeg

### 6. Regulatory and Legal Events
- AUSD does not serve US persons or entities; if **regulatory action** in other jurisdictions causes delistings, evaluate remaining exchanges for price
- If Agora **ceases operations** but the AUSD contract remains functional, track the market price
- If regulatory action **freezes the smart contract**, this is treated as a depeg event if it lasts 6+ hours

### 7. Network and Infrastructure Issues

#### Avalanche Network Issues
- If Avalanche experiences a **major outage, hardfork, or chain split**, use the chain that Agora officially recognizes as canonical
- If Avalanche is **unreachable** for 6+ hours preventing AUSD transfers, this is NOT automatically a depeg unless price data shows depeg

#### Ethereum Network Issues
- If Ethereum experiences a **major outage, hardfork, or chain split**, use the chain that Agora officially recognizes as canonical
- If Ethereum is **unreachable** for 6+ hours preventing AUSD transfers, this is NOT automatically a depeg unless price data shows depeg

#### Multi-chain Deployments
- AUSD is deployed on both **Avalanche** and **Ethereum Mainnet**
- Both chains' pricing data is valid for resolution purposes
- If pricing diverges significantly between chains (>5%), evaluate each chain independently
- A qualifying depeg on EITHER chain counts as a depeg event, provided volume thresholds are met on that chain

### 8. Bridge and Cross-Chain Issues
- If **bridge failures** cause temporary price discrepancies between Avalanche and Ethereum, evaluate whether the discrepancy meets depeg criteria independently on each chain
- Bridge-related arbitrage delays do NOT count as depegs if neither chain shows a qualifying depeg

### 9. Market Closure Scenarios
- If **all major exchanges** simultaneously delist or suspend AUSD trading, and no price can be determined for 6+ hours, this SHALL be considered a depeg event
- If trading volume falls to **zero** for 6+ hours while price shows depeg, this counts as a depeg

### 10. Data Source Unavailability
- If 2+ primary data sources are **unavailable** at the time of resolution, voters should:
  1. Use historical blockchain data and DEX trades
  2. Reference archived price data from reliable sources
  3. Consult Agora's official communications
  4. Use good-faith judgment based on available evidence

### 11. Time Zone and Calendar Issues
- All times are in **UTC**
- The deadline of "January 31, 2026, 11:59 PM" means **23:59:59 UTC on January 31, 2026**
- Any depeg event must **start** before this deadline; if it starts at 23:55 UTC and continues into February, it still counts

### 12. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize the **spirit of the market** (did AUSD meaningfully lose its peg?)
2. Consider **economic impact** (were users/protocols materially affected?)
3. Evaluate **duration and severity** (was it brief and minor, or prolonged and severe?)
4. Look for **consensus** among Agora, major exchanges, and DeFi protocols
5. Vote based on **available evidence** and good-faith interpretation

## Resolution Process

### Required Evidence
Voters should provide or verify:
- Screenshots or API data from at least 2 price oracle sources
- Timestamps showing the start and end of the depeg period
- Evidence of trading volume during the period
- Blockchain transaction data if relevant
- Official statements from Agora (if any)

### Burden of Proof
- The burden of proof for a **"YES"** vote (depeg occurred) requires clear evidence meeting ALL criteria
- In cases of **ambiguity or missing data**, voters should default to **"NO"** (no depeg)

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by February 7, 2026)
- If disputes arise, allow additional time for evidence gathering and discussion

## Definitions

- **AUSD**: Agora's digital dollar stablecoin as deployed on Avalanche and Ethereum mainnet at the official contract addresses
- **Depeg**: Price deviation beyond the specified threshold for the specified duration with confirmed volume
- **Continuous Period**: An unbroken timeframe; if price returns to peg range even briefly, the timer resets
- **Trading Volume**: Cumulative notional USD value of trades across measured exchanges during the depeg period
- **Major Exchanges**: Exchanges ranked in the top 30 by volume on CoinGecko or CoinMarketCap
- **Price Oracle**: An API or on-chain data source providing reliable AUSD/USD pricing information
- **Agora**: Agora Finance, the issuer of AUSD
- **VanEck**: The $100 billion asset management firm managing AUSD reserves
- **State Street**: The custodian providing custody services for AUSD reserves

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. Agora makes fundamental changes to AUSD that require rule updates
3. Technical changes (blockchain upgrades, etc.) require clarification

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** (depeg occurred), confirm:
- AUSD price was below $0.95 OR above $1.05
- Price remained outside range for 6+ continuous hours
- At least $1M trading volume during depeg period
- At least 2 out of 10 oracle sources confirm the depeg
- The depeg period began before January 31, 2026, 23:59:59 UTC
- The depeg was not solely due to data errors or single-exchange issues

To vote **NO** (no depeg occurred), confirm:
- No qualifying depeg event occurred during the market period
- Any price deviations were too brief, too small, or lacked sufficient volume
- Available evidence does not meet the required threshold

---

**Last Updated**: January 6, 2025
**Version**: 1.0
