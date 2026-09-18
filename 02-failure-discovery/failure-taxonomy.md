# Ascend IQ Failure Taxonomy

## Top 3 Prioritized Failures

| Rank | Failure Type | Trust Tag | Frequency | Severity | Business Impact |
|---|---|---|---|---|---|
| 1 | Unsupported or incorrect factual claims | #HALLUCINATION | 6/20 (30%) — HIGH | P0 | Can cause enterprise users to make strategic decisions based on false, stale, or unsupported market intelligence, directly undermining trust and increasing churn risk. |
| 2 | Failure to use available evidence | #ROBUSTNESS | 1/20 (5%) — LOW | P1 | Makes Ascend IQ appear unreliable even when the correct answer exists in the source, reducing confidence in the assistant as a dependable research tool. |
| 3 | Failure to follow response or brand constraints | #UX_TRUST | 1/20 (5%) — LOW | P1 | Off-brand or unprofessional responses can weaken trust in a premium enterprise product and make the experience feel unsuitable for senior decision-makers. |

## #1 Risk — Business Impact

This failure matters because Ascend IQ can present unsupported or incorrect claims as fact, which can lead enterprise customers to make decisions based on bad market intelligence, eroding trust and increasing churn risk.

## Defending the Prioritization

- Unsupported or incorrect factual claims are the most frequent confirmed failure in the audit: **6 of 20 cases (30%)**.
- This failure directly violates our primary trust metric, **Hallucination Rate**, and undermines the core product promise of reliable, decision-ready intelligence.
- For Fortune 500 strategy users, confident factual errors can affect pricing, competitive, and market decisions, creating materially higher business risk than tone or formatting failures.

## Taxonomy Notes

### Unsupported or Incorrect Factual Claims
Ascend IQ states information that is unsupported by, stale relative to, or contradictory to the available evidence.

Examples observed:
- Using an outdated Enterprise price and inventing a seat minimum.
- Treating a tentative speaker as confirmed.
- Misrepresenting API rate limits.
- Treating an engineering hub as a headquarters.

### Failure to Use Available Evidence
The correct answer is present in the source, but Ascend IQ fails to identify or use it.

Example observed:
- SOC2 Type II certification is visible in the source, but Ascend IQ says it cannot find compliance information.

### Failure to Follow Response or Brand Constraints
The response may not be factually wrong, but it violates explicit experience, style, or brand requirements.

Example observed:
- A cold email uses slang such as "killer" and "game changer" despite the brand requirement to sound confident, professional, and expert.
