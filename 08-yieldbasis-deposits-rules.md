# Yieldbasis $500M Deposits Resolution Rules

## Market Question
**Will Yieldbasis hit $500M in deposits before June 1, 2026, 11:59 PM UTC?**

## Resolution Criteria

### Definition of Success
The market resolves **YES** when **ALL** of the following conditions are met:

1. **Deposit Threshold**: Yieldbasis Total Value Locked (TVL) reaches or exceeds **$500,000,000 USD**
2. **Duration**: The $500M threshold is reached at **any point** before the deadline (does not need to be sustained)
3. **Data Source Verification**: The milestone is confirmed by at least **2 out of 4** designated data sources

### Primary Data Sources

The following sources shall be used for TVL determination (if available):

1. **DeFiLlama** - Yieldbasis TVL data (https://defillama.com/protocol/yieldbasis)
2. **Yieldbasis Official Dashboard** - Protocol's own TVL metrics
3. **On-Chain Data** - Direct smart contract balance queries on applicable chains
4. **CoinGecko** - Protocol TVL data (if available)

### Timing Specification
- **Market Start**: January 6, 2025
- **End Time**: Market closes at June 1, 2026, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The $500M threshold must be reached **at any point** before the deadline

## Edge Cases and Special Circumstances

### 1. TVL Measurement Methodology
- **Deposits** include all assets deposited into Yieldbasis vaults, pools, or staking contracts
- TVL is measured in **USD value** at the time of measurement
- If different sources show different TVL values, use the **median** of available sources
- If only 2 sources are available and they disagree by >10%, investigate the discrepancy before resolution

### 2. Token Price Fluctuations
- If TVL reaches $500M due to **token price appreciation** (not new deposits), it still counts
- If TVL drops below $500M after reaching the threshold, the market still resolves YES (threshold was reached)
- TVL is measured using **real-time USD values** of deposited assets

### 3. Multi-Chain Deployments
- If Yieldbasis operates on **multiple chains**, aggregate TVL across ALL chains
- Include: Ethereum mainnet, Arbitrum, Optimism, Base, Polygon, and any other official deployments
- Only count TVL in **official Yieldbasis contracts** (not third-party integrations)

### 4. Protocol Changes and Migrations
- If Yieldbasis **migrates to new contracts**, include TVL from both old and new contracts during transition
- If Yieldbasis **rebrands** but maintains the same protocol/team, track the rebranded protocol
- If Yieldbasis **merges with another protocol**, evaluate the combined TVL only if Yieldbasis is the surviving brand

### 5. Counting Methodology
- **Include**: Direct deposits, staked assets, LP positions in Yieldbasis pools
- **Exclude**: Borrowed assets, leveraged positions (count only net deposits), rewards/emissions not yet claimed
- **Double-counting**: Ensure assets are not counted multiple times across different pools

### 6. Data Source Unavailability
- If DeFiLlama is unavailable, prioritize **on-chain data** and official dashboard
- If the official dashboard is unavailable, use DeFiLlama and on-chain verification
- If **all sources are unavailable** at resolution time, use the most recent reliable data point within 24 hours

### 7. Smart Contract Issues
- If a **hack or exploit** causes TVL to artificially spike above $500M, this does NOT count
- If TVL reaches $500M and then a hack occurs, the market still resolves YES (threshold was legitimately reached)
- If deposits are **frozen** but still in contracts, they count toward TVL

### 8. Fake or Wash Deposits
- If there is **credible evidence** that deposits were artificially inflated (e.g., team depositing and withdrawing, wash trading), voters should evaluate whether genuine user deposits exceeded $500M
- Incentivized deposits (legitimate yield farming, points programs) DO count
- Self-dealing by the team that is later withdrawn does NOT count

### 9. Protocol Shutdown
- If Yieldbasis **shuts down** before the deadline, the market resolves NO (unless $500M was reached before shutdown)
- If Yieldbasis **pauses deposits** but existing TVL exceeds $500M, the market resolves YES

### 10. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize **on-chain evidence** over off-chain claims
2. Evaluate whether **genuine user deposits** reached the threshold
3. Consider the **spirit of the market** (did Yieldbasis achieve meaningful adoption?)
4. Look for **consensus** among data sources
5. Default to **NO** if evidence is insufficient or contradictory

## Resolution Process

### Required Evidence for YES Vote
Voters must verify:
- Yieldbasis TVL reached $500M+ (provide screenshots from at least 2 data sources)
- Timestamp showing when the threshold was reached (before June 1, 2026, 23:59:59 UTC)
- On-chain verification if possible (contract addresses and balances)

### Required Evidence for NO Vote
Voters must verify:
- Yieldbasis TVL never reached $500M during the market period
- Data from at least 2 sources showing peak TVL was below $500M

### Burden of Proof
- The burden of proof for a **"YES"** vote requires clear evidence from at least 2 data sources
- In cases of **ambiguity or missing data**, voters should default to **"NO"**

### Resolution Timeline
- Resolution should occur within **7 days** after the market end date (by June 8, 2026)
- If disputes arise, allow additional time for evidence gathering

## Definitions

- **Yieldbasis**: The DeFi protocol operating at yieldbasis.com and associated smart contracts
- **TVL (Total Value Locked)**: The total USD value of assets deposited in Yieldbasis smart contracts
- **Deposits**: User funds placed into Yieldbasis vaults, pools, or staking contracts
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
- Yieldbasis TVL reached $500,000,000 USD or higher
- At least 2 of 4 data sources confirm the milestone
- The threshold was reached before June 1, 2026, 23:59:59 UTC
- The TVL was not artificially inflated by exploits or wash deposits

To vote **NO** ($500M not reached), confirm:
- Yieldbasis TVL never reached $500M during the market period
- Available data sources consistently show peak TVL below $500M
- No credible evidence exists that the threshold was reached

---

**Last Updated**: January 6, 2026
**Version**: 1.0
