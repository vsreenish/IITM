# Capstone Milestone 1

## Project Scenario

You have been hired as an AI Solutions Architect for an organization seeking to improve employee access to internal knowledge.

Employees currently depend on:

- HR teams for policy clarifications
- IT helpdesks for technical procedures
- Managers for operational guidelines
- Internal portals that are difficult to search

Your objective is to design an Enterprise Knowledge Assistant (EKA) capable of answering employee questions using approved internal documents while providing citations and confidence indicators.

The EKA must:

- Retrieve organisational knowledge
- Answer employee questions
- Provide source references
- Escalate gracefully when information is unavailable

## Data Description

Unlike traditional machine learning projects, this milestone focuses on building the foundation for a future RAG system.

You will create and maintain:

### 1. Knowledge Corpus

A collection of organisational documents that will later serve as the retrieval source.

Requirements:

- 10–30 documents
- 500–3000 words per document
- Internal organizational knowledge
- Multiple topic clusters
- Suitable for employee question-answering

### 2. Golden Question Set

A human-authored evaluation dataset containing 20 questions.

| Difficulty | Count | Purpose |
| --- | --- | --- |
| Easy | 8 | Single-document retrieval |
| Medium | 8 | Cross-document synthesis |
| Hard/Edge Cases | 4 | Escalation and refusal testing |

## Deliverables

### 1. ADR 0001 – Capstone Framing

File: `docs/adr/0001-capstone-framing.md`

Must include:

- Context
- Problem statement
- EKA scope
- Stakeholders
- KPI targets
- Technology approach
- Alternatives considered
- Trade-offs

### 2. ADR 0002 – API Contract

File: `docs/adr/0002-api-contract.md`

Must include:

- Purpose of API contract
- `/ask` endpoint specification
- Schema versioning rules
- Alternative approaches considered
- Trade-offs and future evolution strategy

### 3. Stakeholder Map

File: `docs/stakeholder-map.md`

Must include:

- Persona name
- Role and experience
- Current workflow
- EKA usage pattern
- Benefits if EKA succeeds

Target: 3–5 named personas

### 4. FastAPI Service Skeleton

Files:

- `src/api/main.py`
- Authentication module
- Logging middleware
- Cost tracking middleware

Must include:

- `/ask` endpoint
- Bearer token authentication
- Request logging
- Placeholder response handler
- Unit tests

### 5. Answer Schema

File: `src/pipeline/models.py`

Required schema:

```python
class Answer(BaseModel):
    content: str
    cost_usd: float
    retries: int
    confidence: float
    sources: list[str]
    schema_version: str = "v1"
```

### 6. Golden Question Set

File: `data/golden_set_full.jsonl`

Must include:

- 20 human-authored questions
- Ideal answers
- Tags
- Difficulty labels

Example:

```json
{
  "id": "q01",
  "question": "How many days of annual leave do employees receive?",
  "ideal_answer": "Employees receive 20 days of annual leave per year.",
  "tags": ["HR", "Leave", "Easy"]
}
```

### 7. Evaluation Framework Baseline

File: `scripts/run_rag_eval.py`

Must support:

```shell
python run_rag_eval.py --fake --label baseline
```

Purpose:

- Baseline evaluation execution
- End-to-end framework validation
- Future performance comparison

### 8. Design Review (DR#1) One-Pager

Length: 400–500 words

Must include:

- What I am building
- Who it is for
- Current architecture
- KPI targets
- Key trade-offs
- Uncertainties and risks

## Success Criteria

### Scope Validation

Your EKA must satisfy all three conditions:

| Requirement | Description |
| --- | --- |
| Enterprise | Internal organizational knowledge |
| Knowledge | Retrieves existing content |
| Assistant | Question-and-answer interaction |

### Corpus Requirements

| Criteria | Requirement |
| --- | --- |
| Documents | 10–30 |
| Document Size | 500–3000 words |
| Topic Coverage | Minimum 5 documents per major topic |
| Rights Status | Approved for project use |

### Golden Set Requirements

| Requirement | Value |
| --- | --- |
| Total Questions | 20 |
| Answerable Questions | Minimum 16 |
| Hard Questions | 4 |
| Human Verification | Mandatory |

## Key Performance Indicators (KPIs)

Learners must define three sponsor-level KPIs such as:

- Question resolution rate
- Employee self-service adoption
- Information retrieval accuracy
- Response time reduction
- Helpdesk ticket reduction

Each KPI must include:

- Baseline value
- Target value
- Business justification

## Submission Instructions

Submit the following:

### Folder Structure

```text
M1_Capstone_[YourLastName]/
├── docs/
│   ├── adr/
│   │   ├── 0001-capstone-framing.md
│   │   └── 0002-api-contract.md
│   └── stakeholder-map.md
│
├── src/
│   ├── api/
│   │   └── main.py
│   └── pipeline/
│       └── models.py
│
├── data/
│   └── golden_set_full.jsonl
│
├── scripts/
│   └── run_rag_eval.py
│
└── DR1_OnePager.pdf
```

Compress the completed project into:

**AI-RAG_M1_[YourLastName].zip**
