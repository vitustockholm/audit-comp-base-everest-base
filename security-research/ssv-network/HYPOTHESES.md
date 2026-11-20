# SSV Network — Initial Hypothesis Queue

All entries are **unconfirmed research hypotheses**, not vulnerability claims. Every item must be checked against the live Immunefi rules, all repository branches, documentation, and audit reports before a PoC or report is considered.

| ID | Area | Initial question | Current status |
|---|---|---|---|
| SSV-001 | EB roots / liquidation | Are there state-transition orderings beyond the documented stale-root / validator-removal sequence that can cause a distinct in-scope impact? | Known-issue screen first; no finding. |
| SSV-002 | Operator lifecycle accounting | Can remove / re-register / re-add / cluster-membership transitions cause an accounting mismatch beyond the documented frozen-index behavior? | Untriaged. |
| SSV-003 | Caller-supplied cluster snapshots | Can stale cluster state cause a persistent or materially more severe failure than the documented single-operation 1-wei grief? | Untriaged; retryability and attacker economics must be demonstrated. |
| SSV-004 | uint64 accounting | Is there a reachable current-parameter state that overflows despite the published simulations and bounds? | Low priority; must establish feasibility before testing. |
| SSV-005 | Staking / cSSV / ETH rewards | Do transfer hooks, reward-index updates, claims, unstaking, or rounding create an independently exploitable accounting discrepancy? | Initial source review only; audit exclusion check pending. |
| SSV-006 | Upgrade / initialization / storage | Do module pointer updates, upgrade initialization, storage layout, or authorization transitions create a reachable unauthorized state? | Untriaged; compare exact deployed version and audit coverage first. |

## Triage gates

1. Identify exact affected code and deployed version.
2. Identify the relevant asset and explicit in-scope impact.
3. Exclude every published known issue, docs item, branch item, and audit finding.
4. Prove attacker capabilities and prerequisites without privileged assumptions excluded by program rules.
5. Reproduce locally with deterministic tests only.
6. Assess severity and funds directly affected; do not infer a bounty from a theoretical condition.
7. Keep PoC and report private until authorized.
