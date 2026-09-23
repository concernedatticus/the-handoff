---
name: backend-api-design
description: Design or review REST/GraphQL endpoints (contracts, errors, pagination, idempotency, versioning, rate limits). Use when adding or changing an API, reviewing an OpenAPI/GraphQL schema, or debugging API behavior.
user-invocable: true
---

# Backend API Design

## Objective
Produce a concrete, reviewable API contract that is secure, idempotent, and backwards compatible.

## Procedure
1. Identify the resource, its consumers, and the auth model (who can call this, with what role/attributes).
2. Draft the OpenAPI spec (or GraphQL SDL) first, before implementation.
3. Use RFC 9457 problem+json errors, cursor pagination, and `Idempotency-Key` on all mutating endpoints.
4. Define authz per operation (role/attribute rules) and rate limits.
5. List failure modes: timeouts, retries, partial failure, replay, and what the client should do.
6. Add observability: request ID, structured logs, metrics per endpoint.

## Rules
- Validate every input and output at the boundary (zod/valibot).
- Versioning and deprecation policy explicit (`Deprecation`/`Sunset` headers).
- GraphQL: persisted queries, depth/complexity limits, DataLoader to avoid N+1, per-field authz.

## Output
Contract diff · Authz matrix · Failure modes · Test list · Rollout/deprecation plan
