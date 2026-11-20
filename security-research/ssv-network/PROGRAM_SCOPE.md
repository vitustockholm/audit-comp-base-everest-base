# SSV Network — Immunefi Program Scope

Source: program text supplied in the research conversation; verify against the live [Immunefi scope](https://immunefi.com/bug-bounty/ssvnetwork/scope/) and [program information](https://immunefi.com/bug-bounty/ssvnetwork/information/) before submission.

## Rewards — Smart Contract

| Severity | Reward |
|---|---:|
| Critical | 10% of directly affected mainnet funds; minimum $50,000, maximum $250,000 |
| High | Flat $30,000 |
| Medium | Flat $10,000 |
| Low | Flat $1,500 |

All four Smart Contract severities are under Primacy of Impact.

Critical reward valuation is determined at report submission time. Repeatable smart-contract attacks are reward-eligible only for the initial attack vector, including for upgradable, pausable, or killable contracts.

## Payment and aggregate cap

- Rewards are denominated in USD and settled exclusively in SSV.
- Conversion uses the average market price reported by CoinMarketCap and CoinGecko at the precise report-submission time.
- No liquidity or slippage adjustment is made.
- Aggregate program pool cap: 150,000 SSV. Actual payout cannot exceed the remaining SSV balance in the program treasury.
- Rewards are administered by the SSV Network Grants Committee.
- KYC (government ID and current proof of address) is required only after a report is confirmed valid and before payout processing.

## Eligibility and exclusions

- Functional PoC is mandatory for every severity.
- Issues already identified in published audits, documented on docs.ssv.network, or documented in any branch of the specified repository are ineligible.
- Public disclosure is prohibited without express authorization from the SSV DAO Grants Committee.
- Responsible Publication: Category 3 — Approval Required.
- Primacy of Impact applies to Smart Contract Critical, High, Medium, and Low. Project-owned assets outside the explicit asset list may qualify only when the relevant impact is in scope. Testnet and mock files are not covered by Primacy of Impact.
- Other projects operated by the same team are not automatically covered.

## Impacts in scope (recorded from the supplied program text)

Confirm the exact live impact table before submitting. The previously reviewed scope listed:

- Critical: direct theft of user funds (excluding unclaimed yield); permanent freezing of funds; protocol insolvency.
- High: theft of unclaimed yield; permanent freezing of unclaimed yield; temporary freezing of funds.
- Medium: block stuffing; griefing causing damage; theft of gas.
- Low: contract fails to deliver promised returns without loss of value.

## Prohibited activities

- Any testing on mainnet or public-testnet deployed code; testing must use local forks of mainnet or public testnet.
- Any testing with pricing oracles or third-party smart contracts.
- Phishing or social engineering against employees or customers.
- Testing third-party systems, applications, or websites.
- Denial-of-service attacks against project assets.
- Automated testing that generates significant service traffic.
- Public disclosure of an unpatched vulnerability during an embargo.
- Any other activities prohibited by Immunefi Rules.

## Research operating constraints

1. Source review and PoCs must run locally.
2. No transaction may be sent to a deployed SSV contract.
3. Do not interact with external price oracles or third-party smart contracts during testing.
4. Do not publish exploit details or PoCs publicly without written approval.
5. Re-check the live program page, audits, docs, and all repository branches before submission.
