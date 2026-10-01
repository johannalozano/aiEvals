# Module 4 · Launch Strategy · Section 4.0 Release Criteria

_Generated from the M4 Launch Strategy Builder. Drop this into your PRD as Section 4.0._

## 4.0 Release Criteria

The following thresholds must be met by Model Candidate v1.x before approval for production deploy. Eval Specs from Module 3 define the measurement methodology.

| Severity | Metric | Threshold | Dataset | Method |
|---|---|---|---|---|
| 🔴 Hard (Blocker) | Hallucination rate / faithfulness failure rate | **≤ 2%** | `Ascend_IQ_Logs` | `03-eval-suites/lab-2-eval-spec.md` · claim-by-claim grounding evaluation using deterministic checks where applicable plus calibrated LLM-as-a-Judge |
| 🟡 Soft (Review) | Evidence-use failure rate | **≤ 6%** | `Ascend_IQ_Logs` | Evaluate cases where relevant evidence is available in retrieved context and measure how often Ascend IQ fails to use it correctly |
| 🔵 Advisory (Monitor) | Brand-voice violation rate | **≤ 10%** | `Ascend_IQ_Logs` | Evaluate responses against Ascend Analytics' professional enterprise tone and flag slang or off-brand phrasing |

## 4.1 CI Gate Policy

These thresholds run in a GitHub Actions gate on every pull request, replaying deterministic fixtures from the regression golden set (≥ 30 cases). PM owns the policy; Engineering owns the YAML.

**Blocking dimensions:** Faithfulness / grounding, task completion, tool selection, and safety / policy. A pull request is blocked if any blocking dimension falls below its minimum floor or exceeds its maximum allowed regression versus `main`.

**Warn-only dimensions:** Latency (p95) and cost per task. Regressions in these dimensions generate warnings for review but do not automatically block the merge.

Current per-dimension policy:

| Dimension | Floor | Max regression | Blocking |
|---|---:|---:|---|
| Faithfulness / grounding | 90 | 3 pts | Yes |
| Task completion | 85 | 5 pts | Yes |
| Tool selection | 85 | 3 pts | Yes |
| Safety / policy | 98 | 1 pt | Yes |
| Latency (p95) | 75 | 6 pts | No |
| Cost per task | 80 | 8 pts | No |

## 4.2 Mitigation Plan · Soft Gate

**Mitigation lever:** Feature flag

**If our Soft Gate fails because the evidence-use failure rate exceeds 6%, we recommend using a feature flag because it lets us contain the risk without fully blocking launch. We can disable or limit Ascend IQ for affected users or accounts while the retrieval and evidence-use issue is investigated and fixed.**

---

_Lab artifact for Module 4, AI Evals Certification, Product School. Becomes the Eval Gates slide of the Final Project deck._
