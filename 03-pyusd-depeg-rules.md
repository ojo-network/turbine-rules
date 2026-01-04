# PayPal pyUSD Depeg Resolution Rules

## Market Question
**Will PayPal's pyUSD stablecoin depeg before January 31, 2025, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Depeg
A depeg event occurs when **ALL** of the following conditions are met:

1. **Price Threshold**: pyUSD trades at a price **outside the range of $0.95 to $1.05** (i.e., greater than 5% deviation from $1.00 peg)
2. **Duration**: The price remains outside this range for a **continuous period of at least 6 hours**
3. **Volume Threshold**: During the depeg period, there is at least **$1,000,000 USD in trading volume** across measured exchanges
4. **Data Source Verification**: The depeg is confirmed by at least **2 out of 12** designated price oracle sources

### Primary Data Sources (Price Oracles)

The following sources shall be used for price determination (if available):

**Aggregators:**
1. **CoinGecko API** - pyUSD/USD pricing data
2. **CoinMarketCap API** - pyUSD/USD pricing data

**Decentralized Exchanges:**
3. **Curve Finance** - pyUSD pools (pyUSD/USDC, pyUSD/FRAX, etc.)
4. **Uniswap V3** - pyUSD/USDC and pyUSD/USDT pool TWAP (Time-Weighted Average Price)
5. **Manifest DEX** - pyUSD pricing data

**Centralized Exchanges:**
6. **Binance** - pyUSD/USD pricing data
7. **MEXC** - pyUSD/USD pricing data
8. **Bullish** - pyUSD/USD pricing data
9. **Hotcoin** - pyUSD/USD pricing data
10. **Biconomy** - pyUSD/USD pricing data
11. **CoinUp** - pyUSD/USD pricing data

**On-Chain Oracles:**
12. **Chainlink Oracle** - pyUSD/USD price feed (if available)

### Timing Specification
- **Market Start**: January 4, 2025, 00:00:00 UTC
- **End Time**: Market closes at January 31, 2025, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The 6-hour continuous depeg period must **begin and end** within the market timeframe

## Edge Cases and Special Circumstances

### 1. Flash Crashes and Manipulation
- **Wick events** (price spikes lasting less than 5 minutes on a single exchange) do NOT count as depegs
- If a depeg is caused by a **confirmed exploit, hack, or smart contract vulnerability** affecting pyUSD or its primary liquidity pools, it SHALL count as a depeg
- If a depeg is caused by **market manipulation** that is later proven and reversed (e.g., exchange rollback), voters should evaluate whether the manipulation was economically significant

### 2. Exchange-Specific Issues
- If a depeg occurs on **only one exchange** due to that exchange's technical issues (e.g., deposit/withdrawal suspension, exchange hack not affecting pyUSD contract), it does NOT count unless 2+ oracle sources confirm the depeg
- If **multiple major exchanges** (2+) simultaneously show depeg due to their own technical issues (not pyUSD-related), this does NOT count as a legitimate depeg

### 3. Liquidity Events
- **Low liquidity conditions**: If total pyUSD liquidity across all major DEXs falls below $5M, price deviations during this period require additional scrutiny
- **Circuit breakers**: If exchanges implement trading halts or circuit breakers, the time during the halt does NOT count toward the 6-hour continuous period

### 4. Smart Contract Events

#### Oracle Failures
- If **ALL price oracles simultaneously fail** or show obviously erroneous data (e.g., $0.00 or $1,000,000.00), voters should use the last known reliable price before failure
- If oracles disagree significantly (>10% variance), use the median value of available oracles

#### pyUSD Contract Changes
- If Paxos (pyUSD issuer) **deploys a new pyUSD contract** and initiates a migration:
  - The old pyUSD contract price is tracked until migration completes or old token liquidity becomes negligible (<$1M)
  - The new contract is tracked from deployment
  - A depeg in EITHER version counts as a depeg event

#### Upgrades and Pauses
- If the pyUSD contract is **paused** by admin functions, this is considered a depeg event if it lasts 6+ hours and trading cannot occur
- If the contract is **upgraded** and the upgrade causes price disruption, this counts as a depeg if criteria are met

### 5. Multi-Chain Considerations
- pyUSD exists on **Ethereum and Solana**
- Only **Ethereum mainnet** pyUSD price is used for resolution unless >70% of total pyUSD liquidity migrates to Solana
- Cross-chain bridge failures do NOT automatically constitute a depeg unless they cause Ethereum mainnet pyUSD to depeg

### 6. Collateral and Backing Issues
- pyUSD is backed by **USD deposits, U.S. Treasuries, and cash equivalents** held by Paxos
- If Paxos's **reserves** are questioned or found to be below 100% backing, but pyUSD maintains its peg on markets, this does NOT count as a depeg
- If **backing concerns** cause a market depeg that meets all criteria, it DOES count

### 7. Regulatory and Legal Events
- If pyUSD is **delisted** from exchanges due to regulatory action, evaluate remaining exchanges for price
- If Paxos or PayPal **ceases pyUSD operations** but the contract remains functional, track the market price
- If regulatory action **freezes the smart contract**, this is treated as a depeg event if it lasts 6+ hours
- If Paxos **blacklists addresses** or freezes funds (as permitted by the contract), this does NOT constitute a depeg unless it causes market price to depeg

### 8. Network and Infrastructure Issues

#### Ethereum Network Issues
- If Ethereum experiences a **major outage, hardfork, or chain split**, use the chain that Paxos officially recognizes as canonical
- If Ethereum is **unreachable** for 6+ hours preventing pyUSD transfers, this is NOT automatically a depeg unless price data shows depeg

#### Solana Network Issues
- If Solana experiences issues affecting pyUSD on that chain, this does NOT affect resolution unless Ethereum mainnet pyUSD depegs
- If Solana pyUSD bridges fail, evaluate **Ethereum mainnet** price only

### 9. PayPal Platform Issues
- If **PayPal's platform** experiences outages affecting pyUSD purchases/redemptions within the PayPal app, this does NOT constitute a depeg unless on-chain market prices show depeg
- If PayPal **suspends pyUSD services** but on-chain trading continues at peg, this is NOT a depeg

### 10. Market Closure Scenarios
- If **all major exchanges** simultaneously delist or suspend pyUSD trading, and no price can be determined for 6+ hours, this SHALL be considered a depeg event
- If trading volume falls to **zero** for 6+ hours while price shows depeg, this counts as a depeg

### 11. Data Source Unavailability
- If 2+ primary data sources are **unavailable** at the time of resolution, voters should:
  1. Use historical blockchain data and DEX trades
  2. Reference archived price data from reliable sources
  3. Consult Paxos's and PayPal's official communications
  4. Use good-faith judgment based on available evidence

### 12. Time Zone and Calendar Issues
- All times are in **UTC**
- The deadline of "January 31, 2025, 11:59 PM" means **23:59:59 UTC on January 31, 2025**
- Any depeg event must **start** before this deadline; if it starts at 23:55 UTC and continues into February, it still counts

### 13. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize the **spirit of the market** (did pyUSD meaningfully lose its peg?)
2. Consider **economic impact** (were users/protocols materially affected?)
3. Evaluate **duration and severity** (was it brief and minor, or prolonged and severe?)
4. Look for **consensus** among Paxos, PayPal, major exchanges, and DeFi protocols
5. Vote based on **available evidence** and good-faith interpretation

## Resolution Process

### Required Evidence
Voters should provide or verify:
- Screenshots or API data from at least 3 price oracle sources
- Timestamps showing the start and end of the depeg period
- Evidence of trading volume during the period
- Blockchain transaction data if relevant
- Official statements from Paxos or PayPal (if any)

### Burden of Proof
- The burden of proof for a **"YES"** vote (depeg occurred) requires clear evidence meeting ALL criteria
- In cases of **ambiguity or missing data**, voters should default to **"NO"** (no depeg)

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by February 7, 2025)
- If disputes arise, allow additional time for evidence gathering and discussion

## Definitions

- **pyUSD**: PayPal USD stablecoin issued by Paxos Trust Company, deployed on Ethereum mainnet at the official contract address (0x6c3ea9036406852006290770BEdFcAbA0e23A0e8)
- **Depeg**: Price deviation beyond the specified threshold for the specified duration with confirmed volume
- **Continuous Period**: An unbroken timeframe; if price returns to peg range even briefly, the timer resets
- **Trading Volume**: Cumulative notional USD value of trades across measured exchanges during the depeg period
- **Major Exchanges**: Exchanges ranked in the top 30 by volume on CoinGecko or CoinMarketCap
- **Price Oracle**: An API or on-chain data source providing reliable pyUSD/USD pricing information
- **Paxos**: Paxos Trust Company, the regulated issuer of pyUSD

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. Paxos or PayPal makes fundamental changes to pyUSD that require rule updates
3. Technical changes (blockchain upgrades, etc.) require clarification

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** (depeg occurred), confirm:
- [ ] pyUSD price was below $0.95 OR above $1.05
- [ ] Price remained outside range for 6+ continuous hours
- [ ] At least $1M trading volume during depeg period
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
