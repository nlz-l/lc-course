# LC Course

LangChain, LangGraph, notebook, and FastAPI practice project.

## Contents

- `notebooks`: LangChain course notebooks and self-written agent notes
- `app`: FastAPI backend for a personal chef assistant
- `app/api/v1`: chat and OSS upload URL APIs
- `app/agents`: LangGraph/LangChain agent logic

## Run

```bash
uv sync
copy .env.example .env
uv run python -m app.main
```

Fill `.env` with your own model, search, LangSmith, and OSS credentials before running.
