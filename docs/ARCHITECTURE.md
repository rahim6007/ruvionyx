# System Architecture — Ruvionyx MVP

## Architecture choice
Use a modular FastAPI application plus a separate background worker. Keep identity, organization, knowledge-base, document, ingestion, retrieval, chat, and audit domains in separate modules. Avoid microservices in the MVP; the team and delivery window do not justify distributed-service complexity.

## Components
1. Next.js web application.
2. FastAPI application for authentication, workspace, document, chat, and admin APIs.
3. PostgreSQL as system of record, with pgvector for embeddings.
4. Redis as background-job broker/cache.
5. Celery worker for extraction, chunking, embedding, and indexing.
6. S3-compatible object storage for originals; MinIO locally.
7. LLM and embedding providers behind replaceable adapters.
8. Structured logs and OpenTelemetry instrumentation.

## Document ingestion
1. Authenticate and authorize upload to the selected organization and knowledge base.
2. Validate extension, detected MIME type, file size, and content.
3. Store the original in private object storage.
4. Create document and ingestion-job records.
5. Enqueue a job and return promptly to the browser.
6. Worker extracts text and page information, normalizes content, and chunks it.
7. Generate embeddings with a versioned embedding model.
8. Persist chunks and vectors with organization, knowledge-base, document, page, and chunk metadata.
9. Mark document ready; on error, record a safe failure code and allow bounded retry.

## Question answering
1. Authenticate user and validate organization membership.
2. Validate access to the selected knowledge base.
3. Embed the query and retrieve candidates using tenant- and permission-scoped filters.
4. Combine semantic and keyword retrieval, then rank candidates.
5. Build context only from authorized relevant evidence.
6. Ask the LLM to answer only from supplied evidence and abstain when evidence is insufficient.
7. Validate citation identifiers against retrieved chunks.
8. Store answer, citations, model/version metadata, and trace ID.
9. Return answer and source metadata to the browser.

## Security boundaries
- Authorization is application logic, never an LLM responsibility.
- Apply tenant filters in the database query before content leaves persistence.
- Do not retrieve globally and filter in application memory afterwards.
- Use opaque object keys and private storage.
- Treat document content as untrusted input and defend against prompt injection.
- Do not log raw document content, secrets, or full prompts by default.

## Data flow
Browser -> FastAPI -> authentication and authorization -> workspace/document APIs -> private object storage and Redis job queue -> worker -> extraction/chunking -> embedding adapter -> PostgreSQL/pgvector.
Chat follows Browser -> FastAPI -> authorization -> scoped retrieval -> context/citation builder -> LLM adapter -> citation validation -> grounded answer.

## Repository layout
- frontend: Next.js app.
- backend/app/core: configuration, database, security.
- backend/app/modules: auth, organizations, knowledge bases, documents, ingestion, retrieval, chat, audit.
- backend/app/integrations: LLM, embeddings, storage adapters.
- backend/app/workers: background tasks.
- infrastructure: local and deployment assets.
- docs: product and engineering decisions.
- tests: unit, integration, security, and end-to-end tests.

## Operational expectations
Run API and worker as separate processes. Add health/readiness endpoints, structured logs, correlation IDs, bounded retries, timeouts, and provider error handling. Add metrics and tracing before a production pilot.

## Open decisions
Confirm provider, cloud, region, object storage, embedding model/dimensions, retention policy, and authentication strategy during Sprint 1. Record decisions as ADRs.
