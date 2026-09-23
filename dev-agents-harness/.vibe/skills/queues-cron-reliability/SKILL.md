---
name: queues-cron-reliability
description: Design or debug queues, workers, and cron jobs (idempotency, retries, DLQ, outbox, overlap protection). Use when adding background jobs, scheduled tasks, or investigating stuck/duplicate work.
user-invocable: true
---

# Queues & Cron Reliability

## Objective
Make background work correct under at-least-once delivery and observable when it degrades.

## Procedure
1. Make every consumer idempotent: dedupe key per message/event ID; state what happens on redelivery.
2. Use the transactional outbox pattern when a DB write and an enqueue must be atomic.
3. Configure bounded retries with exponential backoff + jitter, max attempts, and a dead-letter queue with a replay path.
4. Cron: authenticated endpoint (secret header or signed request), idempotent, overlap-safe (advisory lock or lease), timeboxed. Cron enqueues work; the queue does the work.
5. Emit metrics: queue depth, age of oldest message, processing latency, retry and DLQ rates. Alert on age, not just depth.

## Rules
- Postgres-based queues (pg-boss/graphile-worker/SKIP LOCKED) first; managed or Redis queues only when throughput demands.
- Poison messages go to the DLQ, never an infinite retry loop.

## Output
Consumer contract · Retry/DLQ policy · Overlap protection · Metrics & alerts · Failure-mode table
