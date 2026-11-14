# Initial Data Model

This is a logical starting point. Confirm constraints, indexes, and migrations with the backend and AI/RAG engineers before implementation.

## Main entities

| Entity | Purpose |
|---|---|
| users | User accounts |
| organizations | Company workspaces / tenants |
| memberships | User roles within an organization |
| knowledge_bases | Document collections |
| knowledge_base_permissions | Optional per-knowledge-base member access |
| documents | Original file metadata and storage key |
| ingestion_jobs | Processing state, attempts, and safe error code |
| document_chunks | Extracted text, page metadata, and embedding |
| conversations | Chat sessions scoped to organization, user, and knowledge base |
| messages | User questions and assistant answers |
| citations | Links between assistant messages and source chunks |
| audit_events | Security and lifecycle activity |

## Relationships
- One organization has many memberships and knowledge bases.
- A user can belong to multiple organizations through memberships.
- A knowledge base belongs to exactly one organization.
- A document belongs to one organization and one knowledge base.
- A document has ingestion jobs and, when indexed, many chunks.
- A conversation belongs to one organization, user, and knowledge base.
- A message belongs to one conversation.
- A citation links an assistant message to a source chunk.
- An audit event is scoped to an organization where applicable.

## Integrity rules
- Use UUIDs or similarly non-guessable public identifiers.
- Enforce unique membership per organization/user.
- Ensure a document's knowledge_base_id and organization_id cannot disagree.
- Ensure conversation user membership is valid for its organization.
- Store embedding model and dimensions/version on indexed chunks.
- Define deletion and retention rules for dependent chunks, vectors, and citations.

## Tenant isolation
Every tenant-owned query must include organization context. A caller must not access another tenant's records by supplying a guessed ID. Apply organization and access filters inside the SQL query used for vector retrieval. Add automated negative tests for cross-tenant access.

## Initial index suggestions
- Unique index on memberships (organization_id, user_id).
- Index knowledge_bases by organization.
- Index documents by organization, knowledge base, and status.
- Index chunks by organization, knowledge base, and document.
- Index conversations by organization, user, and creation time.
- Index messages by conversation and creation time.
- Index audit events by organization and creation time.
- Add pgvector index after choosing the similarity operator and benchmarking realistic data.

## Open decisions
Choose UUID generation, auth model, per-knowledge-base permission semantics, deletion/retention behavior, and embedding dimension before final migrations.
