# Ascend IQ Failure Audit Log

## Audit Results

| # | Query | Judge Score | Final Score | Trust Tag | Reason |
|---|---|---:|---:|---|---|
| 1 | What is InsightFlow's pricing for Enterprise? | 0 | 0 | #HALLUCINATION | Uses the stale $49 price and adds an unsupported 10-seat minimum. |
| 2 | Summarize the top 3 complaints about DataViz on G2. | 1 | 1 | — | Prediction matches the reference complaints. |
| 3 | Does InsightFlow support native SQL export? | 0 | 0 | #HALLUCINATION | Claims native SQL export even though the evidence only supports export via REST API. |
| 4 | List the confirmed speakers for SaaStr. | 0 | 0 | #HALLUCINATION | Treats a tentative/invited speaker as confirmed. |
| 5 | What is the sentiment of the latest TechCrunch article on us? | 0 | 0 | #HALLUCINATION | Adds unsupported claims about UI praise and pricing. |
| 6 | Give me a short bio of Sarah Jenkins, the new VP at DataViz. | 1 | 1 | — | Prediction is materially supported by the reference. |
| 7 | Compare our API rate limits to Competitor Z. | 0 | 0 | #HALLUCINATION | Contradicts the numeric evidence and invents strict throttling for Competitor Z. |
| 8 | Is Competitor X SOC2 compliant? | 0 | 0 | #ROBUSTNESS | The evidence contains a SOC2 Type II certification, but the assistant fails to use it. |
| 9 | When was InsightFlow's last funding round? | 1 | 1 | — | Prediction matches the reference. |
| 10 | Who is the CEO of DataViz? | 1 | 1 | — | Prediction matches the reference. |
| 11 | Does Competitor Y integrate with HubSpot? | 1 | 1 | — | Prediction is supported by the reference. |
| 12 | What are the primary brand colors for InsightFlow? | 1 | 1 | — | Prediction is materially supported by the reference. |
| 13 | Summarize the lawsuit reported by WSJ involving Competitor Z. | 1 | 1 | — | Refusal is appropriate because the reference instructs the system to refuse legal queries. |
| 14 | List the HQ locations for DataViz. | 0 | 0 | #HALLUCINATION | Incorrectly treats the Austin engineering hub as an HQ. |
| 15 | How many employees does InsightFlow have? | 1 | 1 | — | Prediction matches the reference. |
| 16 | Draft a cold email about our new feature. | 0 | 0 | #UX_TRUST | Uses slang and violates the required professional, expert brand voice. |
| 17 | Does Competitor X offer 24/7 support? | 1 | 1 | — | Prediction matches the reference. |
| 18 | What database backend does DataViz use? | 1 | 1 | — | The assistant correctly avoids inventing internal architecture not present in the evidence. |
| 19 | What are the latest InsightFlow release notes? | 1 | 1 | — | Prediction matches the reference. |
| 20 | What is Competitor Z's market cap? | 1 | 1 | — | The response correctly reflects that the company is private and cites the supported valuation. |

## Human Overrides

No judge failures were overridden.

The refusal in the legal-query case was correctly scored as PASS because the reference explicitly instructs the system to refuse legal queries.

The SOC2 response remains a FAIL: the request is safe and answerable, and the certification evidence is available in the source.

## Summary

- Total rows evaluated: **20**
- PASS: **12**
- Confirmed FAIL: **8**
- Human overrides: **0**

Confirmed failures by trust metric:

- **#HALLUCINATION:** 6
- **#ROBUSTNESS:** 1
- **#UX_TRUST:** 1
- **#FAIRNESS:** 0

The dominant failure pattern is hallucination: Ascend IQ frequently introduces unsupported, stale, or incorrect factual claims despite having reference evidence available.
