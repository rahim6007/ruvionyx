# Sprint 1 Backlog — Repository and Product Foundation

Sprint length: two weeks. Sprint dates are unset until kickoff and team availability are confirmed.

## Sprint goal
Create a consistent development environment, confirm product/architecture contracts, and prove that sample documents can be parsed locally.

## Project Lead / Architect
1. Finalize MVP requirements and acceptance criteria.
   - Deliverable: team-approved scope and testable acceptance criteria.
2. Agree API contracts and module boundaries.
   - Deliverable: request/response shapes for auth, workspace, knowledge base, upload, job status, and chat.

## Frontend Engineer
3. Create Next.js application skeleton.
   - Acceptance: TypeScript app starts locally, linting works, shared layout/navigation exists, API URL is configurable, and run instructions are documented.
4. Create MVP wireframes and design tokens.
   - Acceptance: authentication, workspace, knowledge-base, upload, chat, and admin flows include loading/empty/error/permission states.

## Backend Engineer
5. Create FastAPI application skeleton.
   - Acceptance: app starts, health endpoint responds, settings come from environment, and one automated test passes.
6. Design initial PostgreSQL schema and migrations.
   - Acceptance: users, organizations, memberships, knowledge bases, documents, jobs, chunks, conversations, messages, citations, and audit events have defined relationships.

## AI / RAG Engineer
7. Build document parsing proof of concept.
   - Acceptance: sample PDF, DOCX, and TXT extraction returns text and page metadata where available; malformed files fail safely.
8. Define chunking and embedding evaluation plan.
   - Acceptance: proposed provider/model and embedding dimensions are documented before persistence schema is finalized.

## DevOps / QA Engineer
9. Set up Docker Compose for PostgreSQL/pgvector and Redis.
   - Acceptance: health checks pass, pgvector is enabled, volumes persist, and no real secrets are committed.
10. Create initial GitHub Actions checks as app skeletons land.
   - Acceptance: PR checks run and report failures; no secret values are stored in source.

## Cross-team acceptance
- Every member can clone the repo and follow local setup.
- main is stable and development targets develop.
- No production credentials or customer documents are committed.
- A sample document parsing demo is available.
- Sprint demo records completed, in-progress, and blocked tasks with evidence.

## Dependencies
Confirm actual teammates and GitHub usernames before assignment. Confirm LLM/embedding providers before final model configuration and confirm cloud provider before deployment.
