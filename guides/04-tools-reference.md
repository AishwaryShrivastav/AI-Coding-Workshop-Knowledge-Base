# Tools Reference Table

**Question:** A single table of every tool discussed in the workshop, grouped by category, with the main tool we used and the alternatives.

**How to read this:** For each job there's a **Primary** (what we taught and used in labs) and **Alternatives** (shown as landscape, same idea, different product). Pick the primary unless you have a specific reason to switch.

---

## By category

| Category | What it's for | Primary | Alternatives |
|---|---|---|---|
| **Code assistant (in-IDE)** | AI that completes and edits code as you work | **GitHub Copilot** | Continue (for local models) |
| **AI code editor / agent** | Editor where an AI agent edits many files from a description | **Cursor** | Windsurf, Antigravity |
| **Agentic CLI** | AI coding agent in the terminal, persistent project context | **Claude Code (CLI)** | — |
| **UI / design generation** | Describe it → get a UI prototype, wireframe, or slides | **Claude Design** | Figma (AI), v0, Bolt |
| **Frontend** | The user-facing app | **Lovable** (generates React) | Streamlit (for data UIs) |
| **Full-stack / backend** | App + database + auth from a prompt | **Lovable** (React + Supabase + auth) | Replit |
| **Database** | Where data lives | **Supabase** (SQL) | ChromaDB (vector), time-series DBs |
| **Context layer** | How the AI safely reaches your data and rules | **MCP** (Model Context Protocol) | `.cursorrules`, `CLAUDE.md` (project rules) |
| **Local LLM runtime** | Run models offline on your own machine | **Ollama** | Hugging Face (self-host) |
| **LLM providers** | The models themselves, via API | **Anthropic (Claude)** | OpenAI (ChatGPT), Google (Gemini) |
| **Vision / OCR (VLM)** | Read images, diagrams, handwriting → structured data | **Gemini VLM** | LLaVA (local, via Ollama) |
| **RAG framework** | Search your documents to ground answers | **LangChain** | — |
| **Embeddings** | Turn text into vectors for search | **nomic-embed-text** (via Ollama) | provider embedding APIs |
| **Reranking** | Second-pass model to sharpen search results | **bge-reranker** | — |
| **Workflow automation** | Connect apps, run jobs automatically | **n8n** | Make, Zapier |
| **Office automation** | AI inside docs/sheets/email | **Google Workspace AI** | — |
| **Testing (functional)** | Unit, integration, edge-case tests | **pytest** | — |
| **Testing (browser)** | Drive a real browser like a user | **Playwright** | — |
| **Security scanning** | Catch vulnerabilities in code | **Snyk** (live in IDE) | Bandit (Python linter) |
| **Deployment — data app** | Host a dashboard or demo | **Streamlit Cloud** | Hugging Face Spaces |
| **Deployment — frontend** | Host a web front end | **Vercel** | — |
| **Deployment — full app** | Host app + database | **Railway** | Render |
| **Deployment — self-host** | Full control, sensitive data | **Docker** | Kubernetes (at scale) |
| **CI/CD** | Automate lint → test → scan → deploy | **GitHub Actions** | — |
| **Version control** | Track code, collaborate | **GitHub** | — |

---

## Paid vs. free

From the workshop setup:

- **Paid subscriptions used:** Claude Max · Cursor Pro · GitHub Copilot.
- **Everything else** in the table is free or has a usable free tier.

---

## Categories to confirm / add later

These were asked about but were **not** covered in depth in the 5-day workshop. Leaving them open so we fill them with what we actually recommend, not a guess:

| Category | Status |
|---|---|
| **Email verification** | Not covered in the workshop — to be added. |

> If you want a recommendation for email verification (or any other category), add it to the [Q&A](../qna/README.md) and we'll research and slot it in here.
