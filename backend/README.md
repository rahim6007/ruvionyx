# Backend

The FastAPI service will be implemented in Sprint 1.

Suggested structure:
- app/core: configuration, database, security.
- app/modules: auth, organizations, knowledge bases, documents, ingestion, retrieval, chat, audit.
- app/integrations: LLM, embeddings, and storage adapters.
- app/workers: background task entry points.

First milestone: app startup, environment settings, health endpoint, PostgreSQL connection, migrations, pytest, and lint/type checks.
