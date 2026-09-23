---
name: caching-layers
description: Design caching across browser, CDN, app, and data layers with correct headers, keys, invalidation, and stampede protection. Use when tuning performance, setting Cache-Control, or debugging stale/incorrect content.
user-invocable: true
---

# Caching Layers

## Objective
Cache the right things at the right layer, without serving stale or cross-user data.

## Procedure
1. Classify content: immutable / shared-public / per-user / sensitive. Sensitive and authenticated responses never hit shared caches without explicit keys.
2. Set headers: `Cache-Control` with `s-maxage`, `stale-while-revalidate`, `stale-if-error`; fingerprinted assets get `immutable` + long max-age; set `Vary` correctly.
3. Choose invalidation: versioned keys > tag/surrogate-key purge > short TTL + SWR. Prefer boring over clever.
4. App layer: in-memory LRU first, Redis/KV when shared across instances.
5. Add stampede protection: request coalescing, jittered TTLs, single-flight locks.
6. Measure hit ratio per layer before and after.

## Output
Content classification table · Header/invalidation plan per layer · Stampede guards · Hit-ratio evidence
