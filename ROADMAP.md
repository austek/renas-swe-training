# Roadmap

Three milestones, each one a self-contained slice worth describing as a
project in an interview.

## M1 — Production Skeleton

Scaffolding, dependency injection, `Dockerfile` / compose, DB migrations,
baseline CI pipeline. Seed issues:

1. Dev environment dry run — clone, `docker compose up`, confirm
   backend/frontend/db come up together
2. Design the `Incident` entity + Flyway migration (state machine:
   triggered → acknowledged → resolved)
3. `Incident` CRUD API skeleton — routes wired, handlers stubbed, tests
   scaffolded
4. Wire the frontend incident list view to the API

## M2 — Core Domain & API

Domain entities, repository pattern, REST endpoints, idempotent handlers
(the webhook ingestion endpoint in particular — replaying the same alert
must not create duplicate incidents), real test coverage.

## M3 — Observability & Resilience

Structured logging, `/healthz` & `/metrics`, graceful shutdown, input
validation schemas. An incident tracker that can't observe its own health
is a good story to avoid telling in an interview — this milestone closes
that gap deliberately.

## Later, not scheduled yet

- Live AWS deployment (ECS + RDS) — see `infra/README.md`
- CodeQL / coverage gates in CI
- Promoting conventional-commit convention from documented expectation to
  a CI-enforced check
