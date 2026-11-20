# SSV Network — Security Research Workspace

Status: **initial reconnaissance / source triage**  
Program: [SSV Network on Immunefi](https://immunefi.com/bug-bounty/ssvnetwork/)  
Target repository: [ssvlabs/ssv-network](https://github.com/ssvlabs/ssv-network)  
Research branch: `audit/ssv-network-research`

## Purpose

This directory records the SSV Network bug-bounty rules, known-issue exclusions, source-version observations, and initial audit hypotheses. It is separate from the Base Everest research notes already in this repository.

## Current status

- Program scope and reward rules transcribed from the supplied Immunefi program text.
- Seven known-issue entries recorded for exclusion screening.
- Initial source comparison identified a mainnet hotfix affecting `SSVClusters` and `SSVValidators`.
- Initial review areas: operator accounting lifecycle, staking/reward accounting, and EB/liquidation state transitions.
- **No vulnerability is confirmed.**
- **No local tests, static-analysis run, or PoC have been executed as part of this SSV review yet.**
- No deployed contract or public testnet has been tested.

## Version baseline

| Reference | Commit / evidence | Notes |
|---|---|---|
| SSV repository `main` | `27c9d572ae974d5865f34821286e7eee099c492c` | Repository baseline observed during initialization. |
| `deploy/v2.0.0-mainnet` | `f6d3cceec3f03fc023309a73d3b08e152fb1824e` | v2.0.0 deployment branch observed during initialization. |
| Mainnet deployment | Block `24912723`, 2026-04-19 | Recorded in official deployment attestation. |
| Mainnet module hotfix | 2026-05-06 attestation | Replaces SSVClusters and SSVValidators module pointers; details in `SOURCE_TRIAGE.md`. |

The source branch and the deployed implementation must not be treated as interchangeable. Confirm deployed bytecode / implementation pointers against the official deployment records before asserting that a code path is live.

## Files

- `PROGRAM_SCOPE.md` — rewards, eligibility, impacts, prohibited testing and disclosure rules.
- `KNOWN_ISSUES.md` — known issues that must not be resubmitted without a materially different impact or vector.
- `SOURCE_TRIAGE.md` — revision and hotfix observations.
- `HYPOTHESES.md` — unconfirmed research queue and current disposition.
- `AUDIT_LOG.md` — dated progress and validation status.

## Safety / handling

Use local source and local forks only. Do not test deployed mainnet or public-testnet contracts, third-party oracles, or third-party smart contracts. Do not publish vulnerability details without express authorization under the program's Responsible Publication rules. Keep any future PoCs deterministic, self-contained, and limited to local test environments.
