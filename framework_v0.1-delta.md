# SR Ratings DeFi Risk - Question Framework

| Version | Release Date |
|---|---|
| **v0.1-delta** | 13.11.2026 |

## Security

### Smart Contract Security

**Whats the risk of an on-chain protocol exploit?**

- Have all core contracts that hold or route funds been independently audited?
- Who performed the most recent audit and what is their reputation tier?
- Have upgrades to core contracts been followed by new audits?
- Have all critical and high-severity audit findings been fully remediated and re-verified?
- Are core contracts upgradeable and how tightly are upgrades constrained?
- Has any on-chain exploit or critical bug affecting user funds occurred, were affected users compensated and were post-mortems published?
- Has any confirmed rug-pull event occurred?
- Has any timelock protecting upgrade or fund-custody paths been reduced or removed in the last 12 months?
- Does the protocol run an active bug-bounty via a reputable platform (e.g. Immunefi, Code4rena)?
- Are real-time security monitoring and alerting systems in place?
- Are automatic safety controls (e.g. pause, circuit breakers) triggered by monitoring alerts?
- Has the deployed configuration of fund-critical infrastructure (bridge verifier set, oracle sources and parameters, access-control and permission assignments) been independently reviewed, and does the live configuration match the reviewed or documented state?

### Key Management & Permissions

**What is the risk of an off-chain protocol exploit?**

- Who controls admin and upgrade keys for (proxy-) contracts holding user funds and have previous changes been documented?
- Can any single key move user funds or upgrade custody contracts?
- Are the signers of critical multisigs independent of each other, and is the signer set managed transparently?
- How constrained are pause and freeze permissions: who can trigger them, over what scope, and for how long?
- Are all user assets, and the assets backing them, held in non-custodial smart contracts?
- Are user funds fully segregated from treasury and operational wallets?
- Which protocols, venues, staking modules or operators can user funds be routed to, and how is that set enforced?
- Can any role block, freeze, seize or force-transfer the funds of individual addresses, and how is that power constrained?
- Who can change risk parameters that affect user funds (collateral listings, LTVs and liquidation thresholds, supply/borrow or allocation caps, fees, oracle sources, staking-module or venue limits), and how constrained is that power?

## Strategy

### Protocol Mechanics

**How likely does the yield source goes negative?**

- What are the sources of yield aligned with the mandate of the vault or protocol?
- Under which conditions does net yield become negative or cause loss?
- Is leverage or rehypothecation used and up to what effective level?
- Are there automated mechanics to prevent Liquidation Events (health rate, LTV thresholds)
- Has this strategy or a close variant ever experienced negative yield?
- Is a risk framework documented for the vault's curation or, where there is no curator, for the protocol's own mechanics (parameter limits, caps, change control)?
- Is current yield sustainable relative to underlying economics?
- Can the position be fully or mostly unwound under conservative liquidity assumptions without slippage, penalties, or lockups turning expected yield negative?
- Does the strategy rely on a spread, peg, or funding rate that can invert (e.g. basis trades, stablecoin pegs, LST discounts, market making)?
- Can automated or externally-invocable mechanisms increase the product's exposure without real-time human approval?

### Collateral

**How likely is a collateral depeg?**

- Which assets are accepted as collateral and how are they risk rated?
- How did each collateral behave versus its underlying during past stress or depegs?
- How concentrated is exposure to any single collateral or LST?
- How is validator or slashing risk handled for staking-based collaterals?
- What share of TVL relies on bridged or wrapped assets, and how robust is the bridge security?

### Infra Counterparty Exposures

**How likely does a malfunction of counterparty Chain, Bridge, Oracle, Wallet, Validators, APIs, Frontends or CEX affect the principal?**

- Which chains, bridges, oracles, wallets and CEXs does the strategy depend on and how are they risk rated or tiered?
- How redundant are oracle and bridge setups, and can oracle values be corrected under abnormal conditions?
- Are off-chain infrastructure providers certified by standard IT security audits like SOC 2 or ISO27001 or VSP?
- How did these infra components behave in past outages or chain incidents?
- Has the base chain recently halted block production, experienced consensus failure or become non-operational?
- Has the validator set experienced slashing events that could impact staked collateral?
- Are the validators the product itself stakes with diverse geographically and by operator?
- Can any single infra component failure alone block withdrawals or cause losses?
- How robust is the cross-chain messaging or bridge verification setup?
- Are rate limits or circuit breakers enforced on cross-chain escrow releases or minting?
- Is the off-chain verification infrastructure resilient to data-source manipulation?
- Does the chain the product runs on carry sequencer, forced-exit or finality risk?

### Protocol Counterparty Exposures

**How likely does a malfunction of counterparty protocol affect the collateral?**

- Into which external protocols, CEXs or RWA platforms is collateral deployed and how are they risk rated?
- Are revenue-share or incentive arrangements documented and do they create conflicts of interest?
- Are there hard limits and rebalancing rules per counterparty?
- How quickly and safely can positions be unwound from each counterparty?
- Are third-party validators, custody providers or asset managers disclosed?

### Liquidity

**How likely is it that 100% of the collateral can be withdrawn within the stated withdrawal period?**

- How are withdrawals executed and are they enforced permissionlessly on-chain or can they be paused, queued or delayed?
- Is there enough liquidity and market depth to redeem close to 100% of TVL within the stated withdrawal time, under normal conditions?
- Have there been past withdrawal delays queues or freezes and does the avg processing time match expectations?
- Do caps or limits restrict timely redemptions during high utilization?
- How does exit liquidity behave during volatility and network congestion?
- What share of assets cannot realistically exit within the stated withdrawal terms, whatever the mechanism (unstaking, vesting, bridge exits, queues, or utilisation of a lending market)?
- Does redemption depend on secondary-market liquidity and is it sufficient?
- What is the liquidity depth of collateral and receipt tokens?
- What is the risk of bank-run scenarios under full utilization?

### Market

**What happens in a market black-swan event or high market volatility?**

- How has the LST or receipt token peg performed under market stress?
- How likely can adverse moves in broader crypto markets cause permanent losses due to directional exposure?
- Are interest rate/incentive models robust during TVL shifts or volatility spikes?
- How much could depositors lose in historic high-volatility market moves, and is that loss bounded?
- Can sharp price moves trigger forced liquidations that crystallize losses before positions can be adjusted?

## Operations

### Governance

**How likely can governance changes or capture cause losses or block withdrawals?**

- What governance model controls protocol changes and upgrades?
- How concentrated is voting power among top holders and delegates, and can a single address or a small coalition pass a proposal alone?
- Are mechanisms in place to limit major changes in scope and time like timelocks and veto or delays?
- Can the protocol replace the strategy manager without blocking user withdrawals and how is this governed?

### Team & Legal & Compliance

**How robust is the team and legal setup in protecting my collateral from fraud or seizure?**

- Are core team and operating entities publicly identified and credible?
- Is the protocol dependent on a single developer or a small team, and does this ensure optimal management for the strategy?
- What legal entity and jurisdiction operate the protocol and/or assets at the rating date?
- Are there known investigations or regulatory actions related to the entity?
- Is there an on-call and incident response process for the core team and, where one exists, the strategy manager?
- Does the team provide timely support for critical user or integrator issues?
- Are major investors or strategic partners disclosed?
- Does the strategy manager run other mandates or venues that create a conflict of interest for this vault?
- Has the strategy manager previously been involved in products with collateral loss or materially adverse curation decisions?
- Has the curator, or in a lending market its delegated risk manager, shown the ability to keep the product within its stated mandate, including under stress?

### Documentation & Transparency

**How clearly does the protocol explain what happens to my collateral and when I could lose it?**

- Is there up-to-date documentation explaining architecture, strategy mechanics, and risks?
- Is it clearly documented how collateral is used and when loss occurs?
- Are all contract, proxy and implementation addresses documented in one canonical place and verified on-chain?
- Are roles, permissions and timelocks documented with a visible change history?
- Does the protocol publish proof-of-reserves and where applicable proof-of-liabilities?
- Are all contracts verified on the leading block explorers?

### Financial Resilience

**How likely can the protocol absorb shocks without passing permanent losses to depositors?**

- Is there backstop reserve or safety module for user losses and is there any guarantee it will be used in a loss event?
- Is there a funded layer that absorbs losses before depositors, and has it paid when it was needed?
- What is the estimated operational runway at current burn for operational teams and managers?
- How have TVL, revenue and buffers behaved in past stress events, including composability contagion?
- Can the protocol remain safe in maintenance mode if team disappears?
