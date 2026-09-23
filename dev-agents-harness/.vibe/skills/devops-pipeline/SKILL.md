---
name: devops-pipeline
description: Design or harden CI/CD pipelines (GitHub Actions baseline, gated migrations, progressive delivery, supply-chain security). Use when creating workflows, adding deploy gates, or fixing a broken pipeline.
user-invocable: true
---

# DevOps Pipeline

## Objective
A pipeline that is fast, reproducible, least-privileged, and safe to fail.

## Procedure
1. Order: install (frozen lockfile) → typecheck → lint → unit → integration (real Postgres service container) → build → security scans → deploy.
2. Pin every action by commit SHA; set least-privilege `permissions:` per job; concurrency groups with cancel-in-progress.
3. Use OIDC federation to cloud providers; no long-lived keys in secrets.
4. Run `prisma migrate deploy` as a separate, gated step before app rollout (expand/contract guarantees both versions work).
5. Deploy progressively: canary/blue-green or feature flags; automatic rollback on SLO burn; one-click rollback is a requirement.
6. Supply chain: lockfiles, Renovate/Dependabot, `pnpm audit`/OSV, SBOM, signed artifacts.

## Output
Workflow YAML · Permissions & pinning checklist · Migration gate · Rollback plan · Required checks list
