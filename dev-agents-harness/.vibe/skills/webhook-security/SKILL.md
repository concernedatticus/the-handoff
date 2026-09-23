---
name: webhook-security
description: Harden webhook receivers and senders (signature verification, replay protection, dedupe, safe delivery). Use when adding any webhook endpoint or dispatching outbound events.
user-invocable: true
---

# Webhook Security

## Objective
Guarantee that only authentic, non-replayed events are processed, and that outbound delivery cannot be abused.

## Procedure
1. Inbound: verify the HMAC signature over the raw request body with constant-time comparison; never verify the parsed body.
2. Enforce a timestamp tolerance window; reject stale deliveries.
3. Dedupe by event ID (idempotent consumer); store processed IDs with a TTL.
4. Respond 2xx immediately, then process asynchronously via a queue.
5. Outbound: sign payloads (Standard Webhooks pattern), retry with exponential backoff + jitter, cap attempts, dead-letter failures with a replay UI/API.
6. SSRF-safety: resolve and block private/loopback/link-local IP ranges before delivery; per-endpoint rate limits.

## Output
Verification steps · Replay/dedupe policy · Outbound retry/DLQ policy · Test list (tampered, stale, replayed, signed)
