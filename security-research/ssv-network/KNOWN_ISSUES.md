# SSV Network — Known-Issue Exclusion Register

This register transcribes the known-issue descriptions supplied for the SSV Immunefi program. These entries are **not candidate findings**. A future report must demonstrate a materially different root cause, attack vector, or impact and must still pass the program's audit/docs/all-branches exclusion.

## KI-001 — Liquidations between root commitments / EB drift

Committed EB roots are point-in-time snapshots. Removing validators changes on-chain validator count immediately, but a still-valid root can retain higher EB until a fresh root is committed and consumed. A subsequent `updateClusterBalance` can increase fees/liquidation threshold and trigger liquidation if the owner withdrew close to the threshold.

Do not report the documented stale-root → validator removal → aggressive withdrawal → root consumption → liquidation sequence as-is.

## KI-002 — Removed-operator frozen fee indices

`removeOperator()` settles accrued earnings and resets active operator state, but intentionally preserves `snapshot.index` and `ethSnapshot.index`. Cluster accounting continues to include these frozen indices to preserve unsettled earnings.

Do not report preserved indices alone.

## KI-003 — Permissionless 1-wei deposit changes cluster snapshot

Cluster operations accept caller-supplied cluster state. A permissionless deposit, including 1 wei, changes the cluster state and can make one pending owner operation revert with stale data. The documented trade-off is retryable and does not itself cause permanent loss.

Do not report the documented one-shot stale-cluster grief alone.

## KI-004 — Theoretical uint64 operator / cluster accounting overflow

Fee accounting uses uint64 arithmetic. Program simulations under current limits (including 3,000 validators per operator and current fee bounds) report no overflow under realistic conditions, including an extreme long-unwithdrawn scenario.

Do not report theoretical overflow without proving a reachable current state and an in-scope impact.

## KI-005 — ETH cluster insolvency depends on liquidator liveness

Pending fees may reduce the effective cluster balance to zero, and liquidation checks execute when an actor calls `liquidate` or an applicable update path. There is no autonomous background transaction.

Do not report the documented dependency on off-chain liquidator/updater liveness alone.

## KI-006 — Shared first-come operator validator capacity

The 3,000 ETH-validator capacity per operator is shared and permissionless for public operators. An actor may occupy remaining capacity, blocking new registrations and potentially legacy migration/reactivation. The program describes the cost, liquidation release, operator privatization, and legacy-cluster exit paths as reasons this is accepted.

Do not report shared capacity exhaustion or the documented migration/reactivation limitation alone.

## KI-007 — Operator fee increase ceiling division

`declareOperatorFee` uses ceiling division, which may allow one additional raw fee unit (100,000 wei per block) above an exact percentage limit. The absolute `operatorMaxFee` cap is still enforced, and the new fee is public during the declaration period.

Do not report the documented one-unit rounding effect alone.

## Exclusion rule

The program additionally excludes vulnerabilities already identified in audit reports, docs.ssv.network, or any branch of the specified repository, whether or not they appear in this short register. This file is not a substitute for checking those sources.
