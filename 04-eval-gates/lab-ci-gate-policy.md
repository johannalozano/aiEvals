# Lab, CI Eval Gate Policy (Ascend IQ PR #218)

| Dimension | main | PR | Δ | Floor | Max reg | Blocking | Result |
| --- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Faithfulness (grounding) | 96 | 87 | -9 | 90 | 3 | yes | ✕ FAIL |
| Task completion | 92 | 93 | +1 | 85 | 5 | yes | ✓ PASS |
| Tool selection | 90 | 88 | -2 | 85 | 3 | yes | ✓ PASS |
| Safety / policy | 99 | 99 | 0 | 98 | 1 | yes | ✓ PASS |
| Latency (p95) | 84 | 80 | -4 | 75 | 6 | no | ✓ PASS |
| Cost per task | 88 | 82 | -6 | 80 | 8 | no | ✓ PASS |

**Gate result:** ⛔ **BLOCKED** — a required blocking dimension regressed past policy.

## Merge decision

**BLOCK merge** — Faithfulness regressed from **96 to 87**, a **9-point drop**. This falls below the **90 floor** and exceeds the allowed **3-point maximum regression** on a blocking P0 dimension.

The developer should revisit the retrieval-prompt change, correct the grounding regression, and rerun the same deterministic 30-case golden-set replay before the PR can merge.

Task completion, tool selection, and safety remain within policy. Latency and cost are warn-only dimensions and do not block the merge.

---
_Generated for M4 CI Gate Policy · Ascend IQ PR #218._
