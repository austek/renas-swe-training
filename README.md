# renas-swe-training

Portfolio repo for interview prep — building one production-shaped
full-stack service, milestone by milestone, instead of a checklist of
isolated exercises. The goal is evidence you can point to in an interview:
real trade-offs, real CI, real PR reviews, not a tutorial you followed.

## Stack

- **Backend** — Java 17, Spring Boot, Gradle
- **Frontend** — React (Vite)
- **Data** — PostgreSQL, Flyway migrations
- **Infra** — Docker Compose locally now; AWS (ECS + RDS) once there's a
  working app worth deploying (see `infra/README.md`)

## Domain

An **Incident & On-Call Tracker** — see `docs/adr/0001-overview.md` for why
this domain and what it's meant to demonstrate.

## Workflow

- Work is milestone-shaped, not phase-shaped — see `ROADMAP.md`.
- Every change goes through a PR (`.github/PULL_REQUEST_TEMPLATE.md`) —
  no self-merges.
- CI (`.github/workflows/ci.yml`) runs backend and frontend build/test/lint
  on every PR and push to `main`.
- Track progress on the repo's project board.

## Running locally

```
docker compose up
```

Backend on `:8080` (`/actuator/health`), frontend on `:5173`, Postgres on
`:5432`. Backend and frontend can also be run individually — see
`backend/` and `frontend/` for their own build commands.
