# Ruvionyx

**Enterprise Knowledge Intelligence Platform**

Ruvionyx helps companies store, search, and find answers from their documents.

> Repository bootstrap: the product is in its planning and foundation stage. The application services have not yet been implemented.

## MVP

- Company workspaces, user accounts, memberships, and role-based access.
- PDF, DOCX, and TXT uploads.
- Background document extraction, chunking, and indexing.
- PostgreSQL with pgvector for document and vector storage.
- RAG chat that answers from authorized documents and shows source citations.
- Conversation history, document administration, and audit events.
- Automated tests, Docker-based local development, CI/CD, and basic monitoring.

## Proposed stack

| Area | Technology |
|---|---|
| Frontend | Next.js, React, TypeScript, Tailwind CSS |
| Backend | Python, FastAPI |
| Database | PostgreSQL + pgvector |
| Background jobs | Redis + Celery |
| File storage | S3-compatible storage; MinIO for local development |
| Document parsing | PyMuPDF, python-docx |
| Testing | Pytest, Playwright |
| Delivery | Docker, GitHub Actions |
| Observability | Structured logs, OpenTelemetry |

## Repository layout

```text
frontend/          Next.js application
backend/           FastAPI application
infrastructure/    Local and deployment configuration
docs/              Product, architecture, security, and delivery docs
tests/             Cross-service and end-to-end tests
.github/           Issue and pull-request templates/workflows
```

## Local setup

1. Copy `.env.example` to `.env`.
2. Review and change local passwords in `.env`.
3. Start infrastructure:

```bash
docker compose up -d
docker compose ps
```

At this stage Docker Compose starts PostgreSQL with pgvector and Redis. Frontend and backend services will be added in the first implementation sprint.

## Workflow

- `main`: stable, release-ready code.
- `develop`: integration branch.
- Use short-lived branches named `feature/<issue>-short-name`, `fix/<issue>-short-name`, or `docs/<issue>-short-name`.
- Open pull requests into `develop`; link the issue and request peer review.
- Merge only after acceptance criteria are met and required checks pass.
- Promote tested work to `main` with a release pull request.

## Team ownership

| Role | Ownership |
|---|---|
| Project Lead / Architect | Scope, architecture, API contracts, integration, decisions, release acceptance |
| Frontend Engineer | UI, workspace, documents, chat, citations, browser tests |
| Backend Engineer | FastAPI, authentication, tenancy, RBAC, database, APIs, audit events |
| AI / RAG Engineer | Parsing, chunking, embeddings, retrieval, generation, citations, evaluation |
| DevOps / QA Engineer | Docker, CI/CD, environments, testing, security checks, deployment, monitoring |

Add real team members as collaborators and assign issues only after their GitHub accounts are confirmed.

## Definition of Done

A task is complete when its acceptance criteria are met, relevant tests pass, the change has been peer-reviewed, documentation is updated, and the change is merged into the agreed branch.

## Security principles

- Enforce organization membership and resource permissions on the server.
- Apply tenant filters before vector search results or document text reach the LLM.
- Never let the model make authorization decisions.
- Keep credentials out of source control.
- Validate uploaded files and store originals outside the web root.
- Treat retrieved document text as untrusted input and test prompt-injection handling.

See `docs/` for the project charter, requirements, architecture, data model, security baseline, AI evaluation, and Sprint 1 backlog.
