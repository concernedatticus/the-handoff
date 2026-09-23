---
name: incident-response
description: Lead a structured incident response (triage, mitigation, comms, blameless postmortem). Use during live incidents or when reviewing past incidents.
user-invocable: true
---

# Incident Response

## Objective
Restore service fast, communicate clearly, and convert the incident into durable fixes.

## Procedure
1. Triage: state impact, affected tenants, and severity. Assign an incident commander; one person coordinates, others fix.
2. Stabilize before diagnosing: rollback > config revert > feature flag off > hotfix, in that order of preference.
3. Capture evidence as you go: logs, metrics, timelines, commands run, decisions made (with timestamps).
4. Communicate on a cadence: status to the team channel every N minutes with impact, actions, next update time.
5. After mitigation: verify with real checks (not assumptions), watch for secondary effects.
6. Blameless postmortem within 48h: Impact, Timeline, Cause, Mitigation, Follow-ups (each with an owner and due date). Update runbooks and ADRs.

## Rules
- Never experiment on production without stating the hypothesis and the abort condition.
- Destructive recovery steps need explicit human confirmation naming the environment.

## Output
Impact statement · Timeline · Cause · Mitigation taken · Follow-up list with owners
