# Vectoree

> **"Give your coding agent a backend."**

| | |
|---|---|
| **Website** | https://vectoree.ai |
| **Docs** | https://vectoree.ai/SKILL.md |
| **GitHub** | https://github.com/VectoreeAI/vectoree-skills |
| **Classification** | `agent-native` |
| **Category** | [Agent Runtime & Infrastructure Services](README.md) |

---

## Official Website

https://vectoree.ai

---

## Official Repo

Skill pack: https://github.com/VectoreeAI/vectoree-skills

Hosted skill: https://vectoree.ai/SKILL.md

---

## How to Use (Agent Onboarding)

> **URL Onboarding — This service can be joined with a single sentence.**

Vectoree hosts a machine-readable `SKILL.md` that coding agents (Cursor, Claude Code, Codex, and others) can read and follow to install the skill, log in, link a project, and operate models / auth / Postgres / storage / Tool Hub.

**One-sentence instruction:**
```
Read https://vectoree.ai/SKILL.md and follow the instructions to connect this project.
```

**What the agent gets by reading the URL:**
- Skill install: `npx skills add VectoreeAI/vectoree-skills` (or paste `set up https://vectoree.ai/SKILL.md`)
- CLI login + project link: `npx @vectoree/cli login` → `link` → `current`
- One project key for an OpenAI-compatible model gateway plus auth, Postgres, object storage, and Tool Hub MCP
- Scene playbooks that map agent intents onto atomic `@vectoree/cli` commands

**Interaction pattern:** `URL Onboarding` ⭐ — the highest tier of agent-nativeness.

```bash
npx skills add VectoreeAI/vectoree-skills
npx @vectoree/cli login --api-url https://vectoree.ai
npx @vectoree/cli link --api-url https://vectoree.ai
npx @vectoree/cli current
```

---

## Agent Skills

**Status:** ✅ Available

```bash
npx skills add VectoreeAI/vectoree-skills
```

| Skill | What It Teaches the Agent |
|---|---|
| `vectoree` | Install / refresh the skill, CLI login+link, then operate Model Plaza, app-user auth, Postgres, object storage, and Tool Hub without inventing platform APIs |

Hosted entry point: https://vectoree.ai/SKILL.md

---

## MCP

**Status:** ⚠️ Available via Tool Hub (hosted MCP); configure from the Vectoree console after the project is linked

| Detail | Value |
|---|---|
| **MCP Repo** | Hosted via Vectoree Tool Hub (not a separate public MCP package) |
| **Transport** | Hosted MCP (Bearer project key) |
| **Compatible Clients** | Coding agents that consume MCP tools after Tool Hub connection |

Primary interfaces remain the Skill + CLI + OpenAI-compatible HTTP gateway.

---

## What It Does

Vectoree is a **backend cloud for coding agents**: models, app-user auth, Postgres, and object storage behind one project key. Agents install the Vectoree skill, log in and link a project with the CLI, then call an OpenAI-compatible gateway (`https://vectoree.ai/api/v1`) or create tables / buckets through the CLI and console.

Model Plaza reaches providers including xAI, OpenAI, Google, Anthropic, and DeepSeek (and other OpenAI-compatible endpoints) with one key. Auth covers email and Google sign-in for the agent's app users. Database is Postgres (dashboard or `vectoree db`). Storage is buckets for avatars, assets, and user content. Tool Hub lets the agent discover and connect agent-callable tools.

Pricing is pay-as-you-go for tokens with no monthly platform fee; new accounts get $5 welcome credit after CLI login and link, then Stripe top-ups into the org wallet.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | Homepage: *"Give your coding agent a backend"*; SKILL.md: *"This skill is for developers and their coding agents wiring Vectoree Cloud into an app, into Codex, or into agent tools."* — https://vectoree.ai · https://vectoree.ai/SKILL.md |
| **Agent-specific primitive** | Hosted `SKILL.md` the coding agent follows to self-provision (`login` → `link` → `current`), plus scene playbooks that map agent intents onto atomic `@vectoree/cli` commands; Tool Hub for agent-tool discovery |
| **Autonomy-compatible control plane** | After one-time human browser login/link, the agent operates via CLI and a project-scoped API key (`.vectoree/config.json` or `VECTOREE_API_KEY`); pay-as-you-go billing; skill instructs agents to stop after setup |
| **M2M integration surface** | Skill (`npx skills add VectoreeAI/vectoree-skills` / URL onboarding), CLI (`npx @vectoree/cli`), OpenAI-compatible HTTP gateway, hosted Tool Hub MCP |
| **Identity / delegation** | Per-project API keys scoped to the linked project; app-user auth is separate from developer console login; `.vectoree/` kept out of git; skill documents explicit "When NOT to use" boundaries |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Model Plaza + OpenAI-compatible gateway** | One project key across multiple model providers; chat and related modalities via `https://vectoree.ai/api/v1` |
| **App-user Auth** | Email and Google sign-in for the shipped app's users, configured in the dashboard |
| **Postgres** | Tables, schema, and SQL from the dashboard or `vectoree db` |
| **Object storage** | Buckets and uploads for avatars, assets, and user content |
| **Tool Hub** | Discover and connect agent-callable tools (including hosted MCP) |
| **Skill + CLI** | Agent-followable onboarding and atomic commands (`ai`, `auth`, `db`, `storage`, `tools`, …) |

---

## Autonomy Model

1. Agent reads https://vectoree.ai/SKILL.md (or installs `VectoreeAI/vectoree-skills`).
2. Human completes one-time browser login if needed; agent runs `npx @vectoree/cli login` then `link`.
3. Agent confirms with `current`, then uses CLI / OpenAI-compatible API / Tool Hub for the task loop without further human clicks.
4. Billing is pay-as-you-go against the org wallet; skill tells the agent to stop after setup and not invent platform APIs.

---

## Identity and Delegation Model

- Developer / coding-agent access uses a project-scoped API key after CLI link.
- App-user auth (email / Google) is a separate product surface for the shipped application's users.
- Keys live under `.vectoree/` (gitignored) or `VECTOREE_API_KEY` for headless/CI.
- Skill documents boundaries so the agent does not silently migrate unrelated MCP/API setups.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| URL Onboarding / Skill | https://vectoree.ai/SKILL.md · `npx skills add VectoreeAI/vectoree-skills` |
| CLI | `npx @vectoree/cli` (`login`, `link`, `current`, `ai`, `auth`, `db`, `storage`, `tools`, …) |
| OpenAI-compatible HTTP | `https://vectoree.ai/api/v1` with project API key |
| Tool Hub MCP | Hosted MCP tools configured after project link |

---

## Human-in-the-Loop Support

One-time human browser login/link is expected for account setup. After the project is linked, the agent operates through CLI and API without per-action human confirmation. Dashboard remains available for humans to inspect projects, billing, and Tool Hub connections.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **OpenAI API (or a single provider)** | Models only; no agent-followable Skill that also provisions auth, Postgres, and storage behind the same project key |
| **Generic BaaS (e.g. Supabase) + separate model vendor** | Human-developer wiring of multiple SDKs; agents are a secondary consumer, not the primary onboarding path |
| **Object storage alone (e.g. S3)** | No agent-native onboarding, model gateway, or app-user auth packaged for coding agents |

---

## Use Cases

- **Ship an agent-built app backend** — models + auth + Postgres + storage from one project without stitching vendors
- **Point Codex / Cursor / Claude Code at a multi-provider gateway** — OpenAI-compatible base URL and one project key
- **Agent self-provisioning** — read the skill URL, login/link via CLI, then continue the coding task autonomously
