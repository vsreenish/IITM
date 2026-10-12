# AI-RAG · Week 13 — Activity: The Tool-Design Clinic

> **Mandatory hands-on · ~30–40 min · fully offline (no API key).**
> Tool design is ~80% of agent reliability. Six tool definitions are broken —
> each violates exactly one of the four principles. Diagnose each, and be able to
> state the fix. This is the highest-leverage skill of the week.

The four principles: **naming · schema · description · idempotency**
(reference: `docs/tool_design_principles.md`).

---

## Part 1 — Diagnose the six broken tools

For each case: show it, decide which principle it breaks, then check yourself.

```bash
python3 scripts/tool_clinic.py list           # overview of all six
python3 scripts/tool_clinic.py run C1          # C1's full definition + symptom
python3 scripts/tool_clinic.py grade C1 naming # check your answer → reveals why + fix
```

Stuck? The linter checks a tool against all four principles and shows which fails:

```bash
python3 scripts/tool_clinic.py lint C1
```

**Fill in this table as you go** (this is your submission):

| Case | Symptom (one line) | Principle it breaks | Why | The fix |
|------|--------------------|---------------------|-----|---------|
| C1 | | | | |
| C2 | | | | |
| C3 | | | | |
| C4 | | | | |
| C5 | | | | |
| C6 | | | | |

## Part 2 — See what "good" looks like

```bash
python3 scripts/tool_clinic.py lint good       # the 3 reference tools — all four principles pass
```

Note *why* each reference tool passes — you'll copy these habits into your own tools.

## Part 3 — Apply it to your capstone

Pick **one** tool you'll build for your capstone agent (e.g. `query_sql`,
`search_web`, or your own). Write its definition to the four-principle standard:

- **name** — a specific verb (`snake_case`)
- **schema** — a typed Pydantic model, required fields + defaults
- **description** — model-facing, says *when to use* and *when not to*
- **idempotency** — declared (and, if it has side effects, marked non-idempotent)

Then run it past the mental linter: would `tool_clinic.py`'s four checks pass?
Write 2–3 sentences on the one principle you had to think hardest about.

---

## What to submit

1. The completed **six-row diagnosis table** (Part 1).
2. Your **one capstone tool definition** to standard (Part 3) + the 2–3 sentence note.

## Done when…

- [ ] All six cases graded correct with `tool_clinic.py grade`.
- [ ] You ran `lint good` and can say why the reference tools pass.
- [ ] You wrote one capstone tool to the four-principle standard.

*Why this matters:* in Lab Step 2 you'll measure tool-selection accuracy on the
real model. Nearly every point of accuracy you gain there comes from applying
exactly these four principles — so getting them into your hands now pays off
immediately.
