# Test Strategy

- Backend: pytest for unit and API integration tests.
- Frontend: component tests and Playwright browser tests.
- Cross-service: verify upload, ingestion, retrieval, citations, and persistence.
- Security: tenant-isolation and role/permission tests are release requirements.
- AI: run the versioned evaluation set in docs/AI-EVALUATION.md.

Use only synthetic or public sample documents in the initial test suite. Never use confidential company documents or production secrets.
