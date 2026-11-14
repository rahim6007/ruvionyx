# ADR-002: PostgreSQL with pgvector for initial retrieval storage

- Status: Proposed; confirm during Sprint 1.
- Owners: Backend Engineer and AI / RAG Engineer.

## Context
The application needs relational data for tenants, permissions, documents, and conversations, plus vector search over document chunks.

## Decision
Use PostgreSQL as the system of record and pgvector for initial embedding storage and similarity search. Keep retrieval behind an application interface so a dedicated search service can be considered later if measurements justify it.

## Consequences
- One primary database to operate and back up.
- Tenant filters can be applied in the same query path as vector similarity search.
- Embedding model and dimensions must be versioned.
- Index choice and query performance must be benchmarked against realistic sample data.
