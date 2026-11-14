# GitHub Tracking Guide

## Repository
- Repository: rahim6007/ruvionyx
- Default branch: main
- Integration branch: develop
- Keep repository private during development unless the owner explicitly chooses otherwise.
- Add confirmed teammates as collaborators with least privilege.
- Protect main and develop with pull requests, approvals, and passing checks once CI is available.

## Suggested project board
Name: Ruvionyx — MVP Delivery.

Fields:
- Status: Backlog, Ready, In progress, In review, Blocked, Done.
- Priority: Critical, High, Medium, Low.
- Owner role: Lead, Frontend, Backend, AI/RAG, DevOps/QA.
- Sprint: Sprint 1–5.
- Target date: set only after kickoff and availability are confirmed.

Views:
1. Team board grouped by Status.
2. Sprint table filtered by Sprint.
3. Roadmap grouped by Sprint.
4. Blockers view filtered to Blocked.

## Labels
Issue type: feature, task, bug, documentation, security, research.
Component: frontend, backend, ai-rag, devops, database, api, ingestion, chat.
Priority: priority: critical, priority: high, priority: medium, priority: low.
Workflow: blocked, needs-design, needs-decision, good-first-issue.

## Pull request rules
- Branch from develop.
- Target develop.
- Include issue link, summary, tests, verification, and security/data-impact notes.
- Require peer review and passing CI before merge.
- Squash merge is preferred for a concise feature history.

## Sprint review evidence
Use commits, issues, PRs, checks, test results, and demo/deployment links. Moving an issue to Done is not sufficient evidence by itself.
