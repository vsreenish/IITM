# MP2 · Mini-RAG over Sherlock Holmes

A small retrieval-augmented generation pipeline: the stories in `corpus/` are chunked, embedded with OpenAI, stored in Qdrant, and queried to produce cited answers.

```
corpus/*.txt → chunks → embeddings → Qdrant → retrieve → answer + citations
```

## Setup

1. Install dependencies (Python 3.10+):
   ```bash
   pip install -r requirements.txt
   ```
2. Create a `.env` from the template and fill in your keys:
   ```bash
   cp .env.example .env
   ```
   Required: `OPENAI_API_KEY`, `QDRANT_URL`, and `QDRANT_API_KEY` (omit the API key if running Qdrant locally via Docker — see `.env.example`).

   `mp2_rag.py` loads `.env` automatically via `python-dotenv`, so `source .env` is optional.

## Run

```bash
python mp2_rag.py ingest     # chunk + embed corpus, build Qdrant collection (run once)
python mp2_rag.py ask        # interactive Q&A — empty line or Ctrl-C to exit
python mp2_rag.py validate   # score against data/predefined_questions.jsonl
                             # (and data/learner_questions.jsonl if filled in)
```

Running `ingest` again drops and rebuilds the `mp2_sherlock` collection.

## Files

| Path | Purpose |
|---|---|
| `mp2_rag.py` | The pipeline and CLI |
| `corpus/` | Five Sherlock Holmes stories (`.txt`) |
| `data/predefined_questions.jsonl` | Provided validation questions |
| `data/learner_questions.jsonl` | Your own validation questions |
| `mp2_reflection.md` | Written reflection |
| `mp2_validation.txt` | Saved output from `validate` |
