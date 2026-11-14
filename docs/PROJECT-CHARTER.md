# Ruvionyx — Project Charter

## Purpose
Ruvionyx helps employees find trustworthy answers from documents their organization is allowed to use. It combines private document management, search, RAG answers, source citations, and workspace access controls.

## Problem
Company knowledge is spread across policies, manuals, guides, and reports. Employees waste time searching, while general AI tools may lack access to company content or produce unsupported answers.

## MVP goal
Build a secure, deployable web application where an authorized user can upload supported documents, ask a question, receive an answer grounded in retrieved evidence, and open the cited source.

## In scope
- User accounts, organization workspaces, memberships, and roles.
- Knowledge bases within organizations.
- PDF, DOCX, and TXT uploads with validation.
- Asynchronous extraction, chunking, embeddings, and indexing.
- PostgreSQL with pgvector.
- Keyword and semantic retrieval.
- RAG chat with citations and conversation history.
- Document administration and audit events.
- Docker-based local environment, automated tests, CI/CD, staging, and monitoring.

## Out of scope for MVP
OCR for scanned documents; Google Drive, SharePoint, Slack, and Notion connectors; SSO/SAML; billing; autonomous agents; multi-provider routing; advanced workflow automation. Revisit after the core product is reliable.

## Roles
- Owner: creates workspace and manages administrators/settings.
- Admin: manages members, knowledge bases, and documents in the organization.
- Member: searches and chats only with resources they are allowed to access.

## Team ownership
- Project Lead / Architect: scope, system design, API contracts, integration, decisions, release acceptance.
- Frontend Engineer: Next.js interface, workspace, document flows, chat, citations, browser tests.
- Backend Engineer: FastAPI, authentication, tenancy, roles, database, APIs, audit events.
- AI / RAG Engineer: extraction, chunking, embeddings, retrieval, prompting, citations, evaluation.
- DevOps / QA Engineer: Docker, CI/CD, test strategy, security/performance checks, deployment, monitoring.

## Delivery assumptions
The plan is ten weeks and five two-week sprints. The estimate assumes five contributors with around 10–15 hours per week each. It is not a committed deadline until kickoff and team availability are confirmed.

## Governance
Every issue must have one responsible owner, priority, and acceptance criteria. Every code change uses a pull request and peer review. Run a weekly status review and a demo/retrospective at the end of each two-week sprint.

## Success criteria
Authorized users can manage a workspace, upload supported documents, see processing status, ask questions, inspect valid citations, and use persisted conversations; tenant-isolation tests pass; ingestion failures are visible and recoverable; and the system can be run locally and deployed to a test environment.
