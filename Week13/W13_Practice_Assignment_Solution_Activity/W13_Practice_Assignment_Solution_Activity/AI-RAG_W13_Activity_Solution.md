# AI-RAG · Week 13 — Activity Solution (Instructor)
## The Tool-Design Clinic — answer key + rubric

Generated live from `scripts/tool_clinic.py answers`. Learners can self-check with
`grade`, so this is for grading Part 3 and confirming the diagnosis table.

---

## Part 1 — the six diagnoses

| Case | Title | Principle | Why | Fix |
|------|-------|-----------|-----|-----|
| **C1** | The tool called `data` | **naming** | `data` is a noun, not an action — tells the model nothing about what it does. | Rename to a specific verb phrase (e.g. `get_weather`, `fetch_exchange_rate`). |
| **C2** | The loose schema | **schema** | Parameters are untyped, so the model can't tell what input shape is expected → runtime arg errors. | Type every parameter, mark required, give optionals defaults (Pydantic). |
| **C3** | The silent description | **description** | "Gets the status." says nothing about *when* to use the tool or what it returns. | Write a model-facing description with a clear "use this when…" and the return. |
| **C4** | The unsafe retry | **idempotency** | Sends a message (a side effect) but is marked idempotent, so the loop retries freely → double-send. | Mark non-idempotent, note the side effect, add a dedupe key before retrying. |
| **C5** | The overloaded `handle` | **naming** | `handle` is vague and the tool does three jobs; the model can't reason about it. | Split into single-purpose tools, each with a specific verb name. |
| **C6** | The catch-all description | **description** | Claims it answers *any* question, so the model reaches for it by default, crowding out better tools. | Scope the description to exactly what it does; say what NOT to use it for. |

Note the two pairs: **naming** appears twice (a bad *name* C1, and an *overloaded*
tool C5), and **description** appears twice (a *silent* one C3, and an *over-broad*
one C6). Accept the principle as correct even if a learner's wording differs, as
long as the reasoning matches.

## Part 1 — grading (out of 6)

One point per correctly-diagnosed case. Because `tool_clinic.py grade` reveals the
answer, focus grading on the **"why"** column — a learner who wrote a sensible
reason understood it; one who only copied the principle word did not.

- **6/6** — all correct with coherent reasons → full marks.
- **4–5/6** — minor slips (usually C5 naming-vs-description, or C6 description-vs-naming).
- **≤3/6** — send back to `docs/tool_design_principles.md`; they'll struggle with
  Lab Step 2 otherwise.

## Part 3 — grading the capstone tool (holistic)

Check the learner's one tool against the four principles:

| Principle | Looking for |
|---|---|
| naming | a specific verb, `snake_case`, not overloaded |
| schema | typed Pydantic, required + defaults (not a single free-form string) |
| description | model-facing, includes "use this when…" and ideally "do NOT use it for…" |
| idempotency | declared; side-effecting tools marked `idempotent=False` |

**Strong (full marks):** passes all four *and* the 2–3 sentence note shows real
judgment (e.g. "I marked `create_ticket` non-idempotent and added a dedupe key,
because a retry after a timeout would otherwise open two tickets").

**Weak:** a single-string schema, a human-oriented description with no "when to
use," or idempotency not considered. Point to the specific principle; this is
formative, so don't over-penalise — the point is the habit.

## Quick check

Every reference tool passes all four principles, and every broken tool fails its
designated one — enforced by the test suite (`tests/test_clinic.py`) and
`smoke_test.sh`:

```bash
python3 scripts/tool_clinic.py answers    # this key
python3 scripts/tool_clinic.py lint good  # references — all four pass
```
