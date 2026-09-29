# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Context

Module 4 carries forward the verified failures from the Module 2 Ascend IQ audit. The correct legal-refusal behavior is excluded from gating.

Each verified failure below is assigned:

- a severity: **Advisory · Soft · Hard**
- a pipeline placement: **Pull Request · Staging Build · Release Build**
- a rationale tied to the business impact of that failure

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 01 | Hallucination · Stale Pricing / Unsupported Seat Minimum | **Hard** | **Pull Request** | Incorrect pricing or invented commercial terms can directly mislead enterprise decisions, so regressions should block before merge. |
| 03 | Hallucination · Native SQL Export Falsely Claimed | **Hard** | **Pull Request** | Claiming a product capability that does not exist could affect enterprise workflows or purchasing decisions, so it should block before merge. |
| 04 | Hallucination · Tentative Speaker Presented as Confirmed | **Soft** | **Staging Build** | Overstating tentative information as confirmed is a grounding failure that should be caught before release, but is narrower in impact than pricing or capability misinformation. |
| 05 | Hallucination · Unsupported Sentiment Details | **Soft** | **Staging Build** | Unsupported specifics can distort market intelligence even when the overall sentiment direction is reasonable, so the issue should be caught before release. |
| 07 | Hallucination · Incorrect API-Limit Comparison | **Hard** | **Pull Request** | A false competitive comparison can materially mislead enterprise users making product or vendor decisions, so it should block before merge. |
| 08 | Robustness · Failure to Use Available Evidence | **Soft** | **Staging Build** | Missing evidence that is actually available undermines answer quality and trust, so it should be caught before release without blocking every PR. |
| 14 | Hallucination · HQ vs. Engineering Hub Misclassification | **Advisory** | **Release Build** | The factual distinction matters, but this specific error is lower-impact than pricing, capability, or competitive misinformation, so it should be surfaced and monitored without automatically blocking release. |
| 16 | UX Trust · Brand / Tone Constraint Failure | **Soft** | **Staging Build** | Brand voice is part of Ascend Analytics' premium enterprise experience, so tone violations should be caught before release rather than treated as informational only. |

## Sample Interactions

### Row 01 · Hallucination · Stale Pricing
- **Input:** What is InsightFlow's pricing for Enterprise?
- **Output:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** Old price $49/month; updated price $59/month. No support for a 10-seat minimum.
- **Gate:** Hard · Pull Request

### Row 03 · Hallucination · Native SQL Export
- **Input:** Does the product support native SQL export?
- **Output:** Yes, users can export directly through the native SQL export capability.
- **Reference:** REST API access is available; there is no native export button.
- **Gate:** Hard · Pull Request

### Row 04 · Hallucination · Speaker Status
- **Input:** List the confirmed speakers for SaaStr.
- **Output:** Sam Altman is presented as a confirmed speaker.
- **Reference:** The evidence only indicates invited / tentative status.
- **Gate:** Soft · Staging Build

### Row 05 · Hallucination · Unsupported Sentiment Details
- **Input:** Summarize TechCrunch sentiment.
- **Output:** Adds unsupported claims about UI praise and pricing.
- **Reference:** Evidence supports Neutral / Positive sentiment, but not those additional details.
- **Gate:** Soft · Staging Build

### Row 07 · Hallucination · API Limits
- **Input:** Compare our API rate limits with Competitor Z.
- **Output:** Claims our API is more robust and Competitor Z uses stricter throttling.
- **Reference:** Ascend: 500 rpm. Competitor Z: 1000 rpm.
- **Gate:** Hard · Pull Request

### Row 08 · Robustness · Missed SOC 2 Evidence
- **Input:** Does the evidence show SOC 2 compliance?
- **Output:** Says documentation cannot be found.
- **Reference:** SOC 2 Type II badge is present in the available evidence.
- **Gate:** Soft · Staging Build

### Row 14 · Hallucination · HQ Classification
- **Input:** Where are the company's headquarters?
- **Output:** San Francisco and Austin.
- **Reference:** San Francisco is the HQ; Austin is an Engineering Hub.
- **Gate:** Advisory · Release Build

### Row 16 · UX Trust · Brand Voice
- **Input:** Draft a cold email about our new feature.
- **Output:** Uses language such as "killer" and "game changer."
- **Reference:** Professional expert tone; avoid slang.
- **Gate:** Soft · Staging Build

## Gate Summary

- **Hard:** 3
- **Soft:** 4
- **Advisory:** 1

The map therefore includes at least one gate at each required severity level while reserving Hard blocking behavior for the failures with the clearest potential to materially mislead enterprise decisions.
