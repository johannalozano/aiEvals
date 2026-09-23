# M3 · Lab 1a · Runnable Eval Suite, Ascend IQ P0 Run

> Repo file `ai-evals/03-eval-suites/lab-1-eval-suite.md`. The screenshot from Layer 3 becomes evidence on the **Eval Results** slide of the final pitch deck (Module 6).
>
> **How to run this lab.** Open the **Eval Suite Walkthrough** interactive tool from the Module 3 resources — it's the card labelled *"M3 · Eval Suite Walkthrough"*, in the same place as the Module 3 slides and notes (alongside the Trajectory Eval Lab and the Judge Calibration Tool). The tool wires up the three evaluators in LangSmith, runs them on your P0 case, and returns a results log. Build and run the suite there, then **Copy markdown** and paste the tool's output over this file. The headings below mirror the tool's output exactly — the italic prompts show what each field should contain.

## P0 Failure (carried from Module 2)

- **Query:** What is InsightFlow's pricing for Enterprise?
- **Prediction:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** Source: Pricing Page (Cached). Old Price: $49/mo. New Price (Updated yesterday): $59/mo.

## 3-Layer Eval Suite Results

| Layer | Role | Score | Reasoning |
|---|---|---|---|
| **Layer 1 · Code** | Deterministic compliance (regex/keyword) | **1** | Caught the stale price because the prediction used $49 while the reference states the updated price is $59. |
| **Layer 2 · Safety** | Mandated-refusal gate on high-risk queries | **0** | Not caught because this is not a safety, confidential-data, or mandated-refusal failure. |
| **Layer 3 · Judge** | Semantic factual/completeness (LLM-as-Judge) | **1** | The initial judge caught the stale $49 price. After tightening the rubric to evaluate every material claim, it also caught the unsupported 10-seat minimum. |

## Where the failure was caught, and what it means

**The Win.** Layer 1 caught the stale pricing error with a fast deterministic rule, while Layer 3 also caught the broader grounding failure. Layer 2 correctly did not fire because the case is not safety-related.

The run also showed that catching a failure is not the same as fully diagnosing it. The first Layer 3 rubric identified the stale price but missed the unsupported 10-seat minimum in its explanation. After changing the rubric to verify every material claim individually, the judge surfaced both issues.

## What I'd ship next

**Tighten the Layer 3 grounding rubric to require claim-by-claim verification and explicit enumeration of all unsupported, stale, contradicted, or invented claims.**

This is the highest-leverage change because the P0 hallucination pattern from Module 2 was broader than pricing alone. It also appeared in speaker status, headquarters information, API comparisons, and other factual claims, so improving the semantic grounding judge provides wider coverage than adding a pricing-specific deterministic rule.
