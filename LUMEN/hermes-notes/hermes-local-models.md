---
name: hermes-local-models
description: "Hermes local model support — offline capability, supported backends, hardware requirements, and practical cost implications"
metadata: 
  node_type: memory
  type: project
  originSessionId: b973a205-d423-44fe-b921-622e5f45f49d
---

# Hermes — Local Model Support & Offline Use

## How "Local" Actually Works

Hermes Desktop is a **client** to local inference servers — it does not bundle inference itself. You need one of these running separately:

| Backend | Notes |
|---|---|
| **Ollama** | Most popular, easy setup |
| **LM Studio** | GUI-friendly, good for beginners |
| **vLLM** | High-performance, GPU-optimized |
| **llama.cpp** | Lightweight, CPU-capable |
| **Atomic Chat** | Supported via preset |

All connected via OpenAI-compatible endpoints. So "offline" = Hermes Desktop + one of the above servers running locally. No internet needed once set up.

## Cloud Providers Also Supported

| Provider | Notes |
|---|---|
| OpenRouter | 200–300+ models (count inconsistent across pages) |
| Anthropic | Claude models |
| OpenAI | GPT models |
| Google Gemini | — |
| xAI Grok | — |
| Nous Portal | Native OAuth, paid tiers |
| Any OpenAI-compatible endpoint | Custom / self-hosted |

## Practical Use Case: Free Unlimited Local Agent

Running Qwen 27B locally via DGX Spark = effectively **free and unlimited** inference. Alex Finn runs a cron job every 20 minutes scanning Reddit/X for business opportunities — only viable at that frequency because it's free. With cloud models (Opus/ChatGPT), the same job would cost significantly per run.

## Hardware Recommendations (June 2026)

| Hardware | Pros | Cons |
|---|---|---|
| **DGX Spark** (~$4,800) | 128 GB unified memory, plug-and-play, runs Qwen 27B + Nemotron, no monitor needed | Expensive, recently price-increased |
| **Mac Studio** (used/secondhand) | Large unified memory options, macOS UX, runs good models | Mostly sold out at higher memory configs; slower inference than Nvidia |

**DGX Spark details:**
- 128 GB unified memory → can run any model up to 128 GB
- Recommended models: Qwen 27B, Nvidia Nemotron (built with Spark in mind)
- Just plug into wall, works out of the box
- Nvidia now producing their own open-source models optimized for this hardware

**ROI framing (from Alex Finn):**
$200/mo for Claude and $4,800 for DGX Spark are investments in productivity/output, not entertainment subscriptions. If you generate 10× the value, the math works. Recommendation: prove value with the free Hermes app first, *then* invest in hardware.

## What Requires Internet vs. What Doesn't

| Action | Internet needed? |
|---|---|
| Hermes Desktop app shell (launch/UI) | Unknown — not confirmed either way |
| Local model inference (Ollama/LM Studio) | No |
| Cloud model inference (Opus, GPT, Gemini) | Yes |
| Cron job execution with local model | No |
| Nous Portal (paid tier features) | Yes |

**Why:** See [[hermes-overview]], [[hermes-pricing]]
**How to apply:** When asked "can Hermes run offline?" — answer is: yes for inference if you have local model hardware, but requires separate inference server setup. Not a single-binary offline solution.
