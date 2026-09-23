---
name: realtime-sse-ws
description: Build or review SSE, WebSocket, webhook, push, and streaming endpoints. Use for realtime features, event delivery, webhook receivers/senders, or streaming responses.
user-invocable: true
---

# Realtime: SSE, WebSocket, Webhooks, Push, Streaming

## Objective
Deliver events reliably, authentically, and without unbounded resource use.

## Procedure
1. Pick the transport: SSE for server-to-client streams; WebSocket for bidirectional; webhooks for server-to-server; push for user devices.
2. SSE: heartbeats, honor `Last-Event-ID`, `Cache-Control: no-cache`, disable proxy buffering, mind HTTP/1.1 connection limits.
3. WebSocket: authenticate at the handshake (not after), enforce `Origin`, per-message authz, size limits, ping/pong, backpressure, reconnect with backoff and resume tokens.
4. Webhooks in: verify HMAC over the raw body (constant-time compare), timestamp tolerance, dedupe by event ID, respond 2xx fast, process async.
5. Webhooks out: signed, retried with backoff + jitter, DLQ, replay API, per-endpoint rate limits, SSRF-safe delivery (block private IP ranges).
6. Fan out via Redis/NATS/Postgres LISTEN-NOTIFY as scale requires; load-test connection counts.

## Output
Transport choice with rationale · Auth/authz points · Backpressure & reconnect behavior · Test plan
