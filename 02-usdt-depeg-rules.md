# Tether USDT Depeg Resolution Rules

## Market Question
**Will Tether's USDT stablecoin depeg before January 31, 2025, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Depeg
A depeg event occurs when **ALL** of the following conditions are met:

1. **Price Threshold**: USDT trades at a price **outside the range of $0.95 to $1.05** (i.e., greater than 5% deviation from $1.00 peg)
2. **Duration**: The price remains outside this range for a **continuous period of at least 6 hours**
3. **Volume Threshold**: During the depeg period, there is at least **$10,000,000 USD in trading volume** across measured exchanges
4. **Data Source Verification**: The depeg is confirmed by at least **2 out of 12** designated price oracle sources

### Primary Data Sources (Price Oracles)

The following sources shall be used for price determination (if available):

**Aggregators:**
1. **CoinGecko API** - USDT/USD pricing data
2. **CoinMarketCap API** - USDT/USD pricing data

**Decentralized Exchanges:**
3. **Curve Finance** - USDT/USDC, USDT/DAI, and 3pool pricing
4. **Uniswap V3** - USDT/USDC and USDT/ETH pool TWAP (Time-Weighted Average Price)
5. **Manifest DEX** - USDT pricing data

**Centralized Exchanges:**
6. **Binance** - USDT/USD or USDT/BUSD pricing data
7. **MEXC** - USDT/USD pricing data
8. **Bullish** - USDT/USD pricing data
9. **Hotcoin** - USDT/USD pricing data
10. **Biconomy** - USDT/USD pricing data
11. **CoinUp** - USDT/USD pricing data

**On-Chain Oracles:**
12. **Chainlink Oracle** - USDT/USD price feed

### Timing Specification
- **Market Start**: January 4, 2025, 00:00:00 UTC
- **End Time**: Market closes at January 31, 2025, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The 6-hour continuous depeg period must **begin and end** within the market timeframe

## Edge Cases and Special Circumstances

### 1. Flash Crashes and Manipulation
- **Wick events** (price spikes lasting less than 5 minutes on a single exchange) do NOT count as depegs
- If a depeg is caused by a **confirmed exploit, hack, or smart contract vulnerability** affecting USDT or its primary liquidity pools, it SHALL count as a depeg
- If a depeg is caused by **market manipulation** that is later proven and reversed (e.g., exchange rollback), voters should evaluate whether the manipulation was economically significant

### 2. Exchange-Specific Issues
- If a depeg occurs on **only one exchange** due to that exchange's technical issues (e.g., deposit/withdrawal suspension, exchange hack not affecting USDT contract), it does NOT count unless 2+ oracle sources confirm the depeg
- If **multiple major exchanges** (2+) simultaneously show depeg due to their own technical issues (not USDT-related), this does NOT count as a legitimate depeg

### 3. Liquidity Events
- **Low liquidity conditions**: If total USDT liquidity across all major DEXs falls below $100M, price deviations during this period require additional scrutiny
- **Circuit breakers**: If exchanges implement trading halts or circuit breakers, the time during the halt does NOT count toward the 6-hour continuous period

### 4. Smart Contract Events

#### Oracle Failures
- If **ALL price oracles simultaneously fail** or show obviously erroneous data (e.g., $0.00 or $1,000,000.00), voters should use the last known reliable price before failure
- If oracles disagree significantly (>10% variance), use the median value of available oracles

#### USDT Contract Changes
- If Tether **deploys a new USDT contract** (e.g., USDT v2) and initiates a migration:
  - The old USDT contract price is tracked until migration completes or old token liquidity becomes negligible (<$10M)
  - The new contract is tracked from deployment
  - A depeg in EITHER version counts as a depeg event

#### Upgrades and Pauses
- If the USDT contract is **paused** by admin functions, this is considered a depeg event if it lasts 6+ hours and trading cannot occur
- If the contract is **upgraded** and the upgrade causes price disruption, this counts as a depeg if criteria are met

### 5. Multi-Chain Considerations
- USDT exists on **multiple chains** (Ethereum, Tron, Solana, etc.)
- Only **Ethereum mainnet** USDT price is used for resolution unless >70% of total USDT liquidity migrates to another chain
- Cross-chain bridge failures do NOT automatically constitute a depeg unless they cause Ethereum mainnet USDT to depeg

### 6. Collateral and Backing Issues
- If Tether's **reserves** are questioned or found to be below 100% backing, but USDT maintains its peg on markets, this does NOT count as a depeg
- If **backing concerns** cause a market depeg that meets all criteria, it DOES count

### 7. Regulatory and Legal Events
- If USDT is **delisted** from exchanges due to regulatory action, evaluate remaining exchanges for price
- If Tether Limited **ceases operations** but USDT contract remains functional, track the market price
- If regulatory action **freezes the smart contract**, this is treated as a depeg event if it lasts 6+ hours
- If Tether **blacklists addresses** or freezes funds, this does NOT constitute a depeg unless it causes market price to depeg

### 8. Network and Infrastructure Issues

#### Ethereum Network Issues
- If Ethereum experiences a **major outage, hardfork, or chain split**, use the chain that Tether officially recognizes as canonical
- If Ethereum is **unreachable** for 6+ hours preventing USDT transfers, this is NOT automatically a depeg unless price data shows depeg

#### Cross-Chain Issues
- If bridges between chains fail, evaluate **Ethereum mainnet** price only
- If Tron or other major USDT chains experience issues, this does NOT affect resolution unless Ethereum mainnet USDT depegs

### 9. Market Closure Scenarios
- If **all major exchanges** simultaneously delist or suspend USDT trading, and no price can be determined for 6+ hours, this SHALL be considered a depeg event
- If trading volume falls to **zero** for 6+ hours while price shows depeg, this counts as a depeg

### 10. Data Source Unavailability
- If 2+ primary data sources are **unavailable** at the time of resolution, voters should:
  1. Use historical blockchain data and DEX trades
  2. Reference archived price data from reliable sources
  3. Consult Tether's official communications
  4. Use good-faith judgment based on available evidence

### 11. Time Zone and Calendar Issues
- All times are in **UTC**
- The deadline of "January 31, 2025, 11:59 PM" means **23:59:59 UTC on January 31, 2025**
- Any depeg event must **start** before this deadline; if it starts at 23:55 UTC and continues into February, it still counts

### 12. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize the **spirit of the market** (did USDT meaningfully lose its peg?)
2. Consider **economic impact** (were users/protocols materially affected?)
3. Evaluate **duration and severity** (was it brief and minor, or prolonged and severe?)
4. Look for **consensus** among Tether, major exchanges, and DeFi protocols
5. Vote based on **available evidence** and good-faith interpretation

## Resolution Process

### Required Evidence
Voters should provide or verify:
- Screenshots or API data from at least 3 price oracle sources
- Timestamps showing the start and end of the depeg period
- Evidence of trading volume during the period
- Blockchain transaction data if relevant
- Official statements from Tether (if any)

### Burden of Proof
- The burden of proof for a **"YES"** vote (depeg occurred) requires clear evidence meeting ALL criteria
- In cases of **ambiguity or missing data**, voters should default to **"NO"** (no depeg)

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by February 7, 2025)
- If disputes arise, allow additional time for evidence gathering and discussion

## Definitions

- **USDT**: Tether's USD-pegged stablecoin as deployed on Ethereum mainnet at the official contract address (0xdAC17F958D2ee523a2206206994597C13D831ec7)
- **Depeg**: Price deviation beyond the specified threshold for the specified duration with confirmed volume
- **Continuous Period**: An unbroken timeframe; if price returns to peg range even briefly, the timer resets
- **Trading Volume**: Cumulative notional USD value of trades across measured exchanges during the depeg period
- **Major Exchanges**: Exchanges ranked in the top 30 by volume on CoinGecko or CoinMarketCap
- **Price Oracle**: An API or on-chain data source providing reliable USDT/USD pricing information

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. Tether makes fundamental changes to USDT that require rule updates
3. Technical changes (blockchain upgrades, etc.) require clarification

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** (depeg occurred), confirm:
- [ ] USDT price was below $0.95 OR above $1.05
- [ ] Price remained outside range for 6+ continuous hours
- [ ] At least $10M trading volume during depeg period
- [ ] At least 2 out of 12 oracle sources confirm the depeg
- [ ] The depeg period began before January 31, 2025, 23:59:59 UTC
- [ ] The depeg was not solely due to data errors or single-exchange issues

To vote **NO** (no depeg occurred), confirm:
- [ ] No qualifying depeg event occurred during the market period
- [ ] Any price deviations were too brief, too small, or lacked sufficient volume
- [ ] Available evidence does not meet the required threshold

---

**Last Updated**: January 4, 2025
**Version**: 1.0
