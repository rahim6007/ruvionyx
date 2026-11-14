# ADR-001: Modular monolith with a separate worker

- Status: Proposed for MVP; confirm during Sprint 1.
- Owner: Project Lead / Architect.

## Context
The MVP has several related domains, a small team, and a short delivery window. Microservices would add networking, deployments, observability, and distributed consistency overhead before boundaries are proven.

## Decision
Use one modular FastAPI application with explicit domain modules and a separate background worker for long-running document ingestion. Keep LLM, embeddings, and storage integrations behind adapters.

## Consequences
Benefits: simpler local development, transactions, authorization boundaries, and end-to-end tests; worker can scale independently.
Trade-offs: modules share one API deployment artifact; boundaries must be enforced through reviews and tests.

## Revisit when
Independent scaling, availability, release cadence, team ownership, or measured performance needs justify extracting a service.
