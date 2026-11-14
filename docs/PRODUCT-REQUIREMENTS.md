# Product Requirements — Ruvionyx MVP

## Product summary
A multi-tenant web application that lets organizations upload internal documents and ask questions answered using relevant, permission-checked evidence.

## Primary users
1. Workspace Owner: creates the organization and manages access.
2. Admin: manages members, knowledge bases, and documents.
3. Member: asks questions against authorized knowledge bases.

## Core user journeys

### Create a workspace
- A user registers and signs in.
- The user creates an organization workspace and becomes its Owner.
- The owner can invite members and assign supported roles.

### Upload a document
- An authorized user opens a knowledge base and uploads PDF, DOCX, or TXT.
- The API validates the file and stores the original in private object storage.
- A background job is queued.
- The UI shows queued, processing, ready, or failed status.
- Authorized users can retry a failed job.

### Ask a question
- A member selects a knowledge base they can access.
- The backend verifies organization membership and knowledge-base access.
- Retrieval searches only authorized document chunks.
- Relevant evidence is sent to the LLM.
- The answer is stored with citations to exact source chunks and page numbers when available.
- If evidence is insufficient, the assistant says it cannot find enough information.

## Functional requirements
- FR-01: Register, sign in, and sign out.
- FR-02: Create and manage organization workspaces.
- FR-03: Owners/Admins can invite and manage members.
- FR-04: Enforce role and resource permissions server-side.
- FR-05: Create knowledge bases within organizations.
- FR-06: Upload PDF, DOCX, and TXT files.
- FR-07: Validate uploads and store originals outside the web root.
- FR-08: Run document processing asynchronously.
- FR-09: Show processing status and safe failure details.
- FR-10: Normalize, chunk, embed, and index text with source metadata.
- FR-11: Support semantic and keyword retrieval.
- FR-12: Generate answers only from retrieved, authorized evidence.
- FR-13: Include citations to source documents and relevant page/chunk.
- FR-14: Abstain when evidence is insufficient.
- FR-15: Persist conversations and messages.
- FR-16: Record document lifecycle and security-relevant audit events.
- FR-17: Test core flows with automated tests.
- FR-18: Run local dependencies using Docker Compose.

## Non-functional requirements
- Security: tenant filters are applied before retrieval results reach an LLM.
- Reliability: ingestion jobs are retryable and idempotent.
- Traceability: citations resolve to the evidence used.
- Maintainability: backend domains and provider integrations are modular.
- Observability: capture request IDs, job status, latency, failures, and model usage without logging secrets or unnecessary document content.
- Accessibility: primary flows and error states are keyboard-accessible.
- Performance: establish baselines with a representative test corpus before making scale claims.

## MVP acceptance tests
- A user in Organization A cannot read or retrieve Organization B's documents.
- Unauthorized users cannot access a knowledge base by guessing its ID.
- PDF, DOCX, and TXT sample files ingest asynchronously.
- Failed jobs can be retried without duplicate chunks.
- Answers with supporting text return citations that resolve to source chunks.
- Questions without supporting evidence receive an abstentions.
- Conversation history survives refresh.
- Local setup is reproducible.

## Open decisions
Confirm LLM provider, embedding provider/model, cloud provider, region, object storage, authentication strategy, and retention policy during Sprint 1.
