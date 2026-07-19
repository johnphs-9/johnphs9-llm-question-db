# Local LLM Question Log
Github: https://github.com/johnphs-9/johnphs9-llm-question-db

A small FastAPI web app that asks a locally-running LLM (Ollama with `llama3.2`) a question and persists the conversation history in Postgres. Built as the capstone of the Local LLM Question Log course.

## What it does

- POST a question to `/ask` → backend calls a local LLM and returns the answer
- Every interaction (question, answer, timestamp, model) persists to Postgres
- The web UI shows the most recent ten interactions
- A `/healthz` endpoint reports reachability of Ollama and Postgres

## Stack

- **FastAPI** + **Uvicorn** — Python web server
- **Ollama** + **llama3.2** — local LLM runtime
- **Postgres** — interaction history
- **Pydantic** — typed request/response validation
- **Jinja2** + vanilla `fetch()` — the web UI

## Run it locally

Requires Python 3.11+, Postgres running on `localhost:5432`, and Ollama with `llama3.2` pulled (~2 GB).

## Run

```bash
source venv/bin/activate
pip install -r requirements.txt   # adds python-dotenv
cp .env.example .env
uvicorn app.main:app --reload
```
Open <http://localhost:8000>.

## Verify (self-check)

The happy path:z

```bash
curl -s http://localhost:8000/healthz
curl -s -X POST http://localhost:8000/ask -H "Content-Type: application/json" -d '{"question":"Hello"}'
```


