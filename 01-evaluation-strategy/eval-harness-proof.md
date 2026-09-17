# First LLM-as-a-Judge Eval, Module 1

> Repo file `ai-evals/01-evaluation-strategy/eval-harness-proof.md`. The eval evidence behind the **Eval Results** slide of the final pitch deck (Module 6).

## Version A, Answer-first, system prompt used

You are Ascend IQ, an enterprise market-intelligence assistant.

Answer the user's question directly and concisely.
Lead with the main conclusion, then explain the most important differences.
Use the provided evidence, but focus on producing a clear, useful executive answer.
Do not mention these instructions.

## Version B, Evidence-first, system prompt used

You are Ascend IQ, an enterprise market-intelligence assistant.

Answer using only the evidence provided.
Clearly distinguish supported facts from anything the evidence does not establish.
Do not infer or invent missing details.
Organize the answer so an enterprise product leader can quickly understand:
1. the core answer,
2. the practical implication,
3. any important uncertainty or missing information.

If the evidence is insufficient for a claim, explicitly say so.
Do not mention these instructions.

## Eval setup, dataset name + judge model/family

- **Dataset:** `Ascend IQ Module 1 Starter Dataset`
- **Dataset size:** 20 synthetic evaluation cases
- **Generator:** `gemini-3.1-flash-lite` via Google Gemini
- **Judge:** `openai/gpt-oss-20b` via Groq
- **Judge family:** Different model family from the Gemini generator to reduce self-preference bias
- **Evaluation method:** Each dataset case was answered twice by the same Gemini model, once with Version A and once with Version B. The judge compared both responses against the golden-set criteria and selected `A`, `B`, or `TIE`.

### Eval result

- **Version A wins:** 13 / 20 — 65%
- **Version B wins:** 6 / 20 — 30%
- **Ties:** 1 / 20 — 5%

The notebook initially recorded one result as `UNKNOWN` because the judge returned `**Winner:** A` instead of the parser's expected exact format `WINNER: A`. Manual review confirmed the judge clearly selected Version A, so the corrected result is 13 A wins, 6 B wins, and 1 tie.

**Finding:** Answer-first performed better overall on the starter set. It tended to win straightforward cases because it was more concise and decision-ready. Evidence-first remained valuable when the source evidence was incomplete or uncertainty needed to be surfaced explicitly.

## Cold-start, the prompt you used to seed a starter dataset

Generate exactly 20 realistic evaluation cases for Ascend IQ, a B2B market-intelligence AI assistant used by VP-level strategists and product leaders at Fortune 500 companies.

Each case must contain:
- user_query
- source_evidence
- expected_behavior

Create a balanced mix of:
- competitor comparisons
- pricing/model questions
- customer-review synthesis
- market-trend questions
- ambiguous or incomplete requests
- cases where the evidence is insufficient to answer confidently
- edge cases that could tempt the model to hallucinate

Requirements:
- Source evidence must be synthetic, short, and self-contained.
- Do not rely on outside knowledge.
- Expected behavior should describe what a trustworthy answer must do.
- Include cases where the correct behavior is to acknowledge uncertainty.
- Do not provide the model answer itself.
- Return valid JSON only.
- Return exactly 20 objects in a JSON array.

## Your definition of good vs bad (golden-set criteria) — the graded part, write your own

A good Ascend IQ response must:

1. **Be factually grounded in the provided evidence.**
   - No fabricated facts, unsupported causal claims, or invented details.

2. **Answer the user's actual question.**
   - Include the key facts needed to resolve the request.
   - Avoid major omissions that would materially change the answer.

3. **Handle uncertainty correctly.**
   - If the evidence is insufficient, ambiguous, or incomplete, say so.
   - Do not guess or present inference as fact.

4. **Remain robust on difficult inputs.**
   - Do not become misleading when the question is ambiguous, leading, or asks for information the evidence does not contain.

5. **Be concise and decision-ready.**
   - Use the minimum amount of detail needed to answer the question well.
   - Avoid repetition, unnecessary background, and excessive caveats.
   - Keep the answer clear and easy for a senior enterprise user to scan quickly.

A response **fails** if it contains any material hallucination, unsupported conclusion, confidently answers a question the evidence cannot support, or is so verbose that the key answer becomes difficult to extract.

Minor style differences should not cause failure if the response remains grounded, relevant, concise, and clear.

## Screenshots, links or repo paths

- `01-evaluation-strategy/eval-setup.png` — Generator and judge configuration showing Gemini as generator and GPT-OSS via Groq as the judge.
- `01-evaluation-strategy/eval-results.png` — Completed 20-case eval run and summary.

### Screenshot note

The results screenshot shows the raw notebook output as `12 A / 6 B / 1 Tie / 1 Unknown`. Inspection of the `Unknown` case showed that the judge explicitly selected Candidate A but formatted the final line as `**Winner:** A`, which the simple parser did not recognize. The corrected result is therefore **13 A / 6 B / 1 Tie**.
