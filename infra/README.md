# infra

Local stack only — `docker-compose up` from the repo root brings up Postgres,
the Spring Boot backend, and the React frontend (served via nginx) together.

## AWS target (not provisioned yet)

Milestone 1 is Docker/local-only on purpose. The intended production target,
scaffolded here only as documentation until a later milestone actually
provisions it:

- **Backend** — ECS Fargate service, image pushed to ECR
- **Database** — RDS for PostgreSQL
- **Frontend** — S3 + CloudFront
- **IaC** — Terraform or AWS CDK (undecided — pick one and record the choice
  as an ADR when this milestone starts)

Deferring the live account avoids burning setup time on IAM/billing before
there's a working app to deploy.
