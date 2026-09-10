# Capstone Corpus Design — Northwind Ltd EKA

**Sreenish Varakkoth · AI-RAG Capstone · Milestone 1**

An authored corpus for the Northwind Ltd Enterprise Knowledge Assistant.
Northwind is fictional; the corpus is written, not collected, so that every
retrieval failure mode in it is deliberate and its location is known in advance.

Conformance to `Milestones/Capstone Milestone 1.md` is tracked in Section 6.

---

## 1. Why an authored corpus

The corpus has to satisfy one non-negotiable condition: **the model must not be
able to answer the golden set without retrieval.** If it can, the RAG-vs-no-RAG
ablation shows no lift and the pipeline becomes unmeasurable. Public documents
published before the model's training cutoff fail this test. An authored corpus
passes it by construction, and trivially satisfies the milestone's "approved for
project use" rights requirement.

Authoring buys a second thing that collected corpora cannot give: control over
*where the hard cases are*. Each defect below is planted at a known location, so
when a retrieval technique fixes it, the improvement is attributable rather than
coincidental.

## 2. The constraint that shapes everything: 8 cross-document questions

The milestone golden set is 8 easy (single-document) / 8 medium (cross-document
synthesis) / 4 hard (escalation and refusal). **Forty percent of the evaluation
requires two or more documents.** Cross-document capability is not a stretch goal
here; it is the median case.

A corpus written first and questioned afterwards cannot support that. The
split-fact pairs below are therefore designed *before* the documents are written,
and each is authored deliberately: the fact is placed in one document, and the
document that would naturally also carry it explicitly defers to the first.

| # | Question theme | Fact A | Fact B |
|---|---|---|---|
| X1 | Paid parental leave | Eligibility + duration — `hr-leave-policy.md` | Pay rate — `hr-benefits.md` |
| X2 | New joiner equipment | Device standard — `it-device-endpoint.md` | Issue timing + approver — `hr-onboarding.md` |
| X3 | Working remotely from abroad | Eligibility + duration cap — `hr-remote-work.md` | Insurance + notification — `ops-travel-v2.md` |
| X4 | Claiming a conference | Spend approval threshold — `ops-procurement.md` | Claim window + receipts — `ops-expenses.md` |
| X5 | On-call compensation | Rota + eligibility — `it-oncall.md` | Allowance rate — `hr-benefits.md` |
| X6 | Contractor system access | Contractor status — `hr-leave-policy.md` §7 | Non-employee provisioning — `it-access-control.md` |
| X7 | Promotion and salary review | Rating scale + cycle — `hr-performance-review.md` | Bands + effective date — `hr-benefits.md` |
| X8 | Personal-data incident | Severity + escalation path — `it-oncall.md` | Breach notification window — `it-data-retention.md` |

Note that `hr-benefits.md` is Fact B in three pairs. That is intentional: a
single document that many questions must reach, but that no question is *about*,
is the hardest kind of chunk for naive top-k to surface.

## 3. Planted defect register

Every defect maps to the week whose technique is expected to address it. This
register is the spine of the final writeup.

| # | Defect | Location | Technique expected to fix it |
|---|---|---|---|
| D1 | Vocabulary mismatch — corpus says "remote working arrangements", questions ask "WFH" | `hr-remote-work.md` | Dense embeddings (W6) vs. keyword baseline |
| D2 | Distractor — "30 days" is both a resignation notice period and an expense claim window | `hr-leave-policy.md`, `ops-expenses.md` | Top-k precision; reranking (W9) |
| D3 | Needle — one eligibility threshold buried mid-document | `it-oncall.md` (1,231 words) | Chunk-size sweep (W6 assignment) |
| D4 | Cross-document — the eight pairs in Section 2 | throughout | Multi-hop / query decomposition (W9-W10) |
| D5 | Superseded — travel policy v1 (2024) and v2 (2026) both present | `ops-travel-v1.md`, `ops-travel-v2.md` | Metadata filtering on `effective_date` (W8) |
| D6 | Table-only fact — mileage rates exist solely in a markdown table | `ops-travel-v2.md` | Chunking that respects table boundaries (W6) |
| D7 | Hub document — `hr-benefits.md` is required by 3 questions but is the topic of none | `hr-benefits.md` | Retrieval recall; query rewriting (W9) |

Two conditions are deliberately *absent* so that refusal questions have somewhere
to land: Northwind has no sabbatical scheme and no stated position on
cryptocurrency payments. A third, the absence of a leave-appeal process, is the
basis of the escalation question.

## 4. Document manifest

Sixteen documents across three topic clusters, mirroring the three support
channels the milestone scenario names — HR teams, IT helpdesk, and managers /
operational guidance. Every cluster carries at least five documents, and every
document falls inside the 500–3,000 word band.

Lengths are deliberately uneven. A corpus of uniformly sized documents produces
a flat chunk-size sweep and hides the optimum.

### Cluster 1 — HR & People (6 documents)

| File | Type | Words | Version | Carries |
|---|---|---|---|---|
| `hr-leave-policy.md` | policy | 906 | 2.0 | D2, X1, X6 |
| `hr-benefits.md` | reference | 923 | 2.1 | D7, X1, X5, X7 |
| `hr-remote-work.md` | policy | 830 | 1.2 | D1, X3 |
| `hr-onboarding.md` | procedure | 724 | 1.1 | X2 |
| `hr-performance-review.md` | procedure | 752 | 2.0 | X7 |
| `hr-hiring-process.md` | procedure | 1,335 | 1.4 | — |

### Cluster 2 — IT & Technical (5 documents)

| File | Type | Words | Version | Carries |
|---|---|---|---|---|
| `it-oncall.md` | procedure | 1,231 | 2.3 | D3, X5, X8 |
| `it-access-control.md` | policy | 780 | 1.5 | X6 |
| `it-device-endpoint.md` | policy | 812 | 1.3 | X2 |
| `it-software-requests.md` | procedure | 747 | 1.0 | — |
| `it-data-retention.md` | policy | 932 | 2.0 | X8 |

### Cluster 3 — Operations & Finance (5 documents)

| File | Type | Words | Version | Carries |
|---|---|---|---|---|
| `ops-expenses.md` | policy | 811 | 3.2 | D2, X4 |
| `ops-travel-v2.md` | policy | 854 | 2.0 | D5, D6, X3 |
| `ops-travel-v1.md` | policy | 642 | 1.0 (superseded) | D5 |
| `ops-procurement.md` | procedure | 682 | 1.0 | X4 |
| `ops-facilities.md` | reference | 638 | 1.1 | — |

Total 13,599 words, written and verified. At 800-character chunks with overlap,
roughly 110–140 chunks — enough that top-k selection is a real problem, small
enough that a full re-embed costs about two cents and runs in under a minute.

Word counts in the tables above are actual, measured after writing, not targets.

Frontmatter on every document, carried into the Qdrant payload from W7 and used
as filter predicates in W8: `title`, `category`, `doc_type`, `version`,
`effective_date`, `owner`.

## 5. Golden set

Twenty questions in `data/golden_set_full.jsonl`, to the milestone's difficulty
split.

| Difficulty | Count | Content |
|---|---|---|
| Easy | 8 | Single-document factual. Answer lives in one chunk. Primary precision metric. |
| Medium | 8 | The eight split-fact pairs X1–X8 from Section 2. |
| Hard | 4 | 3 refusals (sabbatical, crypto payments, personal legal advice) + 1 superseded trap on D5, which *is* answerable from v2. |

That gives 17 answerable questions against the milestone's minimum of 16.

The milestone's required schema is `id`, `question`, `ideal_answer`, `tags`. Two
fields are added:

```json
{
  "id": "q07",
  "question": "How much notice do I have to give before resigning?",
  "ideal_answer": "30 calendar days below director level, 90 days at director level and above.",
  "tags": ["HR", "Leave", "Easy"],
  "difficulty": "easy",
  "expected_sources": ["hr-leave-policy#3"]
}
```

`expected_sources` is the important addition. It makes retrieval measurable
independently of generation — recall@k can be computed without an LLM in the
loop. Without it, a wrong answer cannot be attributed to retrieval or to the
model, and the whole evaluation collapses into one undiagnosable number.

## 6. Milestone conformance

| Requirement | Target | This design |
|---|---|---|
| Documents | 10–30 | 16 |
| Words per document | 500–3,000 | 638–1,335 |
| Documents per major topic | ≥5 | 6 / 5 / 5 |
| Rights status | approved for project use | authored — no restriction |
| Golden set total | 20 | 20 |
| Answerable | ≥16 | 17 |
| Hard questions | 4 | 4 |
| Human verification | mandatory | authored and verified by hand |

## 7. Authoring rules

1. **Facts, not prose.** Numbers, thresholds, eligibility rules, named roles,
   dates. Narrative paragraphs produce questions with no verifiable answer.
2. **Write the split-fact pairs first.** For each pair in Section 2, place Fact A,
   then have the second document explicitly defer — "the rate of pay is set out
   in the Benefits reference document". The deferral is what makes the question
   answerable only by retrieving both.
3. **Consistent facts across documents, except where a defect requires
   otherwise.** Unintentional contradictions make the golden set unfalsifiable.
4. **Heading structure throughout.** Section headers are the natural chunk
   boundary and the basis for the structural-chunking comparison.
5. **No document restates another** except D5's superseded pair. Accidental
   near-duplicates create ties in retrieval indistinguishable from real failures.
6. **Record every fact used in the golden set** in the registers above as it is
   written, not afterwards from memory.
