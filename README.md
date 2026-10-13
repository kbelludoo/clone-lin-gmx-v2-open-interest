# clone-lin-gmx-v2-open-interest

Experimental LIN clone of GMX V2 `applyDeltaToOpenInterest` (uint64-scale unsigned open interest + signed long-flipped virtual inventory).

- **Upstream:** [gmx-io/gmx-synthetics](https://github.com/gmx-io/gmx-synthetics) `contracts/market/MarketUtils.sol` commit `a85ea3491c19c93bb4b5a002d9b358fb769b7849` (GPL-2.0-or-later after BUSL Change Date 2026-08-31).
- **LIN kernel:** [`src/lin_gmx_v2_open_interest.lin`](src/lin_gmx_v2_open_interest.lin)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/gmx_v2_open_interest/` and `python3 test/prove_gmx_v2_open_interest_external.py`
- **Class:** EXPERIMENTAL. Not Arbitrum GMX V2 uint256. Not a production replacement. Not `applyDeltaToPositionImpactPool` (pool/lent) and not `applyDeltaToOpenInterestInTokens` (VI iff the tokens flag).

Named goldens (uint64-scale, oi=1e8 vi=5e7): long +3e7 → oi **130000000** / vi **20000000** vs no-flip **80000000**; short +3e7 → vi **80000000** vs always-flip **20000000**; neg OI -1.5e8 **rejects** vs naive **-50000000** vs bounded floor **0**; tokens flag leaves vi **50000000** vs tokens-sibling **20000000**; long +5e7 on vi 2e7 is signed **-30000000** vs unsigned floor **0**; 7e18+3e18 fail-closes vs naive i64 wrap **-8446744073709551616**.
