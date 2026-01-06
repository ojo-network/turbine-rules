# Yieldbasis Bitcoin Pool $500M Deposits Resolution Rules

## Market Question
**Will Yieldbasis Bitcoin pools hit $500M in deposits before June 1, 2026, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Success
The market resolves **YES** when **ALL** of the following conditions are met:

1. **Deposit Threshold**: Yieldbasis Bitcoin pool deposits reach or exceed **$500,000,000 USD**
2. **Duration**: The $500M threshold is reached at **any point** before the deadline (does not need to be sustained)
3. **Data Source Verification**: The milestone is confirmed by at least **2 out of 4** designated data sources

### What Counts as Bitcoin Pool Deposits

Only deposits in **Bitcoin-related pools** count toward the $500M threshold:
- **BTC**: Native Bitcoin bridged to supported chains
- **WBTC**: Wrapped Bitcoin
- **cbBTC**: Coinbase Wrapped Bitcoin
- **tBTC**: Threshold Network Bitcoin
- **sBTC**: Any synthetic Bitcoin variants officially supported by Yieldbasis
- **Other BTC derivatives**: Any other Bitcoin-pegged assets in official Yieldbasis Bitcoin pools

**Excluded from count:**
- ETH, stablecoins, altcoins, or any non-Bitcoin assets
- Bitcoin held in non-Yieldbasis protocols
- LP tokens that are not Bitcoin-denominated

### Primary Data Sources

The following sources shall be used for Bitcoin pool deposit determination (if available):

1. **DeFiLlama** - Yieldbasis Bitcoin pool TVL data (https://defillama.com/protocol/yieldbasis)
2. **Yieldbasis Official Dashboard** - Protocol's own Bitcoin pool metrics
3. **On-Chain Data** - Direct smart contract balance queries for Bitcoin pool contracts
4. **CoinGecko** - Protocol Bitcoin pool TVL data (if available)

### Timing Specification
- **Market Start**: January 6, 2026
- **End Time**: Market closes at June 1, 2026, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The $500M threshold must be reached **at any point** before the deadline

## Edge Cases and Special Circumstances

### 1. Deposit Measurement Methodology
- **Deposits** include all Bitcoin assets deposited into Yieldbasis Bitcoin vaults, pools, or staking contracts
- Deposits are measured in **USD value** at the time of measurement
- If different sources show different deposit values, use the **median** of available sources
- If only 2 sources are available and they disagree by >10%, investigate the discrepancy before resolution

### 2. Bitcoin Price Fluctuations
- If deposits reach $500M due to **Bitcoin price appreciation** (not new deposits), it still counts
- If deposits drop below $500M after reaching the threshold, the market still resolves YES (threshold was reached)
- Deposits are measured using **real-time USD values** of deposited Bitcoin assets

### 3. Multi-Chain Deployments
- If Yieldbasis Bitcoin pools operate on **multiple chains**, aggregate deposits across ALL chains
- Include: Ethereum mainnet, Arbitrum, Optimism, Base, Polygon, and any other official deployments
- Only count deposits in **official Yieldbasis Bitcoin pool contracts** (not third-party integrations)

### 4. Protocol Changes and Migrations
- If Yieldbasis **migrates Bitcoin pools to new contracts**, include deposits from both old and new contracts during transition
- If Yieldbasis **rebrands** but maintains the same protocol/team, track the rebranded protocol's Bitcoin pools
- If Yieldbasis **merges with another protocol**, evaluate the combined Bitcoin pool deposits only if Yieldbasis is the surviving brand

### 5. Counting Methodology
- **Include**: Direct Bitcoin deposits, staked Bitcoin assets, Bitcoin LP positions in Yieldbasis pools
- **Exclude**: Borrowed Bitcoin, leveraged positions (count only net deposits), rewards/emissions not yet claimed
- **Double-counting**: Ensure Bitcoin assets are not counted multiple times across different pools

### 6. New Bitcoin Derivatives
- If Yieldbasis adds support for **new Bitcoin-pegged assets** after market creation, those deposits count
- The asset must be a legitimate Bitcoin derivative (1:1 or near-1:1 backed by BTC)
- Algorithmic or under-collateralized "Bitcoin" tokens do NOT count

### 7. Data Source Unavailability
- If DeFiLlama is unavailable, prioritize **on-chain data** and official dashboard
- If the official dashboard is unavailable, use DeFiLlama and on-chain verification
- If **all sources are unavailable** at resolution time, use the most recent reliable data point within 24 hours

### 8. Smart Contract Issues
- If a **hack or exploit** causes Bitcoin pool deposits to artificially spike above $500M, this does NOT count
- If deposits reach $500M and then a hack occurs, the market still resolves YES (threshold was legitimately reached)
- If deposits are **frozen** but still in contracts, they count toward the threshold

### 9. Fake or Wash Deposits
- If there is **credible evidence** that deposits were artificially inflated (e.g., team depositing and withdrawing, wash trading), voters should evaluate whether genuine user deposits exceeded $500M
- Incentivized deposits (legitimate yield farming, points programs) DO count
- Self-dealing by the team that is later withdrawn does NOT count

### 10. Protocol Shutdown
- If Yieldbasis **shuts down** before the deadline, the market resolves NO (unless $500M was reached before shutdown)
- If Yieldbasis **pauses Bitcoin pool deposits** but existing deposits exceed $500M, the market resolves YES

### 11. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize **on-chain evidence** over off-chain claims
2. Evaluate whether **genuine user Bitcoin deposits** reached the threshold
3. Consider the **spirit of the market** (did Yieldbasis Bitcoin pools achieve meaningful adoption?)
4. Look for **consensus** among data sources
5. Default to **NO** if evidence is insufficient or contradictory

## Resolution Process

### Required Evidence for YES Vote
Voters must verify:
- Yieldbasis Bitcoin pool deposits reached $500M+ (provide screenshots from at least 2 data sources)
- Timestamp showing when the threshold was reached (before June 1, 2026, 23:59:59 UTC)
- On-chain verification if possible (Bitcoin pool contract addresses and balances)

### Required Evidence for NO Vote
Voters must verify:
- Yieldbasis Bitcoin pool deposits never reached $500M during the market period
- Data from at least 2 sources showing peak Bitcoin pool deposits were below $500M

### Burden of Proof
- The burden of proof for a **"YES"** vote requires clear evidence from at least 2 data sources
- In cases of **ambiguity or missing data**, voters should default to **"NO"**

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by June 8, 2026)
- If disputes arise, allow additional time for evidence gathering

## Definitions

- **Yieldbasis**: The DeFi protocol operating at yieldbasis.com and associated smart contracts
- **Bitcoin Pool Deposits**: The total USD value of Bitcoin and Bitcoin-derivative assets deposited in Yieldbasis Bitcoin pool smart contracts
- **Bitcoin Derivatives**: Assets pegged to or backed by Bitcoin (WBTC, cbBTC, tBTC, etc.)
- **Data Source**: A reputable platform providing TVL tracking for DeFi protocols

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. Yieldbasis makes fundamental changes that require rule updates
3. Data source availability changes significantly

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** ($500M reached), confirm:
- Yieldbasis Bitcoin pool deposits reached $500,000,000 USD or higher
- At least 2 of 4 data sources confirm the milestone
- The threshold was reached before June 1, 2026, 23:59:59 UTC
- The deposits were not artificially inflated by exploits or wash deposits

To vote **NO** ($500M not reached), confirm:
- Yieldbasis Bitcoin pool deposits never reached $500M during the market period
- Available data sources consistently show peak Bitcoin pool deposits below $500M
- No credible evidence exists that the threshold was reached

---

**Last Updated**: January 6, 2026
**Version**: 1.0
