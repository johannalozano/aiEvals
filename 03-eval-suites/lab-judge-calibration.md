# Lab, Judge Calibration (Ascend IQ grounding rubric)

> Repo file `ai-evals/03-eval-suites/lab-judge-calibration.md`. Extra practice (async). Label the 12 Ascend IQ grounding traces, compute κ, and revise the rubric until **κ ≥ 0.60**.
>
> Fill this with the **Judge Calibration** tool, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

**Cohen's κ:** **1.00** (perfect agreement) — **PASSES the κ ≥ 0.60 gate**

- Traces labeled: **12/12**
- Raw agreement p₀: **100%**
- Chance agreement pₑ: **55.6%**
- Disagreements: **0**

### Confusion matrix (judge × you)

| | You: PASS | You: FAIL |
|---|---|---|
| **Judge: PASS** | **8** | **0** |
| **Judge: FAIL** | **0** | **4** |

## Diagnosis

Before the rubric revision, the judge was too lenient toward confident or complete-looking answers that contained unsupported factual claims, and too strict toward grounded answers that correctly expressed uncertainty when the retrieved source did not contain the answer.

Examples of the first pattern included unsupported claims about annual renewal, SLA penalty figures, integrations, and volume discounts. The judge also incorrectly failed answers that appropriately said the retrieved data did not contain enough information to identify the CSM or contract renewal date.

The original judge was therefore rewarding confidence and completeness more than factual grounding.

## Rubric revision

Revise the grounding rubric so that a response **FAILS if any material factual claim is unsupported, stale, contradicted, or invented relative to the retrieved source**.

Explicitly state that a response should **PASS when it correctly says the retrieved source does not contain enough information and avoids inventing an answer**.

Do not reward confidence, completeness, length, or polish when grounding is missing.

Add a one-shot fail example:

> **Question:** Does the plan auto-renew annually?  
> **Answer:** Yes, it renews annually.  
> **Retrieved source:** No renewal clause is present.  
> **Verdict:** FAIL  
> **Reason:** The answer asserts a factual claim that is not supported by the retrieved source.

After applying this revision and re-measuring the same 12 calibration traces, the judge achieved **100% raw agreement and Cohen's κ = 1.00**, with **zero disagreements**.
