# LangChain Cheat Sheet

API changes fast. Check docs for current imports.

## Install

```bash
pip install langchain langchain-core langchain-text-splitters
pip install langchain-openai          # or langchain-anthropic, langchain-ollama ...
export OPENAI_API_KEY=...             # provider key, never commit
```

## Components

| Component | Role |
|---|---|
| Chat model | LLM wrapper: `.invoke()`, `.stream()`, `.batch()` |
| Prompt template | Prompt with `{variables}` |
| Output parser | Model output → str / JSON / Pydantic |
| LCEL | Pipe operator chaining prompt → model → parser |
| Document loader | Load PDF, web, files → `Document` |
| Text splitter | Split docs into chunks |
| Embeddings | Text → vector |
| Vector store | Store + search vectors (Chroma, FAISS, pgvector) |
| Retriever | Query → relevant docs |
| Tool | Function model can call |
| Agent | Model + tools loop |
| LangGraph | Stateful multi-step agents as graphs |
| LangSmith | Tracing, debugging, evals |

## Model

```python
from langchain.chat_models import init_chat_model

model = init_chat_model("provider:model-name", temperature=0)
model.invoke("Explain RAG in one line").content
for chunk in model.stream("Hi"):
    print(chunk.content, end="")
```

## Prompt + chain (LCEL)

```python
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a concise tutor."),
    ("human", "Explain {topic} in 3 bullets."),
])
chain = prompt | model | StrOutputParser()
chain.invoke({"topic": "Docker volumes"})
chain.batch([{"topic": "IAM"}, {"topic": "VPC"}])
```

## Structured output

```python
from pydantic import BaseModel

class Summary(BaseModel):
    title: str
    points: list[str]

structured = model.with_structured_output(Summary)
structured.invoke("Summarize: ...")          # → Summary object
```

## RAG pipeline

```python
from langchain_text_splitters import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=100)
chunks = splitter.split_documents(docs)

vectorstore = SomeVectorStore.from_documents(chunks, embeddings)
retriever = vectorstore.as_retriever(search_kwargs={"k": 4})

relevant = retriever.invoke("What is IAM?")
context = "\n\n".join(d.page_content for d in relevant)
answer = chain.invoke({"topic": f"IAM using context:\n{context}"})
```

```text
Load → Split → Embed → Store → Retrieve → Prompt + context → LLM → Answer
```

## Tools

```python
from langchain_core.tools import tool

@tool
def get_weather(city: str) -> str:
    """Return weather for a city."""
    return f"Sunny in {city}"

model_with_tools = model.bind_tools([get_weather])
msg = model_with_tools.invoke("Weather in Chennai?")
msg.tool_calls          # model's requested calls
```
