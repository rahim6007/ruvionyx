# Team Operating Agreement

## Ownership
- Project Lead / Architect: scope, architecture, API contracts, integration, decisions, release acceptance.
- Frontend Engineer: Next.js UI, workspace, document management, chat, citations, browser tests.
- Backend Engineer: FastAPI, authentication, organizations, memberships, roles, PostgreSQL, APIs, audit events.
- AI / RAG Engineer: parsing, chunking, embeddings, retrieval, prompt design, citation validation, evaluation.
- DevOps / QA Engineer: Docker, CI/CD, testing, tenant-isolation checks, cloud deployment, logging, monitoring.

These are role assignments, not real GitHub identities. Confirm actual team members before assigning accounts.

## Communication
- Daily: brief update of yesterday, today, and blockers.
- Weekly: review progress, risks, and decisions.
- Every two weeks: demonstrate working features and run a retrospective.
- Record decisions and blockers in GitHub issues or project docs.

## Issue requirements
Every issue must include purpose, one responsible owner, priority, acceptance criteria, dependencies, and test expectations. Split work into reviewable changes.

## Branch and pull request rules
- Branch from develop.
- Use feature/issue-number-short-description, fix/issue-number-short-description, or docs/issue-number-short-description.
- Target pull requests at develop.
- Link related issues.
- Include tests and verification notes.
- Request peer review; do not self-approve.
- Do not merge with failing required checks or unresolved security concerns.
- Promote tested releases to main through a release pull request.

## Definition of Done
Acceptance criteria are met; tests pass; peer review is complete; docs/migrations/configuration are updated; security and tenant impact are reviewed; no release-blocking defect remains; change is merged into the agreed branch.

## Working agreements
Keep pull requests focused. Never commit secrets or real company documents. Raise blockers early. Do not mark work complete without evidence.
