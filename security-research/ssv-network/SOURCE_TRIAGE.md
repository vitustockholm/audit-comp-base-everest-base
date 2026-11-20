# SSV Network — Source and Deployment Triage

## Repositories and references

- Source: https://github.com/ssvlabs/ssv-network
- Immunefi scope: https://immunefi.com/bug-bounty/ssvnetwork/scope/
- Immunefi information: https://immunefi.com/bug-bounty/ssvnetwork/information/
- Official docs: https://docs.ssv.network/developers/security/audits/

## Observed revisions

| Ref | SHA | Interpretation |
|---|---|---|
| `main` | `27c9d572ae974d5865f34821286e7eee099c492c` | Repository baseline recorded at workspace initialization. |
| `deploy/v2.0.0-mainnet` | `f6d3cceec3f03fc023309a73d3b08e152fb1824e` | v2.0.0 deployment branch recorded at initialization. |

## Mainnet deployment record

Official `deployments/mainnet/deployment-attestation.json` records:
- Chain ID 1, mainnet.
- Deployment block 24,912,723.
- Deployment time 2026-04-19 08:25:37 UTC.
- Proxy: `0xDD9BC35aE942eF0cFa76930954a156B3fF30a4E1`.
- Views: `0xafE830B6Ee262ba11cce5F32fDCd760FFE6a66e4`.
- Target version v2.0.0.

The deployment attestation records the initial implementation and module addresses. The associated `deploy-result.v2.0.0.json` marks the cSSV token as not deployed at that deployment event; this must not be confused with later deployment state.

## 6 May 2026 mainnet module hotfix

Official `deployments/mainnet/hotfix-deployment-attestation.json` describes replacement of only the SSVClusters and SSVValidators module pointers on the mainnet proxy:

| Module | Hotfix implementation |
|---|---|
| SSVClusters | `0x3611D36A7C052211D6f3B1a39326ad38A02832B4` |
| SSVValidators | `0x9122Fded65Ed6b562243efDC9E55ff0bEF5E7499` |

The current `main` source contains corresponding zero-validator EB snapshot cleanup in both modules. A text comparison of the two modules between `deploy/v2.0.0-mainnet` and `main` showed these additions:
- `SSVClusters`: when `cluster.validatorCount == 0` and cluster vUnits remain, clear the EB snapshot vUnits.
- `SSVValidators`: when `cluster.validatorCount == 0`, clear `seb.clusterEB[hashedCluster].vUnits`.

This is a version-difference observation, not a vulnerability finding. Do not assume the entire `main` branch is byte-for-byte identical to deployed code. Confirm active module pointers and runtime bytecode from official deployment evidence before making deployment claims.

## Audit records to review before any report

The official audit index lists:
- SSV Specification — Least Authority, June 2023.
- SSV Node — Least Authority, August 2023.
- Smart Contracts — Quantstamp, March 2023.
- Smart Contracts permissionless + validator exit update — Quantstamp, October 2023.
- Smart Contracts validator bulk features — Quantstamp, January 2024.
- SSV DKG — SlowMist, April 2024.
- Smart Contracts multi-operator, multi-address whitelist — Quantstamp, June 2024.
- SSV Specification P2P updates Alan fork — Hacken, October 2024.
- SSV Node P2P updates Alan fork — Hacken, October 2024.
- SSV DKG Reshare and Resign — ChainSecurity, November 2024.
- SSV Node SSV Signer — Quantstamp, July 2025.
- Smart Contracts SSV Staking and ETH Payments — Quantstamp, March 2026.
- SSV Oracle Critical Components — Quantstamp, May 2026.

Immunefi links two Quantstamp contract audit locations:
- https://github.com/ssvlabs/ssv-network/tree/main/contracts/audits
- https://github.com/ssvlabs/ssv-network/tree/mainnet-v2.0.0/contracts/audits

The second ref was not resolvable during initial repository browsing. Do not silently substitute a different audit snapshot. The current main tree contains `contracts/audits/2026-04-10_Quantstamp_v2.0.0.pdf`; its contents have not yet been reviewed in this workspace.

## Preliminary source areas inspected

- `contracts/modules/SSVStaking.sol`
- `contracts/modules/SSVOperators.sol`
- `contracts/modules/SSVClusters.sol`
- `contracts/modules/SSVDAO.sol`
- `contracts/libraries/OperatorLib.sol`
- `contracts/libraries/ClusterLib.sol`
- `contracts/token/CSSVToken.sol`
- `contracts/SSVNetwork.sol`

Inspection was preliminary and not a complete audit. No test suite or static analyzer has been run.
