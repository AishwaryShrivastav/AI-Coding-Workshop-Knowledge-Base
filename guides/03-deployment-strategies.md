# Deployment Strategies and Platform Selection

**Question:** A guide to deploying AI apps, regular apps, APIs, agentic systems, and enterprise solutions — and how to pick the right platform based on scale, security, cost, performance, and operations.

**Short answer:** First figure out *what kind of thing* you're shipping. Then answer four questions about it. The answers point to a platform.

---

## Step 1: What are you deploying?

The type of app changes the right platform.

| Type | What it is | Typical platforms |
|---|---|---|
| **Simple data/AI app** | A dashboard, a demo, an internal tool | **Streamlit Cloud**, Hugging Face Spaces |
| **Full web app** | Front end + back end + database | **Railway**, **Vercel** (front end), Render |
| **API / service** | Code other systems call | Railway, Fly.io, **Docker** on a cloud VM |
| **Agentic system** | Long-running agents, tools, queues | Self-hosted **Docker**, a cloud VM/container service |
| **Enterprise** | Strict security, on-prem or private cloud | Self-hosted Docker / Kubernetes, private cloud |

---

## Step 2: The 4-question framework

Ask these about the specific project. They decide the platform.

**1. Scale — how many users / how much traffic?**
- Few users, internal → managed platform (Streamlit, Railway). Don't over-build.
- Large or spiky → a platform that auto-scales, or your own containers behind a load balancer.

**2. Security — how sensitive is the data?**
- Normal → managed cloud is fine.
- Sensitive / regulated → self-hosted Docker on infrastructure you control, possibly on-prem. Pairs with a [local LLM](02-choosing-how-to-use-llms.md).

**3. Cost — what's the budget and usage pattern?**
- Low or bursty traffic → pay-per-use / free tiers (Streamlit Cloud, Vercel hobby).
- Steady, heavy traffic → your own server can be cheaper than per-use pricing.

**4. Performance & operations — how fast must it be, and who maintains it?**
- Need it simple, small team → managed platform (less to run).
- Need fine control, have the skills → self-hosted Docker / Kubernetes.

> The honest default: **start on the simplest managed platform that fits, and only move to self-hosting when scale, cost, or security forces you to.** Don't build Kubernetes for ten users.

---

## Step 3: Things that apply to every deployment

### Secrets and environment variables
Never hard-code API keys or passwords. Keep them in **environment variables** or the platform's secrets manager. This is non-negotiable, on every platform.

### CI/CD (automate the path to production)
Set up a pipeline so every change goes: **lint → test → security scan → deploy.**
- **Docker** to package the app the same way everywhere.
- **GitHub Actions** to run the pipeline on every push.
- A **rollback plan**: tagged releases or blue-green deploys, so a bad release can be reversed fast.

---

## Extra concerns for AI apps specifically

If you're hosting your *own* LLM (not just calling a provider API), the cost and hardware maths matters.

- **MVP vs. production:** A tool like Lovable may be all an MVP needs. Calculate the **token cost in production** *before* you build at scale — it can be the biggest line item.
- **Prompt caching / KV cache:** Reusing the cached prefix of a prompt can cut cost dramatically (often ~90% on the repeated part). Use it for anything with a large, repeated system prompt or context.
- **GPU sizing:** A model's size (its layers and heads) sets how much **VRAM** it needs. That, plus how many sessions run at once, decides the GPU you need. Size this before committing to self-hosting an LLM.

---

## Quick chooser

| Situation | Start with |
|---|---|
| Internal dashboard / demo | Streamlit Cloud |
| Front end of a web app | Vercel |
| Full app with a database | Railway |
| API or background service | Docker on a cloud VM |
| Sensitive data, full control | Self-hosted Docker / on-prem |
| Long-running agents | Self-hosted Docker / container service |
