---
name: hermes-overview
description: "What Hermes AI agents are — two distinct open-source projects sharing the name, their origins, licensing, and high-level purpose"
metadata: 
  node_type: memory
  type: project
  originSessionId: b973a205-d423-44fe-b921-622e5f45f49d
---

# Hermes AI Agents — Overview

## Critical Disambiguation: Two Separate Projects

"Hermes" refers to **two unrelated open-source projects** sharing the same name. It is unknown if they coordinate.

| | **Hermes Agent** | **Hermes Desktop / Studio** |
|---|---|---|
| **By** | Nous Research | fathah (desktop) / EKKOLearnAI (studio) — community |
| **GitHub** | github.com/NousResearch/hermes-agent | github.com/fathah/hermes-desktop · github.com/EKKOLearnAI/hermes-studio |
| **Official site** | hermes-agent.nousresearch.com | — |
| **License** | MIT | MIT |
| **Type** | Framework / CLI / backend engine | Electron desktop GUI application |
| **Primary focus** | Self-improving agent engine with persistent memory | UX shell wrapping agent capabilities |
| **Distribution** | CLI, self-hostable on VPS/cloud/serverless | .dmg / .deb / AppImage / .zip / Docker / npm |
| **Pricing** | Free core + paid tiers (Plus, Super, Ultra) | Fully free and open-source |

## What They Are

**Hermes Agent (Nous Research):** An autonomous agent framework built around a local-first, self-improving design. The agent lives on your infrastructure (`~/.hermes/`), persists memory across sessions, learns skills from experience, spawns isolated sub-agents for parallel work, and supports any OpenAI-compatible LLM provider. Core is open-source; paid tiers add API credits and access to 300+ hosted models via Nous Portal.

**Hermes Desktop / Studio:** A polished Electron desktop application that makes agent capabilities accessible without a CLI. Provides a GUI for profile management, session organization, cron job scheduling, artifact browsing, and local/cloud model switching. Latest version: v0.6.15 (June 15, 2026). Active maintenance confirmed.

## Context from Practitioner Use (Alex Finn, June 2026)

Alex Finn — previously known as a heavy Claude (OpenClaw) user — switched to Hermes Desktop as his primary agent interface, describing it as the "Apple route" vs Claude's "Android route": focused, polished, user-tested updates vs. unfocused shotgun releases. He runs it daily for business opportunity scanning, content workflows, and cron-automated research.

**Why:** See [[hermes-architecture]], [[hermes-features]], [[hermes-pros-cons]]
**How to apply:** When the user references "Hermes" in context of agents/automation, clarify which project they mean if ambiguous. Default to Hermes Desktop/Studio for GUI/UX questions and NousResearch for framework/architecture questions.
