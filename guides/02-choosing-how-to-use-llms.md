# Choosing How to Use an LLM

**Question:** A framework for picking the right way to use an LLM — through an API, downloaded locally, or via Hugging Face — based on business needs, security, technical limits, and scale.

**Honest answer up front:** There is no single "correct" framework. There are a few clear *ways* to get an LLM, each with real trade-offs. Once you understand the trade-offs, the right choice for a given project becomes obvious.

---

## The three ways to use an LLM

### 1. Provider API (the brand's own service)

You use the model straight from the company that made it — OpenAI (ChatGPT), Anthropic (Claude), Google (Gemini). You get an API key and call their service.

- **They handle the hard parts** — the servers, the GPUs, scaling, updates. You just send a request.
- **They see your data.** Your prompts travel to their servers. (Most offer business/enterprise tiers with stronger data promises — check those if data is sensitive.)
- **Best capability, least effort.** These are usually the strongest models and the fastest way to start.

### 2. Local download (run it on your own machine)

You download the model weights and run them on your own hardware — **Ollama** is the easiest way to do this.

- **Your data never leaves your machine.** This is the big reason to choose local: sensitive or regulated data.
- **You own the hardware problem.** You need enough GPU/RAM, and you maintain it.
- **Smaller, weaker models** than the top provider APIs — but good enough for many tasks, and getting better fast.
- Bonus: Ollama exposes an **OpenAI-compatible API**, so you can often switch from a cloud model to a local one by changing one URL.

### 3. Hugging Face (the open-model hub)

Hugging Face is the main place to find and download open models. Think of it as the "app store" for open-source LLMs.

- **Huge choice** — thousands of models, many free, each tuned for different jobs (chat, code, embeddings, vision, etc.).
- You can **download and self-host** them (similar to local), or use Hugging Face's **hosted inference** if you don't want to manage hardware.
- **More setup and know-how** than a provider API. You pick the model, the hosting, and the tuning.

> Key point: **every model has its own strengths.** A small code model can beat a huge general model at code, and vice versa. Don't assume "biggest = best for my task."

---

## How to choose: five questions

Ask these about the specific project. Your answers point to the option.

| Question | If the answer is… | Lean toward… |
|---|---|---|
| **1. How sensitive is the data?** | Highly sensitive / regulated, must not leave premises | **Local** (or self-hosted Hugging Face) |
| | Normal business data | **Provider API** (use an enterprise tier) |
| **2. How good must the answers be?** | Cutting-edge reasoning, hardest tasks | **Provider API** |
| | "Good enough" for a focused task | **Local / open model** |
| **3. What's the scale & cost?** | Spiky or low volume | **Provider API** (pay per use) |
| | Huge, steady volume | **Local / self-host** (own hardware can be cheaper at scale) |
| **4. What's your team's capacity?** | Small team, want speed | **Provider API** (least to manage) |
| | Have ML/infra skills | **Local / Hugging Face** |
| **5. How much control do you need?** | Need to fine-tune, fully own the model | **Hugging Face / local** |
| | Happy with what the provider offers | **Provider API** |

---

## Quick comparison

| | Provider API | Local (Ollama) | Hugging Face |
|---|---|---|---|
| Data privacy | Leaves your machine | Stays private | Private if self-hosted |
| Setup effort | Lowest | Medium | Highest |
| Model strength | Highest | Lower | Varies widely |
| Cost model | Pay per token | Hardware + electricity | Hardware, or pay per use |
| Best for | Fast start, top quality | Sensitive data | Choice + control |

---

## Rule of thumb

- **Starting out, or need the best quality, normal data?** → Provider API.
- **Sensitive data that can't leave the building?** → Local with Ollama.
- **Need many specialised models, or want to fine-tune and fully control?** → Hugging Face.

These are not exclusive. A common real setup is: **provider API for hard reasoning + a local model for the private, high-volume parts.**

> Related: cost at scale connects to [deployment strategies](03-deployment-strategies.md) (GPU sizing, KV cache, prompt caching).
