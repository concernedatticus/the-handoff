# 13-backend-infra — Backend infrastructure: queues, cron, secrets, DataAPI/GraphQL, pgvector

Seed sources for this topic — add one file per reference, using this metadata header:

```yaml
---
title:
source:
url:
authority: official | standard | high | medium
topic: 13-backend-infra
version:
last_verified:   # YYYY-MM-DD
applies_to:
notes:
---
```

## Seed sources to ingest (one file each)

- **Transactional outbox & idempotent consumer patterns** — microservices.io patterns catalogue (microservices.io/design/patterns, authority: high)
- **pg-boss / graphile-worker docs** — Postgres-backed queues, SKIP LOCKED semantics (official)
- **Standard Webhooks spec** — standardwebhooks.com (standard)
- **RFC 9457** — Problem Details for HTTP APIs (standard)
- **RFC 9700** — OAuth 2.0 Security Best Current Practice (standard)
- **pgvector README** — HNSW vs IVFFlat, opclass/distance-operator matching (official)
- **OWASP API Security Top 10 (2023)** — owasp.org (high)
- **Google SRE Workbook: release engineering & postmortems** — sre.google/workbook (high)
- **OpenTelemetry docs** — traces/metrics/logs correlation (official)
- **PostgREST / Supabase / Hasura RLS guidance** — RLS as the security boundary for DataAPI (official)

Rules: one page max, link to the primary source, state which versions it applies to, re-verify entries older than 90 days.
