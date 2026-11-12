# GenAI Cheat Sheet

## Terms

| Term | Meaning |
|---|---|
| LLM | Large language model: predicts next token |
| Token | Text chunk, ~4 chars / ~0.75 word in English |
| Context window | Max tokens per request (input + output) |
| Prompt | Input instructions + data |
| System prompt | Persistent role/rules for the model |
| Temperature | Randomness: 0 = focused, 1 = creative |
| Top-p | Sample from top probability mass |
| Max tokens | Output length limit |
| Embedding | Text → vector for similarity search |
| Vector DB | Stores embeddings: pgvector, Pinecone, Chroma |
| RAG | Retrieve docs → add to prompt → answer |
| Fine-tuning | Train model further on own data |
| Tool use / function calling | Model calls external functions/APIs |
| Agent | LLM loop: plan → call tools → observe → repeat |
| MCP | Model Context Protocol: standard tool/data connector |
| Hallucination | Confident but false output |

## Prompt structure

```text
Role:        You are a senior backend engineer.
Task:        Review this API for bugs.
Context:     FastAPI, PostgreSQL, used by mobile app.
Input:       <code> ... </code>
Constraints: No new dependencies. Keep public API.
Format:      Table: file | line | issue | fix.
Examples:    (optional) one sample input → output
```

## Prompt tips

| Tip | Example |
|---|---|
| Be specific | "3 bullet points, max 15 words each" |
| Delimit input | Wrap data in `<doc>...</doc>` tags or code fences |
| Give examples | Few-shot: 1–3 input → output pairs |
| Ask for steps | "Plan first, then implement" |
| Set output format | JSON schema, table, markdown |
| Split big tasks | One phase per prompt |
| Ask to verify | "List assumptions and risks" |

## Task → technique

| Task | Technique |
|---|---|
| Answer from own docs | RAG |
| Consistent style/format | Few-shot examples, system prompt |
| Actions (search, DB, API) | Tool use / agent |
| Domain-specific behaviour at scale | Fine-tuning |
| Structured data out | JSON schema / structured output |
