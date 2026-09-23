---
name: postgres-migrations
description: Plan and write safe Postgres/Prisma migrations (expand/contract, concurrent indexes, backfills, pgvector indexes). Use when changing schema, indexes, constraints, RLS, or data.
user-invocable: true
---

# Postgres Migrations

## Objective
Ship schema changes that never break the currently deployed version and never take a long lock.

## Procedure
1. Additive first: nullable column → dual-write → batched backfill → switch reads → drop later (separate deploy).
2. Use `CREATE INDEX CONCURRENTLY`; set `lock_timeout` and `statement_timeout` before running.
3. Prisma: `migrate dev` local only; `migrate deploy` in CI; commit migrations; hand-edit SQL for RLS, partial indexes, and pgvector operators Prisma cannot express.
4. Test on a production-like copy (Neon branch or restored backup) before proposing.
5. Document the rollback for every step.

## Rules
- Expand/contract only: old and new code must both work during rollout.
- Never `migrate reset` or `migrate dev` against a shared database.
- Backfills run in bounded batches with progress tracking.

## Output
Migration steps · Lock analysis · Backfill plan · Rollback plan · Verification evidence
