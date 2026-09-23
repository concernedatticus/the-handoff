---
name: auth-authz-review
description: Review authentication and authorization (OAuth/OIDC, sessions, JWT, RBAC/ABAC/ACL, RLS). Use for any change touching login, tokens, roles, permissions, or multi-tenant access.
user-invocable: true
---

# Auth & Authz Review

## Objective
Verify that identity is enforced correctly from request to data access, with no gaps.

## Procedure
1. Trace identity through every enforcement point: request → middleware → handler → query → row.
2. Check deny-by-default, tenant scoping, BOLA/IDOR, privilege escalation paths.
3. Token hygiene: `iss`/`aud`/`exp`/`nbf` validation, algorithm allow-list (RFC 8725), short-lived access, rotating refresh with reuse detection.
4. Sessions: HttpOnly, Secure, SameSite, CSRF protection, `__Host-` prefix.
5. Verify Postgres RLS policies and role separation (app role ≠ migration role ≠ read-only role).
6. Require authz matrix tests (role × resource × action) and negative tests in CI.

## Rules
- OAuth 2.1/OIDC with PKCE (RFC 9700); passkeys preferred; Argon2id if passwords.
- Centralize the policy decision point; enforce at every route AND every data access.

## Output
Enforcement map · Findings labeled blocker / should-fix / nit with file:line · Missing tests
