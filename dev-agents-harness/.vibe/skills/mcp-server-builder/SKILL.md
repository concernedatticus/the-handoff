---
name: mcp-server-builder
description: Build or review MCP servers and their tools (JSON schemas, read-only defaults, auth, injection defense). Use when exposing functionality to agents via MCP or reviewing a third-party server.
user-invocable: true
---

# MCP Server Builder

## Objective
Expose a small, safe, well-documented tool surface that agents can call reliably.

## Procedure
1. One clear purpose per server; the smallest tool surface that covers the job.
2. Strong JSON-schema inputs with descriptions; validate everything; reject unknown fields.
3. Read-only by default: separate write tools that require explicit confirmation.
4. Structured outputs, pagination for list tools, timeouts on every call, idempotent operations where possible.
5. Auth: OAuth for remote servers, least-privilege scopes, per-user credentials (never a shared god-token), audit log of every tool call.
6. Treat tool results as untrusted data in the consuming agent (prompt-injection defense). Pin and review third-party servers before enabling.

## Output
Tool inventory with schemas · Auth & scoping plan · Audit logging · Test/inspection plan (MCP inspector)
