# Lab 1, Ascend Analytics Coverage Matrix

> Repo file `ai-evals/05-scale/lab-1-coverage-matrix.md`. Feeds the **Coverage / scale** slide of the final pitch deck (Module 6).
>
> Fill this with the **Coverage Matrix Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly. **Force ≥2 ❌ gaps** — an all-green matrix isn't real.

**Product:** AI-Powered Report Summaries

## Coverage row

| Product | Hallucination | Bias | Latency | Toxicity | Drift Monitoring |
|---|---|---|---|---|---|
| AI-Powered Report Summaries | ✅ | ❌ | ✅ | ⚠️ | ❌ |

## Method + Ground Truth (two ✅/⚠️ cells)

### Hallucination Rate
- **Method:** Run claim-by-claim grounding evaluation against retrieved source evidence using deterministic checks where possible and a calibrated LLM-as-a-Judge for semantic claims.
- **Ground truth:** The verified retrieved source or reference used for each eval case.

### Latency
- **Method:** Measure p95 response latency across the deterministic regression replay and compare it against the defined latency floor and allowed regression limit.
- **Ground truth:** Response-time measurements from the regression golden set, evaluated against the agreed SLA / performance threshold.

## Strategic acceptance

**Accepted gap:** Bias / Fairness

> We are accepting this gap for now because we do not currently have evidence of group-specific disparity, and fairness was not one of the prioritized trust metrics for Ascend IQ.  
>
> **Kill criterion:** If we receive a credible complaint or detect an internal signal showing materially different answer quality across a user or company segment, we stop accepting this gap and build a dedicated fairness evaluation.

## Critical mitigation

- **Critical gap:** Drift Monitoring
- **Why critical:** A model can pass launch evals and still degrade over time as data, prompts, retrieval behavior, or usage patterns change. Without drift monitoring, quality could deteriorate in production without being detected quickly.
- **Mitigation plan:** Ascend IQ Product Lead and AI Engineering will add a recurring production drift evaluation that samples live Ascend IQ interactions, scores key trust dimensions against the launch baseline, and triggers review when performance exceeds agreed regression limits. Monitoring will run **weekly**, with a formal **monthly review**.
