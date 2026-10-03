# Ship/Hold Memo · Ascend IQ

> Repo file `ai-evals/06-culture/lab-1-ship-hold-memo.md`. A Pyramid-Principle executive memo: the recommendation comes **first**.
>
> Fill this with the **Ship/Hold Memo Builder**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

> **Decision:** 🛑 HOLD

**To:** CPO · cc Eng Lead · Trust & Safety  
**From:** Group Product Manager · AI Evals Cohort · October 3, 2026

## The Answer

**HOLD Ascend IQ from production launch until the P0 faithfulness and hallucination gates are back within threshold, because the current regression creates unacceptable trust risk for enterprise customers.**

## The Arguments

### 1. Reliability risk

Ascend IQ's core promise is trustworthy market intelligence, but the current system still produces unsupported or incorrect factual claims. That makes the product unreliable in exactly the situations where enterprise users depend on it for pricing, competitive, and product decisions.

### 2. Revenue and trust risk

If enterprise customers act on incorrect intelligence, the cost is bigger than a bad answer. It can erode confidence in Ascend Analytics, increase churn risk, and weaken the credibility of a premium product that customers expect to be dependable.

### 3. Eval readiness

The evaluation system is now mature enough to detect these failures consistently through calibrated judging, regression gates, and launch thresholds. The problem is no longer whether we can measure quality; it is that Ascend IQ has not yet met the quality bar we defined.

## Evidence · Trust Metrics

```text
- Hallucination rate: 30% (6/20 cases) (Gate: ≤2%) FAIL · Source: M2 Failure Taxonomy / M3 Eval Spec
- Faithfulness: 87, down from 96 on main (-9 pts) (Gate: floor ≥90; max regression 3 pts) FAIL · Source: M4 CI Gate Policy
- Judge calibration: Cohen's κ = 1.00, 100% agreement across 12/12 cases (Gate: κ ≥0.60) PASS · Source: M3 Judge Calibration
- Hallucination coverage: Level 3 continuous monitoring, $85K/Q (Risk: P0) · Source: M5 Budget Crisis
```

The evaluator is calibrated well enough to trust the signal; the product itself is still failing the core trust gate.

## Business Risk

Shipping now would expose at least **$2.5M in annual enterprise contract value** across the planned top-50-account launch cohort to a product that is still failing its core factual-grounding gate.

Holding delays the launch window, but limits the risk of trust erosion, churn, and credibility damage while the P0 regression is corrected.

## Next Step · Decision Needed

**Approve the HOLD and require the retrieval-prompt regression to be corrected, then rerun the 30-case deterministic replay and P0 grounding suite before reconsidering launch. Reassess the ship decision within two weeks.**

## Reflection

Defining "good enough" forced me to separate what feels acceptable from what is actually measurable and defensible. The biggest realization was that a product can sound strong while still failing a trust threshold that should block launch.
