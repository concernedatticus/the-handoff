# dev-agents-harness

Shared Mistral Vibe agent harness for the dev team. Home of **Orion** (Software Architect) and future team agents (frontend, backend, security, SRE, etc.).

## What's here

```
.vibe/
├── config.toml          # project-level Vibe config
├── agents/              # agent definitions (.toml)
├── prompts/             # full system prompts
├── skills/              # reusable SKILL.md workflows
└── knowledge/library/   # curated reference library
docs/
├── adr/                 # architecture decision records
└── architecture/        # system context, diagrams
AGENTS.md                # operating rules for ALL agents in this repo
CONTRIBUTING.md          # how agents and humans add to this repo
```

## Agents

| Agent | Role | Config |
|---|---|---|
| `orion` | Software Architect (DDD, security, performance, PM) | `.vibe/agents/orion.toml` |
| `orion-audit` | Read-only Orion for scheduled/audit jobs | `.vibe/agents/orion-audit.toml` |
| `atticus` | Backend Engineer (Aegis: auth, APIs, realtime, queues/cron, Postgres/pgvector, caching, MCP, DevOps) | `.vibe/agents/atticus.toml` |
| `atticus-audit` | Read-only Atticus for scheduled backend reviews and digests | `.vibe/agents/atticus-audit.toml` |

Run locally after cloning:

```bash
git clone git@github-penny:pennydulum/dev-agents-harness.git
cd dev-agents-harness
vibe --agent orion
# or the backend agent
vibe --agent atticus
```

## Adding a new team agent

1. Copy `.vibe/agents/orion.toml` → `<name>.toml` (keep `agent_type = "agent"`).
2. Write the full system prompt → `.vibe/prompts/<name>.md`, reference it via `system_prompt_id`.
3. Add skills under `.vibe/skills/<skill-name>/SKILL.md` (Agent Skills spec: YAML frontmatter + body).
4. Add a row to the Agents table above.
5. Update `AGENTS.md` only if the new agent changes rules for everyone.

## Layer separation (do not blur)

```
Agent prompt   = how to think
AGENTS.md      = how to operate in this repo
Skills         = how to perform repeatable tasks
Library        = what agents can look up
ADRs           = what we decided
Repository     = what actually exists
```
