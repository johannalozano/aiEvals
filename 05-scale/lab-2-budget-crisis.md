# Lab 2, Ascend IQ Budget Crisis

> Repo file `ai-evals/05-scale/lab-2-budget-crisis.md`. Allocate Level 1/2/3 coverage across the 5 failure modes under the **$200K/quarter cap** with **max 3 at Level 3**.
>
> Fill this with the **Budget Crisis Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

**Quarterly budget cap:** $200,000  
**Total Level 3 spend:** **$150,000 (2 of max 3 L3 slots used)**

## Portfolio decision grid

| Failure | Trust metric | Risk | Level | Cost |
|---|---|---|---|---|
| Data Fabrication | Hallucination Rate | P0 | **L3** | **$85,000** |
| Context Specificity | UX Trust | P1 | **L2** | **$7,000** |
| Source Attribution Failure | Robustness | P1 | **L3** | **$65,000** |
| Data Bias | Fairness | P2 | **L1** | **$2,750** |
| Cost Overruns | Latency | P3 | **L1** | **$1,250** |

**Total quarterly portfolio spend:** **$161,000 / $200,000**

_Reference L3 costs: Hallucination $85K · Context $70K · Attribution $65K · Bias $55K · Latency $25K. L2 ≈ 10% of L3, L1 ≈ 5% of L3._

## Fallback methods (non-Level 3 items)

### L2 · Context Specificity (UX Trust · P1)
- **Method:** Run a weekly audit of sampled Ascend IQ responses, checking whether the answer follows the user's requested scope, emphasis, and constraints rather than merely being generally correct.
- **Why this fallback is defensible:** Context-specificity failures can reduce usefulness and contribute to churn, but they are less catastrophic than fabricated facts or broken source attribution. A weekly audit should surface recurring patterns quickly enough without the cost of continuous Level 3 monitoring.

### L1 · Data Bias (Fairness · P2)
- **Method:** Run manual spot-checks on deploy, with targeted review across geographic or user segments if a complaint, anomaly, or skew signal appears.
- **Why this fallback is defensible:** Bias is currently an accepted lower-priority gap for Ascend IQ, and we do not yet have evidence of systematic disparity. Lightweight spot-checks are proportionate for the current risk, with escalation if a credible disparity signal appears.

### L1 · Cost Overruns (Latency · P3)
- **Method:** Use simple automated threshold checks on deploy for p95 latency and cost/token spikes, with manual spot-checks when usage patterns or model configuration change.
- **Why this fallback is defensible:** Latency and cost are operationally important but lower-severity than hallucination or attribution failures. They were already treated as warn-only in Module 4, so lightweight threshold checks are sufficient to catch obvious regressions without continuous Level 3 coverage.
