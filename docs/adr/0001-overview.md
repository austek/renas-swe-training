# ADR 0001 — Domain, stack, and scope for the portfolio project

## Status

Accepted

## Context

This repo exists to produce interview-ready evidence of production
judgment, on a short timeline. That shapes three decisions up front,
recorded here the way a real ADR would be — this file itself is meant as
rehearsal for the system-design-interview habit of writing decisions down.

## Decision

**Domain: Incident & On-Call Tracker.** Chosen over a generic CRUD demo
(e.g. a task tracker) because it forces real production concerns into the
data model and API from the start, rather than needing to be bolted on
later:

- An incident's lifecycle is a state machine (triggered → acknowledged →
  resolved), not just a row — good for talking about invariants and
  validation.
- Alert ingestion (the entry point for a new incident) is a natural
  idempotency problem: the same upstream alert can and will be delivered
  more than once, and a duplicate incident is a wrong answer.
- Role-based access (engineer vs. on-call lead) gives a real reason for
  auth/authorization beyond "because the tutorial had a login page."
- The domain motivates its own observability story — a tool for watching
  system health should have to answer for its own (Milestone 3).

**Stack: Java/Spring Boot backend, React frontend, PostgreSQL, Docker
Compose locally.** Chosen for depth over breadth — one stack, built
correctly, with real CI and a real PR workflow, reads better in an
interview than several stacks explored shallowly.

**AWS is scoped out of Milestone 1.** The target architecture (ECS
Fargate, RDS, S3/CloudFront — see `infra/README.md`) is documented now so
it's a deliberate deferral, not an omission, but provisioning a live
account is deferred until there's a working app worth deploying. Given the
short timeline, cloud setup time is better spent once, later, on something
real to deploy.

## Consequences

- Milestone 1's seed issues (see `ROADMAP.md`) start with the `Incident`
  entity and its migration, not with auth or notifications — the state
  machine is the core of the domain and should be built first.
- Idempotent webhook ingestion and the notification dispatch land in
  Milestone 2, once the core entity exists to be idempotent about.
