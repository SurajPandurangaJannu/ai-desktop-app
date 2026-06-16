---
name: hermes-features
description: "Hermes Desktop/Studio feature set — profiles, cron jobs, artifacts, skills management, tool sets, group chat, and session organization"
metadata: 
  node_type: memory
  type: project
  originSessionId: b973a205-d423-44fe-b921-622e5f45f49d
---

# Hermes Desktop / Studio — Feature Reference

## Profiles

- Profiles are **fully isolated agents** — each has its own: config, cache, uploads, sessions, jobs, usage stats, memory, skills, plugins, providers, model visibility
- Can be created, renamed, deleted, cloned, and exported as `.tar.gz` archives for backup/sharing
- Switching profiles is one click in the desktop sidebar (vs. CLI command previously)
- Alex Finn's profile setup as a practical example:
  - **Hermes** (default) → Opus 4.8 — deep strategy, orchestration
  - **GPT-me's** → ChatGPT 5.5 — coding (better limits + cost)
  - **Qwen** → Qwen 27B local on DGX Spark — free unlimited quick research
  - **Librarian** → second-brain / link organization agent
  - **Coder** → coding-focused agent
  - **Oracle** → research/analysis

**Recommended profile strategy:** Organize by *model strengths* (cost, capability, limits), not by role hierarchy (PM → designer → engineer). Role-based multi-agent chains burn context through many calls; model-based switching is more efficient.

## Cron Jobs (Scheduled Tasks)

- Built-in visual cron builder — no terminal required
- Create, edit, pause, resume, and delete jobs via GUI
- Cron expression quick presets (minutes, hourly, daily, weekly, custom)
- 15 delivery targets supported
- Jobs persisted in `~/.hermes/cron/jobs.json`
- Confirmation of job creation visible in UI — previously unverifiable via Telegram/CLI

**Best practice — "Brain dump → Reverse prompt":**
Instead of writing a generic cron prompt, brain-dump your interests/context to the agent then ask: *"Based on what you know about me, what's the best prompt for this cron job?"* Produces far more precise, well-formatted, reliable outputs. Example result: formatted daily brief with 24-hour recency enforcement, bold headers, section-specific instructions per topic.

## Artifacts

- Centralizes all **images, files, and links** generated or received across all sessions
- Searchable by keyword (e.g., search "Reddit" to see all Reddit links sent to any agent)
- Replaces manual "second brain" maintenance — just drop links into a Librarian agent, artifacts auto-organizes them
- No need to instruct the agent to "file this" — passive accumulation

## Skills Management

- GUI to view all 150+ installed skills per profile
- Toggle skills on/off to reduce context overhead and save money
- New skills are auto-generated in the background as you work (e.g., "3.js one-file game", "YouTube new scripts", "real-time stock dashboard")
- Many users don't realize skills accumulate silently — turning off irrelevant ones reduces cost

## Tool Sets

- Groups of multiple skills/tools combined for complex tasks
- New concept (as of June 2026) — still evolving
- Useful for bundling related capabilities for a specific workflow

## Group Chat / Multi-Agent Rooms (Studio)

- Multi-agent chat rooms with real-time messaging via Socket.IO
- `@mention` routing directs messages to specific agents within a room
- Enables collaborative multi-agent workflows without separate sessions

## Context Window Visibility

- Real-time context window usage displayed at the bottom of the UI
- Prompt `/new` to start a fresh session and clear context when it fills up

**Why:** See [[hermes-architecture]] for sub-agents, [[hermes-pricing]] for cost-saving implications
**How to apply:** When recommending Hermes workflows, lead with profiles + sessions + cron as the three highest-leverage features for productivity and cost control.
