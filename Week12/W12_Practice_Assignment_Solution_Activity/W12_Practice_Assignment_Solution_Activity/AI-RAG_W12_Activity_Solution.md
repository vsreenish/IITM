# Week 12 Activity — Solution Key

Full diagnoses for the six drill scenarios. (Instructors: the same key is printed
by `python3 scripts/debug_drill.py answers`.)

| # | Bucket | Trace evidence | Root cause | Smallest fix |
|---|---|---|---|---|
| **S1** | Retrieval (recall) | `retrieve` shows only the `-a` chunk; the `-b` (2nd hop) chunk is absent, distractors fill top-K | A required chunk for a multi-hop answer never reached the top-K | Raise top-K / add query expansion for multi-hop questions |
| **S2** | Retrieval (precision) | `retrieve`/`rerank` top chunk_ids are `kb-*` distractors with high scores; the relevant chunk is gone | Distractors outranked the correct chunk, so generation had only noise | Retune hybrid weight / reranker, or reduce chunk size |
| **S3** | Generation | `retrieve`/`rerank` healthy (correct `-a`/`-b`, good scores) but the answer adds a "150%" claim in no chunk | Hallucination — model asserted a fact absent from the context | Lower temperature; tighten the grounding constraint (leave retrieval alone) |
| **S4** | Prompt | `prompt` shows `has_grounding_instruction: false`; answer tacks on a "#general Slack" step not in policy | The prompt template lost its "answer only from context" line | Restore the grounding instruction; pin the template version |
| **S5** | Infra | `cache` shows `cache_hit: true`, `cached_for_question: g003`; retrieve/generate skipped; answer is about working hours | Stale cache — a hit returned a different question's answer (key collision / not invalidated) | Fix the cache key / invalidate stale entries (W10 tombstone + `kb_version`) |
| **S6** | Infra | `generate` marked ✗ with `error: timeout after 30000ms` and a 30000ms latency | Generation call timed out with no retry | Add retry-with-backoff and a timeout budget; check API health |

## Teaching points

- **S3 vs S1/S2** is the key discrimination: all three give a "wrong answer," but
  S3 has *healthy retrieval*. If the chunks are right and the answer is wrong,
  it's generation — not retrieval. Reading the trace makes this obvious; guessing
  does not.
- **S4 looks like generation** but the cause is upstream in the prompt. The tell
  is `has_grounding_instruction: false`. Fixing the model (temperature) would not
  help; fixing the prompt does.
- **S5 looks like generation** (fluent, wrong) but nothing after `cache` even ran.
  Always check whether a cache hit short-circuited the pipeline before blaming
  retrieval or the model.
- **Verify matters:** each fix is only done once `pytest eval/` is green with no
  other KPI regressing.

## Rubric for the Activity (out of the six)

- **Pass (≥ 4/6 correct + evidence):** classifies most scenarios correctly and can
  point to the trace evidence.
- **Strong (6/6 + fixes + own-system writeup):** all six correct with the smallest
  fix each, plus a `wk12-debug-trace.md` applying the workflow to their own
  lowest-scoring golden question. This is DR #2-ready.
