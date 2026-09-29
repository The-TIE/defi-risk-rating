# Morpho - Steakhouse Prime Instant V2 USDC Vault Risk Rating

**Rating Date**: 2026-04-07
**Final Grade**: BB-
**Total Score**: 754.1/900 points
**Product Type**: Vault
**Chain**: Ethereum
**Framework**: Staking Rewards DeFi Protocol Rating Framework v0.1-gamma

---

## Detailed Analysis

### SECURITY (40% Weight) -- Score: 293.2/360 (81.4%)

#### Smart Contract Security (20% weight, 180 max points)

**NOTE: V2-specific audit coverage. The VaultV2 contract is immutable (non-upgradeable, verified on Etherscan, compiler v0.8.28). It was audited by 9+ engagements (ChainSecurity, Spearbit x3, Blackthorn x2, Certora, Zellic, Cantina competition). The broader Morpho ecosystem has 25+ audit engagements (3 dedicated to the Morpho Blue core: OpenZeppelin, Spearbit, Cantina competition), which is immutable (~600 LOC). Platform-level scores (S-SC-06/07/08/09/10/11) are consistent with all other Morpho vault ratings.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-SC-01 | Have all core contracts that hold or route funds been independently audited? | Yes. The VaultV2 contract has 9+ audit engagements: ChainSecurity (Sep 2025), Spearbit (May, Nov, Dec 2025), Blackthorn (Sep, Dec 2025), Certora (Dec 2025), Zellic (Jul 2025), Cantina competition (Jul 2025). All are Tier-0/Tier-1 firms. The broader Morpho ecosystem has 25+ audit engagements, with 3 dedicated to the Morpho Blue core (OpenZeppelin, Spearbit, Cantina competition). Formal verification by Certora covers V2 contracts. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/get-started/resources/audits/), [P1] [ChainSecurity V2 Audit](https://www.chainsecurity.com/security-audit/morpho-vault-v2), [P1] [Sherlock/Blackthorn Case Study](https://sherlock.xyz/case-studies/morpho) |
| S-SC-02 | Who performed the most recent audit and what is their reputation tier? | December 2025: Certora (Tier-0), Spearbit (Tier-0 via Cantina), Blackthorn for Vaults V2 MarketV1AdapterV2. September 2025: ChainSecurity (Tier-0) for Vaults V2 core. Multiple Tier-0 auditors for most recent work. | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Reviews](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-03 | Have upgrades to core contracts been followed by new audits? | Yes. VaultV2 contract is immutable (non-upgradeable, confirmed via Etherscan). Morpho Blue core is immutable (~600 LOC). Every V2 component deployed in 2025 was preceded by multiple Tier-0 audits. No upgrades possible on this vault contract. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan VaultV2](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51#code), [P1] [Security Reviews](https://docs.morpho.org/get-started/resources/audits/) |
| S-SC-04 | Have all critical and high-severity audit findings been fully remediated and re-verified? | Yes. Blackthorn V2 audit found 1 High and 5 Medium findings, all resolved and re-verified during formal fix review period. ChainSecurity V2 audit identified asset solvency issues that were fixed before deployment. Certora formal verification provides mathematical proof of critical invariants. | 9 | 9 | Non-Improvable (optimal) | [P1] [Sherlock/Blackthorn](https://sherlock.xyz/case-studies/morpho), [P1] [ChainSecurity V2](https://www.chainsecurity.com/security-audit/morpho-vault-v2) |
| S-SC-05 | Are core contracts upgradeable and how tightly are upgrades constrained? | VaultV2 contract is immutable (non-upgradeable, ERC4626 compliant, verified on Etherscan). All vault contracts are stated as immutable per Morpho docs. Adapter additions require Curator + 3-day timelock. Adapter removals require 7-day timelock. The Owner DAO proxy (0xe3Acb3A0) is itself an ERC1967 upgradeable proxy, but it is the governance contract, not the fund-custody contract. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51#code), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-SC-06 | Has any on-chain exploit or critical bug affecting user funds occurred? | No confirmed exploit causing user fund loss in Steakhouse vaults or in the V2 vault architecture. The V2 vault launched October 27, 2025 with no incidents since. The April 2025 frontend event (Bundler3 SDK misconfiguration, ~24h exposure window) resulted in $2.6M intercepted by a whitehat who returned funds in full; on-chain contracts were unaffected. The March 2026 Resolv exploit caused ~$6.2M bad debt across 11 other Morpho vaults, but Steakhouse vaults had no USR exposure and recorded zero losses. A March 2026 Steakhouse domain phishing episode did not affect on-chain contracts. The April 2026 KelpDAO/rsETH exploit (~$292M stolen via LayerZero bridge manipulation) caused over $200M in estimated bad debt on Aave; Morpho had only ~$1M exposure across two isolated markets and Steakhouse had <$0.01 exposure, exiting immediately with zero bad debt. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/), [P2] [DeFi Markets Update 2026-04-22](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-04-22) |
| S-SC-07 | Has any confirmed rug-pull event occurred? | No rug-pull events. Morpho operates as ADDMO, a French nonprofit association. Steakhouse has 2+ year track record managing curated vaults. No credible allegations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/) |
| S-SC-08 | Were there reductions to the timelock delay that weaken governance protections? | No reductions. The V2 vault was deployed with per-function timelocks on October 27, 2025. Critical functions have 7-day timelocks (removeAdapter, abdicate, gate functions), moderate functions have 3-day timelocks (addAdapter, cap increases). No changes to any timelock durations since deployment. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (timelocks confirmed via API query) |
| S-SC-09 | Does the protocol run an active bug-bounty via a reputable platform? | Yes. Dual active bounties: (1) Cantina with $2.5M max payout, 573 findings submitted, scope explicitly covers Morpho V2 contracts (VaultV2Factory, adapter factories, Registry); (2) Immunefi with $2.5M max payout for Morpho Blue, $1.5M for periphery. Both are Tier-0 platforms. V2 contracts are explicitly in scope on both platforms. | 9 | 9 | Non-Improvable (optimal) | [P1] [Cantina Bounty](https://cantina.xyz/bounties/35a5f0a1-2ffd-432c-8f3b-77d169add8c3), [P1] [Immunefi Bounty](https://immunefi.com/bug-bounty/morpho/) |
| S-SC-10 | Are real-time security monitoring and alerting systems in place? | Internal monitoring bots perform continuous invariant checks. Chainalysis partnership for transaction monitoring. However, monitoring cannot automatically trigger protective actions -- all responses require manual human intervention. The April 2025 frontend incident had a ~24h exposure window before detection (rollback executed within 4 minutes of alert). The March 2026 Resolv exploit further demonstrated this limitation: monitoring did not trigger automated containment, and the Public Allocator continued directing capital into impaired markets for ~10 hours. The V2 vault's allocator-driven capital flows are not covered by any automated halt mechanism. | 3 | 9 | **Improvable** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| S-SC-11 | Are automatic safety controls (pause, circuit breakers) triggered by monitoring alerts? | No automatic on-chain circuit breakers by design. Morpho prioritizes immutability over admin controls. The Sentinel (Revoker contract) can only revoke pending timelocked actions -- it cannot pause the protocol or halt allocations. No circuit breakers cover the V2 vault's allocator-driven capital flows. Market-level isolation in Morpho Blue provides containment. | 3 | 3 | Non-Improvable | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/), [P0] [Etherscan Revoker](https://etherscan.io/address/0x76303D5Ef2Effb6B489F6d9051e6B409962aB715) |

**Smart Contract Security Subtotal: 158.2/180 (87.9%)**
- 9 questions scored 9 (sum = 81), 2 questions scored 3 (sum = 6)
- Raw sum = 87 out of max 99
- Weighted = (87/99) x 180 = 158.2

---

#### Key Management & Permissions (20% weight, 180 max points)

**NOTE: V2-specific governance architecture. Unlike the V1 vault's 5-of-8 Safe multisig owner, the V2 vault's Owner is an Aragon DAO proxy. The Sentinel is a Revoker contract restricted to the revoke function only. Per-function timelocks range from 0s to 7 days. These differences justify different scores from V1 on S-KM-01, S-KM-02, S-KM-03.**

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| S-KM-01 | Who controls admin and upgrade keys for contracts holding user funds? | Owner: Aragon DAO proxy (0xe3Acb3A0, ERC1967Proxy to Aragon OSx DAO implementation 0x58C1F7Bc). Created on October 27, 2025 by 0xfeed46c1 (Steakhouse deployer). This is a DAO contract, not a multisig -- voting power distribution and decision-making process not publicly verified. Sentinel: Revoker contract (0x76303D5E) restricted to revoke-only capability. 18 Curator addresses listed (including 0x827e..., the V1 curator multisig, among others). Changes to adapter registry require 7-day timelocks; fee changes have 0s timelock. | 3 | 9 | **Source Missing** | [P0] [Etherscan Owner](https://etherscan.io/address/0xe3Acb3A0cC24C7b176101900715e38E8e789DAd4), [P0] [Etherscan DAO Impl](https://etherscan.io/address/0x58C1F7Bc62bb63fb137bc8f6d8ea6321a0501d29), [P0] [Morpho V2 API](https://api.morpho.org/graphql) |
| S-KM-02 | Can any single key move user funds or upgrade custody contracts? | No. The VaultV2 contract is immutable (non-upgradeable). Moving user funds requires going through Morpho Blue's immutable contract logic -- users always have permissionless ERC4626 redemption plus forceDeallocate for in-kind exit. The Owner DAO cannot directly access funds. Allocators can only move funds to/from enabled adapters within curator-set caps. While fee-related timelocks are 0s (allowing instant fee changes up to 50% performance / 5% management), this affects yield, not principal custody. Adapter additions require 3-day timelock, removals 7-day. Per the framework, DAO governance with timelocks >= 24h on critical functions meets Low (9) criteria. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan VaultV2](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51#code), [P0] [Morpho V2 API](https://api.morpho.org/graphql) (timelocks confirmed), [P1] [V2 Architecture](https://docs.morpho.org/learn/concepts/vault-v2/) |
| S-KM-03 | How decentralized and robust is the multisig for critical actions? | Owner is an Aragon DAO proxy, not a traditional multisig. The DAO implementation (Aragon OSx v1.4.0) was created March 7, 2025. Voting power distribution, quorum requirements, and signer independence CANNOT be verified on-chain -- the DAO has only 1 internal transaction (creation). No public documentation found describing who can vote, what the quorum is, or how many independent participants control the DAO. The Steakhouse blog states V1 vault guardians are "Aragon DAO composed of depositors" with proportional voting rights, but this specific V2 Owner DAO has no such documentation. Without verifiable governance parameters, independence cannot be confirmed -- score capped at Mid (3) per framework Source Missing rule. | 3 | 9 | **Source Missing** | [P0] [Etherscan DAO](https://etherscan.io/address/0xe3Acb3A0cC24C7b176101900715e38E8e789DAd4), [P0] [Etherscan DAO Impl](https://etherscan.io/address/0x58C1F7Bc62bb63fb137bc8f6d8ea6321a0501d29), [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |
| S-KM-04 | How constrained are pause, blocklist and withdrawal-control permissions? | No address-level blocking capability on the VaultV2 contract. No pause function on either the VaultV2 or Morpho Blue (both immutable). Withdrawals always permissionless via ERC4626 redeem/withdraw plus forceDeallocate for in-kind exit. Sentinel can only revoke pending timelocked actions. Gates (access control contracts) can restrict deposits/withdrawals but require 7-day timelock to change. Rules publicly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] [Morpho V2 API](https://api.morpho.org/graphql) (gate timelocks = 604800s) |
| S-KM-05 | Are all user assets held in non-custodial smart contracts? | Yes. 100% of user assets held in non-custodial on-chain contracts. V2 vault deploys through MetaMorpho adapter into V1 Steakhouse USDC vault, which deploys into Morpho Blue markets. All on Ethereum. Permissionless redemption via ERC4626. forceDeallocate provides additional exit path. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P0] [Morpho V2 API](https://api.morpho.org/graphql) |
| S-KM-06 | Are user funds fully segregated from treasury and operational wallets? | Yes. Clear on-chain segregation. V2 vault funds flow through MetaMorpho adapter to V1 vault to Morpho Blue markets. Morpho is a nonprofit with no profit extraction from protocol operations. Both performance and management fees are 0% (confirmed via V2 API). No co-mingling with treasury or operational wallets. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (performanceFee=0, managementFee=0) |
| S-KM-07 | What are the whitelisted protocols the vault strategy can interact with? | On-chain enforced adapter whitelist. Currently 2 adapters enabled: (1) MetaMorpho adapter (0xFc98D1...) pointing to the Steakhouse USDC V1 vault, and (2) Markets V1 Adapter (0x2b9681...) providing direct access to Morpho Blue markets, added in April 2026 as part of a Morpho-requested operational simplification. Both adapters access the same underlying Morpho Blue lending markets. New adapter additions require Curator + 3-day timelock. Adapter removals require 7-day timelock. The MorphoRegistry (0x3696c5...) provides additional adapter validation. Absolute and relative caps enforce per-adapter limits. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P2] [V2 Simplification](https://forum.morpho.org/t/steakhouse-vault-v2-simplification/2235) |
| S-KM-08 | Is there a tested incident playbook for admin-key compromise or signer loss? | Limited. The V2 vault introduces a novel DAO owner structure where incident response for key compromise is unclear. For the V1 vault, the Guardian drill (January 2024) tested veto mechanisms but not key rotation. For the V2 vault, no documented playbook exists for DAO compromise, signer loss, or sentinel compromise scenarios. The Supervisor v2 system is new with no published incident response documentation specific to V2 architecture. | 3 | 9 | **Improvable** | [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |

**Key Management Subtotal: 135.0/180 (75.0%)**
- 5 questions scored 9 (sum = 45), 3 questions scored 3 (sum = 9)
- Raw sum = 54 out of max 72
- Weighted = (54/72) x 180 = 135.0

**Improvement Opportunities:**
- **S-KM-01** (+15.0 weighted points): Publish DAO governance parameters (quorum, voting power distribution, proposal thresholds)
- **S-KM-03** (+15.0 weighted points): Publish verifiable DAO membership, quorum requirements, and demonstrate independence of governance participants
- **S-KM-08** (+15.0 weighted points): Publish V2-specific incident response playbook with DAO key rotation procedures

---

### **Security Total: 293.2/360 (81.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Smart Contract Security | 158.2 | 180 | 87.9% |
| Key Management | 135.0 | 180 | 75.0% |
| **Security Total** | **293.2** | **360** | **81.4%** |

---

### STRATEGY (30% Weight) -- Score: 233.2/270 (86.4%)

**NOTE: Strategy scores are largely consistent with the Steakhouse USDC V1 vault rating because the V2 vault deploys assets into the same Morpho Blue markets via two adapters (MetaMorpho adapter to V1 vault + Markets V1 Adapter for direct market access). The underlying strategy, collateral, counterparties, and liquidity dynamics are the same. The 6-point difference from V1 (233.2 vs 239.2) is driven by ST-M-01 (3 vs 9) -- the V2 vault token has not been tested under direct redemption pressure (the vault received inflows during the April 2026 Kelp exploit rather than experiencing withdrawal stress), while the V1 vault token (steakUSDC) demonstrated stable value through November 2025 stress.**

#### Protocol Mechanics (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PM-01 | What are the sources of yield and is it aligned with the mandate? | All yield from overcollateralized USDC lending against blue-chip crypto collateral (cbBTC, WBTC, wstETH) via the underlying V1 vault. 100% mandate-aligned. Yield sources explicitly documented. Steakhouse Prime Instant product line described as "Repo strategy (overcollateralized, variable-rate lending) with instant liquidity" targeting underlying risk rating of A or above. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Prime Instant](https://www.steakhouse.financial/docs/products/vault-products/current/prime-instant), [P0] [Morpho V2 API](https://api.morpho.org/graphql) |
| ST-PM-02 | Under which conditions does net yield become negative or cause loss? | Loss limited to rare tail shocks: simultaneous BTC/ETH crash exceeding the liquidation buffer (86% LLTV provides ~14% buffer), oracle manipulation on immutable oracle, or catastrophic wrapped-asset custodian failure. Bad debt per market is isolated and socialized among lenders. Identical risk profile to V1 vault since funds flow to same markets. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks), [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-03 | Is leverage or rehypothecation used and up to what effective level? | No. Vault simply lends USDC via V1 vault. No rehypothecation. Effective leverage: 1.0x. The V2 wrapper adds no leverage. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-04 | Are there automated mechanics to prevent Liquidation Events? | N/A -- Vault is a lender, not a borrower. Liquidation risk applies to borrowers. Liquidations protect lenders by restoring market solvency; the Liquidation Incentive Factor goes entirely to liquidators, not to lenders. | N/A | N/A | N/A | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |
| ST-PM-05 | Has this strategy or a close variant ever experienced negative yield? | No permanent-loss events for Steakhouse USDC vault or comparable Steakhouse vaults since January 2024 launch. The V2 vault deploys into the same V1 vault which has zero bad debt history. During November 2025 Stream/Elixir contagion, Steakhouse vaults had ZERO bad debt (confirmed by Steakhouse). | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |
| ST-PM-06 | Is a risk framework for vault curation or protocol mechanics documented? | Yes. Steakhouse publishes vault controls documentation with DDQ process (2 internal + 1 external reviewer). Prime Instant product line specifies: underlying risk rating A or above, maximum duration 1 week, aggregated target maturity 1 day (25% allowance). Credora A+ rating. On-chain caps per market. | 9 | 9 | Non-Improvable (optimal) | [P1] [Vault Controls](https://www.steakhouse.financial/docs/risk-management/monitoring/vault-setup-and-controls), [P1] [Prime Instant](https://www.steakhouse.financial/docs/products/vault-products/current/prime-instant) |
| ST-PM-07 | Is current yield sustainable relative to underlying economics? | Yes. Yield is entirely organic from USDC lending demand driven by BTC/ETH leveraged borrowers via the V1 vault. No emissions or token incentives required. V2 vault APY (3.85% as of late April 2026) reflects organic lending demand plus Morpho V2 incentives; core yield is organic. Both performance and management fees are 0%. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| ST-PM-08 | Can the position be fully unwound under conservative liquidity assumptions without slippage turning yield negative? | Yes. USDC is the most liquid stablecoin. The V2 vault also has forceDeallocate which allows permissionless in-kind redemption of underlying positions even during illiquidity (with up to 2% penalty). During November 2025 stress, a Chorus One industry report estimated ~80% of withdrawals across affected Morpho vaults completed within 3 days (ecosystem-wide figure, not vault-specific). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) (forceDeallocate), [P3] [Chorus One Report](https://chorus.one/reports-research/defi-curators-in-2025-navigating-chaos-building-resilience) |
| ST-PM-09 | Does the strategy rely on a spread, peg, or funding rate that can invert? | No. Pure lending interest from overcollateralized borrower demand. No basis trade, peg arbitrage, or funding rate dependency. Interest rates set by immutable Adaptive Curve IRM. | 9 | 9 | Non-Improvable (optimal) | Analytical assessment |
| ST-PM-10 | Can automated or externally-invocable mechanisms increase vault exposure without real-time human approval? | Yes. The V2 vault has 3 allocator addresses (0x0000aeB7..., 0xaaD84c80..., 0xfeed46c1...) that can allocate funds to the 2 enabled adapters (MetaMorpho adapter to V1 vault + Markets V1 Adapter for direct Morpho Blue access) without real-time human approval. Exposure is constrained to these adapters with pre-configured caps. Unlike the V1 vault's Public Allocator (permissionless), V2 allocators are appointed addresses -- reducing the "anyone can invoke" risk. But no automatic kill-switch exists for abnormal conditions. Halting requires curator or sentinel intervention (manual). | 3 | 9 | **Improvable** | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (allocators confirmed), [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Protocol Mechanics Subtotal: 41.7/45 (92.6%)**
- 9 applicable questions (ST-PM-04 = N/A): 8 scored 9 (sum = 72), 1 scored 3 (sum = 3)
- Raw sum = 75 out of max 81
- Weighted = (75/81) x 45 = 41.7

---

#### Collateral (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-C-01 | Which assets are accepted as collateral and how are they risk rated? | Blue-chip only (via V1 vault): cbBTC (Coinbase custody), WBTC (BitGo/BiT Global), wstETH (Lido). All are established, high-market-cap assets. Credora A+ risk rating. LLTV set at 86% for BTC collateral markets. Risk tiering applied per market. Identical to V1 vault. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (underlying V1 vault confirmed) |
| ST-C-02 | How did each collateral behave versus its underlying during past stress or depegs? | cbBTC: No depeg >2% in its history since September 2024 launch. WBTC: Brief depegs during Alameda concerns (Nov 2022) and Justin Sun controversy (Aug 2024) but recovered within 24h. wstETH: Stable tracking. No collateral showed >2% depeg lasting >24h in last 12 months. Identical to V1 vault. | 9 | 9 | Non-Improvable (optimal) | Market data |
| ST-C-03 | How is validator or slashing risk handled for staking-based collaterals? | Only wstETH (~2% of underlying TVL) has staking exposure. Lido uses 30+ diversified operators. Lido slashing insurance/coverage fund absorbs minor events. Risk immaterial given tiny allocation. | 9 | 9 | Non-Improvable (optimal) | Lido operator data |
| ST-C-04 | What share of TVL relies on bridged or wrapped assets? | HIGH RISK: Approximately 98% of underlying V1 vault TVL is in wrapped assets (primarily cbBTC and WBTC markets). Per the framework definition, cbBTC (Coinbase custody) and WBTC (BitGo/BiT Global) are wrapped BTC representations. Exceeds 60% threshold significantly. Identical to V1 vault. | 1 | 9 | **Improvable** | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (underlying V1 vault allocation) |

**Collateral Subtotal: 35.0/45 (77.8%)**
- 3 questions scored 9 (sum = 27), 1 question scored 1
- Raw sum = 28 out of max 36
- Weighted = (28/36) x 45 = 35.0

---

#### Infrastructure Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-IC-01 | Which chains, bridges, oracles, wallets and CEXs does the strategy depend on? | All Tier-0: Ethereum (chain), Morpho oracle adapter contracts (MorphoChainlinkOracleV2 / MorphoChainlinkOracle) consuming primarily Chainlink-sourced data feeds via underlying V1 vault markets. The cbBTC market hardcodes a 1:1 cbBTC=BTC assumption (no cbBTC/BTC price feed); the wstETH market uses a custom WstETHPriceFeed (Chainlink-interface-compatible, not a Chainlink product). No bridges required. No CEX dependency. | 9 | 9 | Non-Improvable (optimal) | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P0] [Etherscan cbBTC Oracle](https://etherscan.io/address/0xA6D6950c9F177F1De7f7757FB33539e3Ec60182a), [P0] [Etherscan WstETHPriceFeed](https://etherscan.io/address/0x4F67e4d9BD67eFa28236013288737D39AeF48e79) |
| ST-IC-02 | How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions? | SINGLE ORACLE RISK with immutable pricing (inherited from V1 vault). Each Morpho Blue market has one immutable Morpho oracle adapter -- no fallback mechanism and values cannot be corrected. Oracles use multi-hop routing: cbBTC/USDC hardcodes 1:1 cbBTC=BTC (no depeg tracking -- a cbBTC depeg would not trigger liquidations); WBTC/USDC chains three Chainlink feeds (WBTC/BTC + BTC/USD + USDC/USD); wstETH/USDC uses a custom WstETHPriceFeed with on-chain exchange rate + Chainlink stETH/ETH; WETH/USDC uses a Chainlink SVR proxy. Underlying Chainlink feeds price deep-liquidity pairs (BTC/USD, ETH/USD) where material depeg historically unprecedented, but multi-hop routing and cbBTC hardcoded peg add trust assumptions. Zero redundancy by design. Caps at Mid (3). | 3 | 3 | Non-Improvable | [P1] [Oracle Docs](https://docs.morpho.org/learn/concepts/oracle/), [P0] [Etherscan cbBTC Oracle](https://etherscan.io/address/0xA6D6950c9F177F1De7f7757FB33539e3Ec60182a) |
| ST-IC-03 | Are off-chain infrastructure providers certified by standard IT security audits? | No public SOC 2 Type II or ISO27001 certification found for Morpho Labs/ADDMO or Steakhouse Financial. Chainlink: enterprise certifications. Coinbase (cbBTC custodian): NY DFS regulated, SOC 2 certified. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| ST-IC-04 | How did these infra components behave in past outages or chain incidents? | Ethereum: No significant halts. Morpho: April 2025 frontend incident had ~24h exposure window (rollback in 4 minutes after alert); $2.6M intercepted and returned by whitehat. March 2026 Resolv exploit caused ~$6.2M bad debt in 11 other Morpho vaults; Steakhouse vaults unaffected (no USR exposure). November 2025 stress: protocol operated correctly. March 2026 Steakhouse domain phishing: contracts unaffected. No blocking of on-chain withdrawals. | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| ST-IC-05 | Has the base chain recently halted block production or experienced consensus failure? | No. Ethereum has had no chain halts >30 minutes in the last 12+ months. Tier-0 chain reliability. | 9 | 9 | Non-Improvable (optimal) | Ethereum operational history |
| ST-IC-06 | Has the validator set experienced slashing events that could impact staked collateral? | Only relevant for wstETH (~2% TVL). Lido slashing events have been trivial and fully absorbed by Lido's coverage fund. No depositor impact. | 9 | 9 | Non-Improvable (optimal) | Lido slashing data |
| ST-IC-07 | Are validators diverse geographically and by operator? | Ethereum validator set is highly distributed. Lido (for wstETH) uses 30+ independent operators. No single operator >33% of relevant stake. | 9 | 9 | Non-Improvable (optimal) | Ethereum validator data |
| ST-IC-08 | Can any single infra component failure alone block withdrawals or cause losses? | No. Permissionless on-chain redemption always available via ERC4626 redeem/withdraw. V2 adds forceDeallocate as a permissionless in-kind backstop (converts vault position to underlying market position, not USDC, with configurable penalty up to 2%). No off-chain dependency for withdrawals. Frontend failure does not block on-chain operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-IC-09 | How robust is the cross-chain messaging or bridge verification setup? | N/A -- The vault operates exclusively on Ethereum with no cross-chain messaging or bridge dependency. | N/A | N/A | N/A | Vault architecture |
| ST-IC-10 | Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting? | N/A -- No cross-chain escrow or minting mechanism exists for this vault. | N/A | N/A | N/A | Vault architecture |
| ST-IC-11 | Is the off-chain verification infrastructure resilient to data-source manipulation? | N/A -- The vault does not rely on off-chain verifiers or cross-chain attestation infrastructure. All oracle data is consumed on-chain via Morpho oracle adapters. | N/A | N/A | N/A | Vault architecture |

**Infrastructure Counterparty Subtotal: 37.5/45 (83.3%)**
- 11 questions total, 3 N/A (ST-IC-09/10/11). 8 scored: 6 scored 9 (sum = 54), 2 scored 3 (sum = 6)
- Raw sum = 60 out of max 72
- Weighted = (60/72) x 45 = 37.5

---

#### Protocol Counterparty Exposures (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-PC-01 | Into which external protocols, CEXs or RWA platforms is collateral deployed? | All allocation to Morpho Blue markets via two adapters: MetaMorpho adapter to V1 Steakhouse USDC vault and Markets V1 Adapter for direct market access (Tier-0 protocol, 25+ audits, formally verified). No CEX exposure. No RWA platforms. Both adapters access the same underlying Morpho Blue markets. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) |
| ST-PC-02 | Are revenue-share or incentive arrangements documented and do they create conflicts? | Yes. Both V2 performance fee and management fee are 0% (confirmed via V2 API). Fee changes have 0s timelock -- an instant fee change risk, but currently no fees are charged. No hidden rebates or undisclosed arrangements. Coinbase partnership is public. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (performanceFee=0, managementFee=0) |
| ST-PC-03 | Are there hard limits and rebalancing rules per counterparty? | Yes. On-chain caps (absolute and relative) per adapter enforced by V2 contract. Currently only 1 adapter enabled with 100% allocation to V1 vault. Cap increases require 3-day timelock. Cap decreases are instant (risk-reducing). | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-PC-04 | How quickly and safely can positions be unwound from each counterparty? | Positions can be unwound from V1 vault as borrowers repay. forceDeallocate provides a permissionless backstop that converts vault shares into the underlying market position (not USDC), with a configurable penalty of up to 2% per adapter. This bypasses vault-level liquidity constraints but the received position remains illiquid until borrowers repay. During November 2025 stress, a Chorus One industry report estimated ~80% of withdrawals across affected Morpho vaults completed within 3 days (ecosystem-wide, not vault-specific). No discretionary approvals needed. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P3] [Chorus One Report](https://chorus.one/reports-research/defi-curators-in-2025-navigating-chaos-building-resilience) |
| ST-PC-05 | Are third-party validators, custody providers or asset managers disclosed? | Pure on-chain lending -- no external validators, custodians, or asset managers involved. Steakhouse Financial (curator) is fully disclosed. Underlying collateral custodians (Coinbase for cbBTC, BitGo for WBTC, Lido for wstETH) are publicly known. | 9 | 9 | Non-Improvable (optimal) | Vault architecture |

**Protocol Counterparty Subtotal: 45.0/45 (100.0%)**
- 5 questions, all scored 9
- Raw sum = 45 out of max 45
- Weighted = (45/45) x 45 = 45.0

---

#### Liquidity (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-L-01 | How are withdrawals executed and can they be paused, blocked or delayed? | Permissionless on-chain redemption via ERC4626 standard. V2 adds forceDeallocate as a permissionless in-kind backstop: converts vault position to underlying market position (not USDC), with configurable penalty up to 2% per adapter (an optional flashloan-based workflow exists for capital-efficient in-kind redemptions but is not required). No address-level blocking. No admin pause. Normal USDC withdrawal availability depends on underlying V1 vault liquidity. Gate changes require 7-day timelock. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |
| ST-L-02 | Is there enough liquidity to redeem close to 100% of TVL within stated withdrawal time? | Moderate. V2 vault TVL ($32.4M as of late April 2026) is moderate relative to V1 vault TVL ($120.3M as of late April 2026), so V2 exits should process under normal conditions. However, during stress, underlying market utilization can reach high levels. A Chorus One industry report estimated ~80% of withdrawals across affected Morpho vaults completed within 3 days during November 2025 (ecosystem-wide, not vault-specific). Permissionless forceDeallocate provides additional in-kind exit path. | 3 | 3 | Non-Improvable | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P3] [Chorus One Report](https://chorus.one/reports-research/defi-curators-in-2025-navigating-chaos-building-resilience) |
| ST-L-03 | Have there been past withdrawal delays, queues or freezes? | The V2 vault launched October 27, 2025 with no reported delays. The underlying V1 vault experienced minor delays during November 2025 stress only, with >95% of withdrawals completing promptly over the full 12-month period. No prolonged freezes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-04 | Do caps or limits restrict timely redemptions during high utilization? | Caps appropriately sized. V2 vault ($32.4M as of late April 2026) has grown but remains moderate relative to underlying market depth. Underlying V1 vault caps are transparent and on-chain. Rate model creates strong incentive for borrower repayment. No history of caps being manipulated to block exits. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-L-05 | How does exit liquidity behave during volatility and network congestion? | V2 vault inherits V1 liquidity dynamics. During November 2025, some Morpho markets temporarily reached 100% utilization. Steakhouse vaults experienced temporary illiquidity but access remained available. forceDeallocate provides an additional backstop for V2 depositors but yields an illiquid market position rather than USDC, and requires a flashloan-based workflow. Conditions normalized within days. | 3 | 3 | Non-Improvable | [P1] [Morpho Nov 2025](https://morpho.org/blog/morpho-effect-november-2025/) |
| ST-L-06 | Do withdrawals rely on unstaking, vesting, or bridge exits longer than stated period? | No. Pure USDC lending with no lockups, vesting, or bridge dependencies. forceDeallocate provides a permissionless in-kind backstop when normal USDC liquidity is unavailable, though the received market position remains illiquid until borrowers repay. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-07 | Does redemption depend on secondary-market liquidity and is it sufficient? | No. Primary redemption through ERC4626 vault always available. forceDeallocate provides an additional in-kind backstop (underlying market position, not USDC). No secondary market required for exit. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-L-08 | What is the liquidity depth of collateral and receipt tokens? | USDC is the most liquid stablecoin. The V2 vault token has grown to $32.4M TVL (as of late April 2026, up from $7.96M at initial rating), improving secondary market depth. For the underlying USDC claim, depth is excellent. In-protocol redemption provides the primary exit path. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P3] [Vaults.fyi](https://app.vaults.fyi/opportunity/mainnet/0xbeef088055857739C12CD3765F20b7679Def0f51) |
| ST-L-09 | What is the risk of bank-run scenarios under full utilization? | Moderate. Bank run at V2 level causes exits from the underlying Morpho Blue markets. V2's size ($32.4M vs $120.3M V1 as of late April 2026) means V2 exits alone would not stress underlying liquidity severely but represent a larger share than at initial rating. Bank run at V1 level causes temporary queues and rate spikes (4x at 100% utilization). forceDeallocate provides additional exit path for V2 depositors. November 2025 demonstrated zero permanent losses for Steakhouse depositors. | 3 | 3 | Non-Improvable | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |

**Liquidity Subtotal: 35.0/45 (77.8%)**
- 6 questions scored 9 (sum = 54), 3 questions scored 3 (sum = 9)
- Raw sum = 63 out of max 81
- Weighted = (63/81) x 45 = 35.0

---

#### Market (5% weight, 45 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| ST-M-01 | How has the LST or receipt token peg performed under market stress? | V2 vault token represents USDC claims plus accrued yield (ERC4626 share price). The vault operated through the April 2026 KelpDAO/rsETH exploit without issues, but this did not test the vault's exit mechanisms under direct redemption pressure — the vault experienced net deposits, not withdrawals, during the period. The underlying V1 vault's steakUSDC token maintained stable value through November 2025 stress. Per framework scoring principle: the V2 token has not demonstrated resilience under withdrawal stress, scored Mid (3). | 3 | 3 | Non-Improvable | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P2] [DeFi Markets Update 2026-04-22](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-04-22) |
| ST-M-02 | How likely can adverse crypto market moves cause permanent losses due to directional exposure? | Very low. Vault lends USDC -- deposits and returns denominated in USDC. No directional BTC/ETH exposure for lenders. Risk is borrower default/bad debt, not market direction. | 9 | 9 | Non-Improvable (optimal) | Vault mechanics |
| ST-M-03 | Are interest rate/incentive models robust during TVL shifts or volatility spikes? | Yes. Immutable Adaptive Curve IRM per market (inherited from V1 vault). Rates auto-increase with utilization. No governance manipulation possible. No history of prolonged >=95% utilization beyond brief stress episodes. | 9 | 9 | Non-Improvable (optimal) | [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| ST-M-04 | Have historic scenarios with high market volatility been explicitly modeled? | Yes. 86% LLTV provides 14% buffer before liquidation. Liquidation mechanism formally verified by Certora. Certora proved reentrancy safety, market independence, arithmetic integrity, and withdrawal safeguards. V2 contract also formally verified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Formal Verification](https://morpho.org/blog/formally-verifying-morpho-blue-with-certorav/) |
| ST-M-05 | Can sharp price moves trigger forced liquidations that crystallize losses? | Borrower-side only. Liquidations protect lenders by restoring market solvency and preventing bad debt; the LIF (~5% at 86% LLTV) goes entirely to liquidators, not to lenders. Risk to lenders: insufficient or slow liquidation creating bad debt that is socialized among lenders. Mitigated by economic incentives for liquidators and 14% buffer at 86% LLTV. | 9 | 9 | Non-Improvable (optimal) | [P1] [Liquidation](https://docs.morpho.org/learn/concepts/liquidation/) |

**Market Subtotal: 39.0/45 (86.7%)**
- 4 questions scored 9 (sum = 36), 1 question scored 3 (sum = 3)
- Raw sum = 39 out of max 45
- Weighted = (39/45) x 45 = 39.0

---

### **Strategy Total: 233.2/270 (86.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Protocol Mechanics | 41.7 | 45 | 92.6% |
| Collateral | 35.0 | 45 | 77.8% |
| Infra Counterparty | 37.5 | 45 | 83.3% |
| Protocol Counterparty | 45.0 | 45 | 100.0% |
| Liquidity | 35.0 | 45 | 77.8% |
| Market | 39.0 | 45 | 86.7% |
| **Strategy Total** | **233.2** | **270** | **86.4%** |

---

### OPERATIONS (30% Weight) -- Score: 227.75/270 (84.4%)

**NOTE: Operations scores differ from the Steakhouse USDC V1 vault (239.0/270) due to O-G-02 scoring 3 (unverified DAO voting concentration) vs V1's 9 (depositor-proportional Guardian DAO). Team, documentation, and financial resilience are platform-level and identical.**

#### Governance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-G-01 | What governance model controls protocol changes and upgrades? | Hybrid with strong checks. Morpho Blue: immutable (no upgrades possible). V2 vault: Owner DAO controls top-level permissions + per-function timelocks + Sentinel veto. Curator manages risk parameters. Allocators execute within caps. Multiple independent layers prevent unilateral changes. Owner DAO cannot directly access funds. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/) |
| O-G-02 | How concentrated is voting power among top holders or delegates? | The Owner DAO is an Aragon DAO proxy. Steakhouse describes V1 guardian DAOs as "composed of depositors" with proportional voting -- if this applies to the V2 Owner DAO, then voting power is distributed across depositors. However, the specific DAO configuration (quorum, proposal threshold, voting power distribution) could not be verified on-chain. The DAO has only 1 internal transaction (creation). Without verifiable voting distribution, scored Mid (3). | 3 | 9 | **Source Missing** | [P0] [Etherscan DAO](https://etherscan.io/address/0xe3Acb3A0cC24C7b176101900715e38E8e789DAd4), [P2] [Supervisor V2 Blog](https://kitchen.steakhouse.financial/p/launching-supervisor-v2-and-migration) |
| O-G-03 | Are mechanisms in place to limit major changes like timelocks and veto? | Yes. Per-function timelocks: critical operations 7 days (removeAdapter, abdicate, gate changes), moderate operations 3 days (addAdapter, cap increases, increaseTimelock). Sentinel (Revoker contract) can veto any pending timelocked action. Sentinel cannot be removed without Owner DAO action. All timelocks verified via V2 API. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql) (all 18 timelocks verified) |
| O-G-04 | Can the protocol replace the strategy manager without blocking user withdrawals? | Yes. Owner DAO can appoint new Curator (curators are a list in V2, not a single address). Withdrawals remain permissionless via ERC4626 throughout, with forceDeallocate available as an in-kind backstop. Users can always exit regardless of curator changes. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Governance Subtotal: 56.25/67.5 (83.3%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3 (sum = 3)
- Raw sum = 30 out of max 36
- Weighted = (30/36) x 67.5 = 56.25

---

#### Team & Legal & Compliance (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-TL-01 | Are core team and operating entities publicly identified and credible? | Yes. Steakhouse: adcv (co-founder, former M&A/investment banking), Sebastien Derivaux (co-founder, former MakerDAO Head of RWA). Morpho: Paul Frambot (CEO), Merlin Egalite, Mathis Gontier Delaunay. All publicly identified with verifiable professional backgrounds. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse](https://www.steakhouse.financial/), [P1] [Morpho](https://morpho.org/) |
| O-TL-02 | Is the protocol dependent on a single developer or small team? | No. Morpho has a full team (ADDMO + Morpho Labs SAS, ~$73.6M raised, 29 investors). Steakhouse Financial is a separate entity with its own team. Multiple independent parties capable of vault operations. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-TL-03 | What legal entity and jurisdiction operate the protocol and/or assets? | Morpho: ADDMO (French nonprofit, W751263773, Paris) + Morpho Labs SAS (France, RCS 902 498 492). Steakhouse: Carniceria Tropical Inc. (Panama) + Steakhouse Financial Ltd (Cayman Islands). All entities clearly identified. | 9 | 9 | Non-Improvable (optimal) | [P1] [Legal Notice](https://morpho.org/legal-notice/), [P2] [Forum](https://forum.morpho.org/t/key-information-on-steakhouse-branded-vaults/1343) |
| O-TL-04 | Are there known investigations or regulatory actions related to the entity? | No known ongoing or past material enforcement actions against ADDMO, Morpho Labs, Steakhouse Financial, or Carniceria Tropical in any major jurisdiction. | 9 | 9 | Non-Improvable (optimal) | Public records |
| O-TL-05 | Is there an on-call and incident response process for core teams? | Partial evidence. Monitoring bots + Chainalysis partnership confirmed. April 2025 incident: ~24h exposure window before detection, 4-minute rollback after alert. However, no public 24/7 on-call SLA, formal incident runbook, or response SLA for V2-specific architecture found. Per v0.1-gamma automation override: the V2 vault uses appointed allocators (less risky than V1's Public Allocator), but incident response documentation does not include procedures to halt V2 allocator flows. | 3 | 9 | **Source Missing** | [P1] [Security Framework](https://morpho.org/blog/morpho-blue-security-framework-building-the-most-secure-lending-protocol/) |
| O-TL-06 | Does the team provide timely support for critical user or integrator issues? | Yes. April 2025: 4-minute rollback after alert (~24h total exposure); $2.6M returned by whitehat. Active Discord community. March 2026 domain phishing: team warned users promptly. Steakhouse publishes regular Substack updates (Kitchen newsletter). | 9 | 9 | Non-Improvable (optimal) | [P1] [Incident Report](https://morpho.org/blog/morpho-app-incident-april-10-2025/) |
| O-TL-07 | Are major investors or strategic partners disclosed? | Yes. Morpho: a16z, Variant Fund, Pantera Capital, Coinbase Ventures, Ribbit Capital (29 investors total, $73.6M raised). Coinbase partnership for crypto-backed loans publicly announced. | 9 | 9 | Non-Improvable (optimal) | [P1] [Pantera](https://panteracapital.com/blog-investing-in-morpho/) |
| O-TL-08 | Does the strategy manager manage similar vaults creating conflict of interest? | Yes. Steakhouse manages 19+ vaults across Ethereum and Base. Potential for allocation decisions to favor some vaults over others. Limited hard constraints -- DDQ process and Credora rating provide qualitative controls, but no formal conflict-of-interest policy with quantitative rules published. V2 introduces additional complexity as it wraps V1 vault. | 3 | 9 | **Improvable** | [P1] [Current Products](https://www.steakhouse.financial/docs/products/vault-products/current) |
| O-TL-09 | Has the strategy manager previously been involved in products with collateral loss? | No. Zero bad debt across all Steakhouse-curated vaults since inception (January 2024). November 2025 stress: Steakhouse vaults confirmed zero bad debt. Clean 2+ year track record. | 9 | 9 | Non-Improvable (optimal) | [P1] [Steakhouse Docs](https://www.steakhouse.financial/docs/products/steakhouse-financial-products/morpho-vaults) |

**Team & Legal Subtotal: 57.5/67.5 (85.2%)**
- 7 questions scored 9 (sum = 63), 2 questions scored 3 (sum = 6)
- Raw sum = 69 out of max 81
- Weighted = (69/81) x 67.5 = 57.5

---

#### Documentation & Transparency (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-DT-01 | Is there up-to-date documentation explaining architecture, strategy mechanics, and risks? | Yes. Morpho V2 documentation comprehensive and up-to-date. Steakhouse publishes Prime Instant product specifications, vault controls, and risk management docs. V2 architecture (adapters, sentinels, timelocks, forceDeallocate) thoroughly documented. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/), [P1] [Prime Instant](https://www.steakhouse.financial/docs/products/vault-products/current/prime-instant) |
| O-DT-02 | Is it clearly documented how collateral is used and when loss occurs? | Yes. V2 docs explain adapter architecture, forceDeallocate, and cap system. Underlying Morpho Blue docs cover liquidation mechanics, bad debt scenarios, oracle risks. Security considerations page covers V2-specific risks (adapter removal frontrunning, ERC4626 inflation attacks). | 9 | 9 | Non-Improvable (optimal) | [P1] [Security Considerations](https://docs.morpho.org/curate/concepts/security-considerations/), [P1] [Risk Docs](https://docs.morpho.org/learn/resources/risks) |
| O-DT-03 | Are all contract, proxy and implementation addresses documented in one canonical place? | Yes. Morpho V2 contract addresses documented: VaultV2Factory (0xA1D9...), adapter factories, MorphoRegistry (0x3696c5...). The specific vault address (0xbeef0880...) is listed on the Morpho app and Steakhouse product page. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Contracts](https://docs.morpho.org/get-started/resources/contracts/morpho-vaults-v2/), [P1] [Addresses](https://docs.morpho.org/get-started/resources/addresses/) |
| O-DT-04 | Are roles, permissions and timelocks documented with visible change history? | Yes. Comprehensive V2 role documentation: Owner, Curator, Allocator, Sentinel capabilities. Per-function timelock durations documented. Capabilities matrix shows exactly what each role can do. Changes visible via on-chain event logs. | 9 | 9 | Non-Improvable (optimal) | [P1] [Roles & Capabilities](https://docs.morpho.org/curate/concepts/roles/) |
| O-DT-05 | Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities? | Yes. Full real-time on-chain proof-of-reserves. V2 vault adapter allocations visible via V2 API and Etherscan. Underlying V1 vault allocations visible on Morpho App. All positions auditable on-chain at any time. | 9 | 9 | Non-Improvable (optimal) | [P0] [Morpho V2 API](https://api.morpho.org/graphql), [P0] [Etherscan](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51) |
| O-DT-06 | Are all contracts verified on the leading block explorers? | Yes. VaultV2 contract verified on Etherscan (Solidity v0.8.28). Owner DAO proxy verified. Sentinel Revoker contract verified. MetaMorpho adapter verified. MorphoRegistry verified. All source code readable. | 9 | 9 | Non-Improvable (optimal) | [P0] [Etherscan VaultV2](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51#code) |

**Documentation Subtotal: 67.5/67.5 (100.0%)**
- 6 questions, all scored 9
- Raw sum = 54 out of max 54
- Weighted = (54/54) x 67.5 = 67.5

---

#### Financial Resilience (7.5% weight, 67.5 max points)

| Code | Question | Answer Summary | Current | Potential | Classification | Evidence |
|------|----------|----------------|---------|-----------|----------------|----------|
| O-FR-01 | Is there a backstop reserve or safety module for user losses? | Limited. No dedicated safety module or ring-fenced reserve for this vault or for Morpho generally. Bad debt is socialized among lenders within each Morpho Blue market. Morpho DAO treasury exists (~$37.5M per DeFiLlama, predominantly MORPHO tokens) but activation for loss coverage is entirely discretionary. | 3 | 9 | **Improvable** | [P3] [DeFiLlama Treasury](https://api.llama.fi/treasury/morpho), [P1] [Bad Debt Docs](https://docs.morpho.org/curate/tutorials-v1/bad-debt/) |
| O-FR-02 | How large and liquid are the backstop reserves and treasury relative to TVL? | Insufficient. Morpho DAO treasury is approximately $37.5M per DeFiLlama (breakdown: ~$24.9M on Base OwnTokens, ~$12.6M on Ethereum OwnTokens, negligible non-MORPHO holdings). Against protocol-wide TVL of ~$6.8B, this is ~0.55%. Treasury is dominated by MORPHO tokens (volatile native token, no stablecoins). Not ring-fenced for this vault ($32.4M TVL). | 1 | 9 | **Source Missing / Improvable** | [P3] [DeFiLlama](https://api.llama.fi/treasury/morpho) |
| O-FR-03 | What is the estimated operational runway at current burn? | Strong. Morpho raised $73.6M total (most recent: $50M Series C, Aug 2024 led by Ribbit Capital). Nonprofit structure reduces overhead. Curator fees growing. Steakhouse generates revenue from other vaults (e.g., Steakhouse ETH at 5% fee). This V2 vault charges 0% fees. Runway comfortably above 24 months. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/) |
| O-FR-04 | How have TVL, revenue and buffers behaved in past stress events, including composability contagion? | The V2 vault has now operated through the April 2026 KelpDAO/rsETH exploit (~$292M stolen, over $200M in estimated bad debt on Aave, $13.2B total DeFi TVL decline) with zero bad debt -- Steakhouse had <$0.01 exposure and the V2 vault's TVL grew from ~$8M to ~$32M during the broader period. Morpho had only ~$1M exposure across two isolated markets, though the broader Morpho protocol experienced temporary net outflows alongside the DeFi ecosystem. The underlying V1 vault previously demonstrated resilience during November 2025 stress (zero bad debt). Protocol-wide TVL grew from $5B to $13B in 2025 despite stress episodes. The V2 vault token is not widely composed into external protocols, limiting composability contagion risk. | 9 | 9 | Non-Improvable (optimal) | [P1] [Morpho 2025 Review](https://morpho.org/blog/the-morpho-effect-2025/), [P2] [DeFi Markets Update 2026-04-22](https://kitchen.steakhouse.financial/p/defi-markets-update-2026-04-22) |
| O-FR-05 | Can the protocol remain safe in maintenance mode if team disappears? | Yes. Morpho Blue is immutable and runs perpetually. V2 vault contract is immutable. Permissionless withdrawals via ERC4626 + forceDeallocate always available. No proprietary off-chain services required for core operations. Sentinel can veto pending changes. Even without team, users can exit via direct contract calls. | 9 | 9 | Non-Improvable (optimal) | [P1] [V2 Docs](https://docs.morpho.org/learn/concepts/vault-v2/) |

**Financial Resilience Subtotal: 46.5/67.5 (68.9%)**
- 3 questions scored 9 (sum = 27), 1 question scored 3, 1 question scored 1
- Raw sum = 31 out of max 45
- Weighted = (31/45) x 67.5 = 46.5

---

### **Operations Total: 227.75/270 (84.4%)**

| Subcategory | Current | Max | Current % |
|-------------|---------|-----|-----------|
| Governance | 56.25 | 67.5 | 83.3% |
| Team & Legal | 57.5 | 67.5 | 85.2% |
| Documentation | 67.5 | 67.5 | 100.0% |
| Financial Resilience | 46.5 | 67.5 | 68.9% |
| **Operations Total** | **227.75** | **270** | **84.4%** |

---

## Final Score Calculation

| Category | Subcategory | Raw Score | Max Raw | Adj Points | Max Points | Percentage |
|----------|-------------|-----------|---------|------------|------------|------------|
| **Security** | Smart Contract Security (11 Q) | 87 | 99 | 158.2 | 180 | 87.9% |
| | Key Management (8 Q) | 54 | 72 | 135.0 | 180 | 75.0% |
| | **Security Subtotal** | | | **293.2** | **360** | **81.4%** |

| **Strategy** | Protocol Mechanics (9 of 10 Q scored) | 75 | 81 | 41.7 | 45 | 92.6% |
| | Collateral (4 Q) | 28 | 36 | 35.0 | 45 | 77.8% |
| | Infra Counterparty (8 of 11 Q scored) | 60 | 72 | 37.5 | 45 | 83.3% |
| | Protocol Counterparty (5 Q) | 45 | 45 | 45.0 | 45 | 100.0% |
| | Liquidity (9 Q) | 63 | 81 | 35.0 | 45 | 77.8% |
| | Market (5 Q) | 39 | 45 | 39.0 | 45 | 86.7% |
| | **Strategy Subtotal** | | | **233.2** | **270** | **86.4%** |
| **Operations** | Governance (4 Q) | 30 | 36 | 56.25 | 67.5 | 83.3% |
| | Team & Legal (9 Q) | 69 | 81 | 57.5 | 67.5 | 85.2% |
| | Documentation (6 Q) | 54 | 54 | 67.5 | 67.5 | 100.0% |
| | Financial Resilience (5 Q) | 31 | 45 | 46.5 | 67.5 | 68.9% |
| | **Operations Subtotal** | | | **227.75** | **270** | **84.4%** |
| **TOTAL** | | | | **754.1** | **900** | **83.8%** |


---

## Smart Contract Addresses

| Role | Address | Explorer Link |
|------|---------|---------------|
| VaultContract | 0xbeef088055857739C12CD3765F20b7679Def0f51 | [Etherscan](https://etherscan.io/address/0xbeef088055857739C12CD3765F20b7679Def0f51) |
| MorphoBlue | 0xBBBBBBBBbb9cc5e90e3b3Af64bdAF62C37EEFFCb | [Etherscan](https://etherscan.io/address/0xBBBBBBBBbb9cc5e90e3b3Af64bdAF62C37EEFFCb) |
| OwnerDAO | 0xe3Acb3A0cC24C7b176101900715e38E8e789DAd4 | [Etherscan](https://etherscan.io/address/0xe3Acb3A0cC24C7b176101900715e38E8e789DAd4) |
| Sentinel | 0x76303D5Ef2Effb6B489F6d9051e6B409962aB715 | [Etherscan](https://etherscan.io/address/0x76303D5Ef2Effb6B489F6d9051e6B409962aB715) |
| MetaMorphoAdapter | 0xFc98D101F6E2F7C27DB2bAEf7D803298F0e0043C | [Etherscan](https://etherscan.io/address/0xFc98D101F6E2F7C27DB2bAEf7D803298F0e0043C) |
| MarketsV1Adapter | 0x2b9681015A1FA2225D1FC8ae40538d3D64C58290 | [Etherscan](https://etherscan.io/address/0x2b9681015A1FA2225D1FC8ae40538d3D64C58290) |
| UnderlyingV1Vault | 0xBEEF01735c132Ada46AA9aA4c54623cAA92A64CB | [Etherscan](https://etherscan.io/address/0xBEEF01735c132Ada46AA9aA4c54623cAA92A64CB) |
| VaultV2Factory | 0xA1D94F746dEfa1928926b84fB2596c06926C0405 | [Etherscan](https://etherscan.io/address/0xA1D94F746dEfa1928926b84fB2596c06926C0405) |
| MorphoRegistry | 0x3696c5eAe4a7Ffd04Ea163564571E9CD8Ed9364e | [Etherscan](https://etherscan.io/address/0x3696c5eAe4a7Ffd04Ea163564571E9CD8Ed9364e) |

