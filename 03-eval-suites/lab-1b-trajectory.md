# Lab, Trajectory Eval (Ascend IQ usage-drop task)

> Repo file `ai-evals/03-eval-suites/lab-1b-trajectory.md`. Grade the agent's **path**, not just the final answer.

**Matching mode:** unordered  
**Score:** 1/6 · **Verdict:** HOLD

## Dimension scores

| Dimension | Score | Note |
|---|---|---|
| Tool selection | FAIL | Skipped `get_ingestion_status` and `compare_weeks`, and added an off-scope `search_web` step. |
| Argument correctness | PASS | The arguments used in the tools it did call were appropriate, including the correct account ID and 4-week usage window. |
| No redundant / looping steps | FAIL | Repeated the same `get_usage` call with identical arguments and gained no new information. |
| Recovery | FAIL | The agent did not notice or correct the bad path after the redundant call and off-scope web search. |
| Plan coherence | FAIL | The investigation drifted away from the required diagnostic path and moved to a generic seasonal explanation before verifying the account data. |
| Task completion | FAIL | It did not check for an ingestion gap or perform the week-over-week comparison, so the cause was not actually verified. |

## Verdict

**HOLD** — the final reply sounds plausible, but the trajectory failed almost every important path-quality dimension. The agent skipped two critical diagnostic steps, did not recover from its errors, and gave an unverified explanation for the usage drop. A convincing final answer does not compensate for an unreliable path.
