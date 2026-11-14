# Security Baseline — Ruvionyx MVP

Security is a release requirement because documents may contain private company information.

## Identity and authorization
- Authenticate every protected request.
- Enforce organization membership and role permissions server-side.
- Check access to the target knowledge base and document before reading, updating, deleting, or querying it.
- Never trust organization IDs or role values supplied by the browser without checking them against authenticated membership.
- Never ask the LLM to decide whether a user may see a document.

## Retrieval and RAG
- Apply tenant and knowledge-base filters in the database retrieval query itself.
- Do not perform global vector search and filter results afterwards.
- Send only authorized, relevant chunks to the model.
- Treat uploaded and retrieved text as untrusted data, not system instructions.
- Validate citation IDs against the exact retrieved chunk set.
- Abstain when evidence is missing or not relevant enough.

## File uploads
- Allow only PDF, DOCX, and TXT.
- Validate extension, detected MIME type, content, size, and parsing result.
- Generate opaque storage keys; never use user-supplied paths.
- Store originals in private object storage, not a public web directory.
- Apply safe limits for page count, extracted text size, and processing time.
- Reject malformed and suspicious files.

## Secrets and data handling
- Never commit credentials, API keys, private documents, or production data.
- Use ignored local environment files and a secrets manager in hosted environments.
- Redact secrets and sensitive payloads from logs.
- Use TLS in hosted environments and encrypted storage where supported.
- Define retention/deletion rules before handling real customer documents.

## Background jobs
- Make ingestion jobs idempotent.
- Limit retries and record safe error codes.
- Ensure retry cannot create duplicate chunks or vectors.
- Recheck document and tenant state in the worker before processing.

## Minimum security tests
1. User from Organization A cannot list, fetch, or delete Organization B's knowledge bases/documents.
2. User cannot retrieve chunks from another tenant by guessing IDs.
3. Member cannot perform Owner/Admin operations.
4. Unauthorized document content never appears in LLM context.
5. Citation IDs absent from retrieval results are rejected.
6. Malformed uploads fail without exposing server paths or stack traces.
7. Logs do not leak credentials or document contents.

## Incident readiness
Record audit events for role changes, invitations, uploads, deletions, access-denied events, and processing failures. Document how to revoke keys, disable compromised accounts, and investigate access incidents.
