---
name: hermes-architecture
description: "How Hermes agents work internally — memory system, sub-agents, self-improving skills loop, session management, and execution model"
metadata: 
  node_type: memory
  type: project
  originSessionId: b973a205-d423-44fe-b921-622e5f45f49d
---

# Hermes Agent — Architecture & Behavior

## Memory System (Nous Research)

All data lives locally in `~/.hermes/`:

| Path | Purpose |
|---|---|
| `~/.hermes/memories/MEMORY.md` | Persistent agent memory across sessions |
| `~/.hermes/memories/USER.md` | User profile, preferences, context |
| `~/.hermes/state.db` | SQLite state database |
| `~/.hermes/pairing/` | Device pairing configuration |
| `~/.hermes/cron/jobs.json` | Scheduled cron job definitions (Desktop) |

Zero telemetry is claimed (self-reported, no independent audit as of June 2026).

## Self-Improving Skills Loop

- Agent creates reusable **skills** (procedural memory) after completing complex tasks
- Skills self-improve during subsequent use
- **Caveat:** High-level confirmed (3-0 adversarial vote). Specifics like "40+ built-in skills", "agentskills.io compatibility", and "5 sandbox backends" all **failed verification** (0-3 votes) — treat as marketing until hands-on confirmed

## Sub-Agents (Nous Research)

- Spawns **isolated sub-agents** with their own conversations, terminals, and Python RPC scripts
- Enables **zero-context-cost parallel pipelines** — each sub-agent has its own context, no bleed between workstreams
- Use case: building a micro-SaaS with 5–6 features → spin up one sub-agent per feature, all coding in parallel

**Sub-agent vs. Profile distinction:**
- **Sub-agents** = copies of the main agent (same skills, same personality) running multiple instances simultaneously
- **Profiles** = fully separate agents with different skill sets, memories, and personalities

Rule of thumb:
- Same skill set, multiple parallel strands → **sub-agents**
- Different skill sets needed → **separate profiles**

## Session Management

- Every conversation is its own **session** — completely isolated context
- Sessions prevent context pollution: sending a message includes everything in that thread
- A single bloated thread can 3–4× API costs vs. clean per-topic sessions
- Sessions can be pinned, organized into folders, searched

## Model Switching

- Hermes architected model selection as dynamic/runtime, not hardcoded
- New models can be swapped in the moment they drop — no waiting for app updates
- Per-task model + reasoning effort selection (e.g., minimal effort for simple tasks)
- Contrast with Claude Desktop (OpenClaw): models are hardcoded, switching requires CLI

**Why:** See [[hermes-overview]], [[hermes-features]], [[hermes-local-models]]
**How to apply:** When discussing agent performance or cost, refer to session isolation and sub-agent parallelism as the primary levers. Self-improvement claims need hands-on verification before trusting.
