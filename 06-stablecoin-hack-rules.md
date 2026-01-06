# Major Stablecoin Hack Resolution Rules

## Market Question
**Will a major stablecoin get hacked before January 31, 2026, 11:59 PM UTC?**

## Resolution Criteria

### Definition of a Qualifying Hack
A hack event occurs when **ALL** of the following conditions are met:

1. **TVL Threshold**: The stablecoin had at least **$50,000,000 USD in Total Value Locked (TVL)** at any point in the **7 days before** the hack occurred
2. **Team Confirmation**: The stablecoin's **official team/organization** publicly confirms the hack occurred
3. **Independent Verification**: At least **2 out of 6** designated independent sources confirm the hack
4. **Material Loss**: The hack resulted in **at least $1,000,000 USD** in stolen, lost, or compromised funds

### Definition of "Hack"
A "hack" includes any of the following events:

1. **Smart Contract Exploit**: Unauthorized exploitation of a vulnerability in the stablecoin's smart contract code
2. **Private Key Compromise**: Theft or unauthorized access to private keys controlling the stablecoin contract or treasury
3. **Flash Loan Attack**: Manipulation using flash loans that results in unauthorized fund extraction from the protocol
4. **Oracle Manipulation**: Exploitation of price oracle vulnerabilities to drain funds
5. **Governance Attack**: Malicious governance proposal execution that results in unauthorized fund transfers
6. **Bridge Exploit**: Hack of an official bridge operated by the stablecoin team that results in loss of backing or minting of unbacked tokens
7. **Reentrancy Attack**: Exploitation of reentrancy vulnerabilities in the protocol
8. **Admin Key Compromise**: Unauthorized use of admin/owner keys to drain or manipulate funds

### What Does NOT Count as a Hack

1. **Depegs without exploitation**: Price deviations caused by market conditions, not technical exploits
2. **Regulatory seizures**: Government-ordered freezing or confiscation of funds
3. **Rug pulls by the team**: Intentional exit scams by the official team (this is fraud, not a hack)
4. **User wallet hacks**: Individual user wallets being compromised (not the protocol itself)
5. **Third-party protocol hacks**: Hacks of DeFi protocols that use the stablecoin, but not the stablecoin contract itself
6. **Phishing attacks on users**: Social engineering attacks on individual users
7. **Exchange hacks**: Centralized exchange breaches (unless the exchange is the stablecoin issuer)
8. **Frontend attacks**: Website/UI compromises that don't affect the underlying smart contracts

### Qualifying Stablecoins

A "major stablecoin" is any USD-pegged stablecoin that meets the **$50M TVL threshold**. This includes but is not limited to:
- USDT (Tether)
- USDC (Circle)
- DAI (MakerDAO)
- USDe (Ethena)
- FRAX (Frax Finance)
- TUSD (TrueUSD)
- USDP (Paxos)
- pyUSD (PayPal/Paxos)
- LUSD (Liquity)
- sUSD (Synthetix)
- crvUSD (Curve)
- GHO (Aave)
- FDUSD (First Digital)
- Any other USD-pegged stablecoin meeting the TVL threshold

### Primary Verification Sources

**Team Confirmation (Required):**
- Official Twitter/X account of the stablecoin project
- Official blog or website announcement
- Official Discord/Telegram announcement from verified team members
- Official GitHub security advisory

**Independent Sources (2 of 6 required):**
1. **Blockchain Security Firms**: SlowMist, PeckShield, CertiK, BlockSec, Halborn, Trail of Bits, OpenZeppelin
2. **Major Crypto News Outlets**: CoinDesk, The Block, Decrypt, Cointelegraph
3. **On-Chain Analysis Platforms**: Etherscan labels, Chainalysis, Elliptic, Nansen
4. **DeFi Security Dashboards**: DeFiLlama Hacks, Rekt News, Web3 Is Going Great
5. **Major Exchanges**: Official statements from Binance, Coinbase, Kraken confirming the hack
6. **Blockchain Explorers**: Verifiable on-chain evidence of unauthorized transactions

### Timing Specification
- **Market Start**: January 4, 2025, 00:00:00 UTC
- **End Time**: Market closes at January 31, 2026, 23:59:59 UTC
- All timestamps must be recorded in UTC
- The hack must **occur** before the deadline (team confirmation can come after)

## Edge Cases and Special Circumstances

### 1. Timing of Confirmation
- If a hack occurs before the deadline but is only **confirmed after** the deadline, it still counts as long as the hack itself occurred before January 31, 2026, 23:59:59 UTC
- The hack timestamp is determined by the **first malicious transaction** on the blockchain

### 2. TVL Measurement
- TVL is measured using **DeFiLlama** as the primary source
- If DeFiLlama data is unavailable, use **CoinGecko market cap** as a proxy
- The $50M threshold must be met at any point in the **7 days before** the hack
- Historical TVL data from archived sources is acceptable

### 3. Partial Hacks and Recoveries
- If funds are **partially recovered** after a hack, the hack still counts if the initial loss exceeded $1M
- If **all funds are recovered** within 24 hours and no users suffered permanent loss, voters should evaluate whether this constitutes a material hack
- White hat hacks where funds are **returned voluntarily** still count as hacks (the vulnerability was exploited)

### 4. Multiple Hacks
- If **multiple stablecoins** are hacked, the market resolves YES after the first qualifying hack
- If the **same stablecoin** is hacked multiple times, each incident is evaluated independently

### 5. Disputed Hacks
- If the team **denies a hack occurred** but on-chain evidence and 2+ independent sources confirm it, voters should evaluate the evidence
- If the team claims it was a "bug" or "unintended behavior" but funds were lost, it still counts as a hack
- If the team claims a "white hat" scenario but cannot identify the hacker and funds are not returned, it counts as a hack

### 6. Upgradeable Contracts
- If a hack occurs through a **malicious upgrade** pushed by a compromised admin key, this counts as a hack
- If the team uses upgrade functionality to **prevent further losses** during an attack, this does not negate the hack

### 7. Cross-Chain Considerations
- Hacks on **any chain** where the stablecoin operates count (Ethereum, Arbitrum, Optimism, Polygon, Solana, etc.)
- Bridge hacks count only if the bridge is **officially operated** by the stablecoin team
- Third-party bridge hacks do NOT count unless they affect the core stablecoin contract

### 8. Wrapped/Synthetic Versions
- Hacks of **official wrapped versions** (e.g., WETH-style wrappers by the issuer) count
- Hacks of **third-party wrapped versions** do NOT count
- The hack must affect the **official token** or its official derivatives

### 9. Loss Calculation
- Loss is calculated in **USD value at the time of the hack**
- If stolen tokens are later burned or become worthless, the value at hack time is still used
- Include all directly stolen funds plus any funds lost due to the exploit mechanism

### 10. Ambiguous Situations
If a situation arises that is not clearly covered by these rules, voters should:
1. Prioritize **on-chain evidence** over off-chain claims
2. Evaluate whether **unauthorized fund extraction** occurred
3. Consider the **intent** (malicious exploitation vs. accidental bug)
4. Look for **consensus** among security researchers
5. Default to **NO** if evidence is insufficient or contradictory

## Resolution Process

### Required Evidence for YES Vote
Voters must verify:
- Stablecoin had $50M+ TVL in the 7 days before the hack (provide DeFiLlama screenshot or archive)
- Team officially confirmed the hack (provide link to official announcement)
- At least 2 independent sources confirmed the hack (provide links)
- At least $1M was stolen/lost (provide on-chain transaction evidence)
- The hack occurred before January 31, 2026, 23:59:59 UTC (provide block timestamp)

### Burden of Proof
- The burden of proof for a **"YES"** vote requires clear evidence meeting ALL criteria
- In cases of **ambiguity or missing data**, voters should default to **"NO"** (no qualifying hack)

### Resolution Timeline
- Resolution should occur within **14 days** after the market end date (by February 14, 2026)
- If a hack occurs near the deadline, allow additional time for confirmation
- If disputes arise, allow additional time for evidence gathering

## Definitions

- **Hack**: Unauthorized exploitation of a technical vulnerability resulting in loss of funds
- **TVL (Total Value Locked)**: The total USD value of assets held by the stablecoin protocol
- **Team Confirmation**: An official public statement from the stablecoin's governing organization acknowledging the hack
- **Independent Source**: A reputable third-party organization with no financial stake in the outcome
- **Material Loss**: Financial loss of at least $1,000,000 USD
- **Major Stablecoin**: Any USD-pegged stablecoin with $50M+ TVL before the hack

## Amendment Process

These rules may be amended by community consensus if:
1. A critical issue is discovered that makes the market unresolvable
2. New stablecoin designs emerge that require rule clarification
3. Technical changes require clarification

Amendments must be proposed, discussed, and approved before the market close date.

---

## Summary Checklist for Voters

To vote **YES** (hack occurred), confirm:
- A USD-pegged stablecoin had $50M+ TVL in the 7 days before the hack
- The stablecoin team officially confirmed the hack occurred
- At least 2 of 6 independent source categories confirmed the hack
- At least $1M in funds were stolen or lost
- The hack occurred before January 31, 2026, 23:59:59 UTC
- The event meets the definition of a "hack" (not rug pull, regulatory action, etc.)

To vote **NO** (no qualifying hack occurred), confirm:
- No stablecoin meeting the TVL threshold was hacked during the market period
- Any reported incidents did not meet all required criteria
- Available evidence does not meet the required threshold

---

**Last Updated**: January 4, 2025
**Version**: 1.0
