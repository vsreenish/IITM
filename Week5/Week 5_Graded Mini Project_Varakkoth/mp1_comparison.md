# MP1 · Comparison Table

*Generated from a live run on 2026-08-16 19:19. Model: `gpt-4o-mini` · Judge: `gpt-4o` · temperature=0.0 · 10 snippets x 4 strategies = 40 calls.*

## Headline metrics by strategy

| strategy   |   Accuracy (of 3) |   Accuracy rate |   Parse rate |   Judge score |   Latency p50 (s) |   Mean out-tokens |   Total cost (cents) |
|:-----------|------------------:|----------------:|-------------:|--------------:|------------------:|------------------:|---------------------:|
| few_shot   |               2.8 |           0.933 |            1 |           4   |              0.65 |              25.6 |               0.0684 |
| cot        |               2.7 |           0.9   |            1 |           3.9 |              1.92 |             170.4 |               0.1263 |
| structured |               2.7 |           0.9   |            1 |           3.9 |              0.9  |              30.5 |               0.0491 |
| zero_shot  |               2.7 |           0.9   |            1 |           3.9 |              1.16 |              34.5 |               0.0374 |

## Per-field accuracy (share of 10 snippets correct)

| strategy   |   company |   role |   years_experience_required |
|:-----------|----------:|-------:|----------------------------:|
| few_shot   |       0.8 |      1 |                         1   |
| cot        |       0.8 |      1 |                         0.9 |
| structured |       0.8 |      1 |                         0.9 |
| zero_shot  |       0.8 |      1 |                         0.9 |

## Strict vs lenient accuracy

| strategy   |   Strict accuracy |   Lenient accuracy |   Punctuation artifact |
|:-----------|------------------:|-------------------:|-----------------------:|
| few_shot   |               2.8 |                3   |                    0.2 |
| cot        |               2.7 |                2.9 |                    0.2 |
| structured |               2.7 |                2.9 |                    0.2 |
| zero_shot  |               2.7 |                2.9 |                    0.2 |

*Lenient scoring ignores trailing punctuation. The gap is measurement error, not model error.*

## Spend

- Worker calls (40 x `gpt-4o-mini`): **$0.0028**
- Judge calls (`gpt-4o`): **$0.0236**
- Total: **$0.0264**

## Column notes

- **Accuracy (of 3)** — mean count of exactly-matching fields per snippet (0-3).
- **Accuracy rate** — the same figure divided by 3, as a 0-1 rate.
- **Parse rate** — share of responses from which a JSON object could be recovered.
- **Judge score** — mean `gpt-4o` rubric score, 1-4.
- **Latency p50** — median wall-clock seconds per call, measured inside the concurrency semaphore (queue wait excluded).
- **Total cost** — worker-call spend only; judge spend is listed separately above.
