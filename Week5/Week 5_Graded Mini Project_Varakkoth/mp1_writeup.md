# MP1 · Reflection

**Sreenish Varakkoth · Week 5 Graded Mini Project**
*10 snippets × 4 strategies = 40 `gpt-4o-mini` calls, temperature 0, judged by `gpt-4o`. Full tables in `mp1_comparison.md`.*

---

## 1. Which strategy performed best?

| | few_shot | structured | zero_shot | cot |
|---|---|---|---|---|
| Accuracy (of 3) | **2.8** | 2.7 | 2.7 | 2.7 |
| Lenient accuracy | **3.0** | 2.9 | 2.9 | 2.9 |
| Judge score (1–4) | **4.0** | 3.9 | 3.9 | 3.9 |
| Parse rate | 1.00 | 1.00 | 1.00 | 1.00 |
| Latency p50 (s) | **0.65** | 0.90 | 1.16 | 1.92 |
| Cost (cents / 10 snippets) | 0.068 | 0.049 | **0.037** | 0.126 |

**Few-shot**, on every quality measure and on speed — fastest despite the largest prompt, because latency tracks *output* length, and its examples demonstrate a compact answer format rather than describing one (25.6 output tokens vs 34.5 for zero-shot).

The margin is thin: `role` scores 1.00 and `company` 0.80 for *every* strategy, so the entire difference between the four rests on one snippet.

## 2. Failure patterns

**The `0`/`null` boundary (j05) — the only genuine model error in the run.** j05 reads *"fresh grads welcome — no prior experience required"*; gold is `0`. Only few-shot returned `0`; the other three returned `null`. The distinction is a data-modelling one: `null` means no requirement is stated, `0` means the stated requirement is nothing. Our instruction defined only the first case, so a model facing an explicit zero defaulted to absence.

**j10 did not fire.** All four returned `null` correctly; fabrication rate 0.00. Every strategy inherited the same instruction clause — *"or null if no years are stated"* — and that alone defeated the trap. Read together with j05, this is the finding I would carry forward: **an explicit instruction handled absence, but only a worked example handled the boundary between absence and zero.**

**Punctuation (j02, j08) — not a model error.** The model returned `"Northwind Ltd."` against gold `"Northwind Ltd"`, where the snippet's full stop is both a sentence terminator and a plausible abbreviation mark. This hit all four strategies identically, cost 8 of 40 rows, and is exactly the 0.2 strict-vs-lenient gap — measurement error, not model error.

## 3. Cost, latency and the evaluation itself

CoT is the clear loser: **3.4× the cost of zero-shot, 4.9× the output tokens, 3× the latency of few-shot, for zero accuracy gain.** Extracting three fields from three sentences offers no reasoning depth to exploit. Its 1.00 parse rate was engineered, not free — the parser falls back to the last `{...}` span; a naive `json.loads()` would have failed every CoT row.

The judge cost **$0.0236 against $0.0028 for the work it graded — 8.4×** — and scored 3.9–4.0 across all four, too compressed to rank anything. It earned its cost on the 8 punctuation rows, scoring them 4/4 and correctly overruling my exact-match code: the weaker instrument for ranking, the stronger for diagnosis.

## 4. Recommendations

1. **Use few-shot for production extraction**, with examples covering the edge cases — an explicit zero, an unstated field, an abbreviation-final company name. At 0.068 cents per 10 extractions, prompt size is not the constraint.
2. **Specify edge cases in the instruction, then demonstrate them anyway.** j05 shows an under-specified rule failing silently while returning confident, well-formed, wrong output.
3. **Fix the golden set's punctuation convention.** A brittle scorer sends you optimising a prompt that was never broken.
4. **Skip CoT for shallow extraction, and use the judge for diagnosis rather than ranking** — sampling rows rather than judging all 40.

**Caveat:** with 10 snippets one row moves a per-field score by 0.10, and the few-shot win rests on a single snippet. These gaps are directional, not significant. Before committing a strategy to the capstone I would extend the golden set, especially with more `0`/`null` boundary cases.
