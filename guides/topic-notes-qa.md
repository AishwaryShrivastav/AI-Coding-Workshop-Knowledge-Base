# Topic Notes — Quick Q&A

Plain-English revision notes for the whole workshop, topic by topic. Each topic has a handful of common questions with short, simple answers. Use it to refresh a concept fast.

> Answers are kept deliberately simple. For depth, see the full [guides](.) and the [programme](../curriculum/programme.md).

**Topics:** [LLMs & Transformers](#1-llms--transformers) · [Tokens & Cost](#2-tokens--token-economics) · [Prompt Engineering](#3-prompt-engineering) · [Zero/Few-Shot](#4-zero-shot--few-shot) · [Copilot & Assistants](#5-github-copilot--ai-code-assistants) · [Cursor, Claude Code & Context](#6-cursor-claude-code--project-context) · [Vibe vs Responsible](#7-vibe-coding-vs-responsible-engineering) · [AI App Builders](#8-ai-design--app-builders) · [Vision & OCR](#9-vision-models--ocr) · [Databases & MCP](#10-databases--mcp) · [Local LLMs](#11-local-llms-ollama) · [RAG](#12-rag-retrieval-augmented-generation) · [Fine-tuning & Advanced RAG](#13-fine-tuning--advanced-rag) · [Multi-Agent](#14-multi-agent-systems) · [Testing](#15-testing-ai-generated-code) · [CI/CD & Deployment](#16-cicd--deployment) · [Cost & Hardware](#17-cost--hardware) · [Automation](#18-automation-n8n)

---

## 1. LLMs & Transformers

**What is an LLM?**
A Large Language Model is a program trained on huge amounts of text. It learns patterns in language so well that it can predict what words should come next. That's how it writes answers, code, and emails.

**Is it actually "thinking"?**
No. At its core it is a very good **next-word guesser**. It has no understanding or memory of you — it just predicts the most likely next piece of text based on what it has seen.

**What is a transformer?**
It's the design (architecture) behind modern LLMs. Its key trick is **attention** — for every word, it works out which other words matter most. That's how it keeps track of meaning across a sentence or a page.

**What is a context window?**
It's the model's short-term memory — how much text it can "see" at once. Anything outside the window is forgotten. Bigger window = it can read more of your document or code in one go.

**Why does AI make things up (hallucinate)?**
Because it's guessing the most likely text, not looking up facts. If it doesn't know, it still produces a confident-sounding guess. Always verify anything important.

**When can I trust it?**
Trust it for drafts, boilerplate, and explanations you can check. Don't trust it blindly for facts, numbers, or anything safety-critical. **You own the output, not the AI.**

---

## 2. Tokens & Token Economics

**What is a token?**
A token is a chunk of text the model reads — roughly ¾ of a word in English. "Engineering" might be 2–3 tokens. Models read and bill in tokens, not words.

**What am I paying for?**
Three kinds of tokens: **input** (your prompt), **output** (the model's reply), and sometimes **thinking** tokens (the model's hidden reasoning). You pay for all of them.

**Why should I care about tokens?**
Because cost adds up fast at scale. A tool that's cheap for one user can be expensive for 10,000. Estimate token cost *before* building something big.

**What is prompt caching?**
If part of your prompt repeats every time (like a long system instruction), the model can cache it and reuse it. This can cut the cost of that repeated part by a large amount.

**How do I keep costs down?**
Send only the context you need, reuse cached prompts, pick a smaller model when it's good enough, and set spend alerts on your API dashboard.

---

## 3. Prompt Engineering

**What is prompt engineering?**
It's the skill of writing instructions that get good results from an AI. A clear, specific prompt beats a vague one every time.

**What makes a good prompt?**
Give it a **role**, the **task**, **context**, and the **format** you want back. "Fix this" is weak. "You're a Python expert. Fix this bug, explain the cause in one line, return only the corrected function" is strong.

**What is the CRISPE framework?**
A checklist for prompts: **C**apacity/role, **R**equest, **I**nsight/context, **S**pecificity, **P**ersonality/tone, **E**xperiment. It helps you not forget the important parts.

**What is chain-of-thought?**
Asking the model to "think step by step." It works through the problem in stages instead of jumping to an answer, which improves accuracy on tricky tasks.

**How do I stop it doing something I don't want?**
Use a **negative prompt** — tell it plainly what *not* to do ("do not use external libraries", "do not change the database schema").

**Why inject domain context?**
The AI doesn't know your company's rules or units. Telling it ("pressures are in bar, tags follow ISA naming") makes its output fit your real work instead of a generic guess.

---

## 4. Zero-Shot & Few-Shot

**What is zero-shot?**
You ask the AI to do a task with **no examples** — just the instruction. Great for simple, common tasks the model already understands.

**What is few-shot?**
You give the AI **2–3 examples** of input and the output you want, then ask it to do the same on new input. It copies the pattern. Use it when the task is specific or unusual.

**When does zero-shot fail?**
When the task is niche, has a strict format, or follows rules the model can't guess. Then it invents its own approach and gets it wrong.

**Why is few-shot so powerful?**
Examples teach the model your exact format and style without any training. It's the fastest way to make output match what you need.

**Can I put these prompts inside my code?**
Yes. You embed the prompt as text in your Python app and send it to the model's API. You can also inject rules and metadata into the prompt at runtime.

---

## 5. GitHub Copilot & AI Code Assistants

**What is GitHub Copilot?**
An AI helper inside your editor that suggests and writes code as you type. Think of it as autocomplete on steroids.

**What are its main modes?**
**Tab** (accept inline suggestions), **Chat** (ask questions), **Explain** (understand code), and **Fix** (repair errors). Each is useful at a different moment.

**Can it write my tests and docs?**
Yes — it's one of the best uses. Ask it to generate unit tests, docstrings, and boilerplate, then review what it produced.

**Can it convert old code?**
Yes. It's good at translating, for example, Excel VBA macros into Python. You still read and test the result.

**What's the one habit I must keep?**
**Read before you run.** Copilot is fast but sometimes wrong. Always check its code before accepting it.

---

## 6. Cursor, Claude Code & Project Context

**What is Cursor?**
A code editor with a built-in AI agent. In **agent mode** you describe a change and it edits multiple files for you, not just one line.

**What is Claude Code?**
An AI coding agent that runs in your terminal. It can read your whole project, make changes, run commands, and keep context across a session.

**What is `.cursorrules`?**
A file where you write your project's briefing for Cursor — coding style, domain rules, forbidden patterns, units. Cursor reads it every time, so it stays consistent with your project.

**What is `CLAUDE.md`?**
The same idea for Claude Code: a file describing your project structure, stack, conventions, and what the agent must never touch. It gives the agent persistent memory of your project.

**Why do these files matter so much?**
Without them, the AI guesses your conventions every session. With them, it follows your rules automatically — fewer mistakes, less repeating yourself.

**What's the difference between Cursor and Windsurf?**
Same idea — an AI-powered editor — just different products. Learn one and you understand the other.

---

## 7. Vibe Coding vs. Responsible Engineering

**What is "vibe coding"?**
Letting the AI generate code from a rough description and running it without really checking — going on the "vibe" that it works. Fine for quick demos and throwaway scripts.

**What is responsible engineering?**
Treating the AI as a junior developer: you review every change, test it, and stay accountable for the result. This is what you do for anything real or important.

**When is each okay?**
Vibe code when speed matters and mistakes are cheap (prototypes, experiments). Be responsible when correctness matters — production, customer data, safety, money.

**Who is responsible when AI code breaks?**
You are. The AI is a tool. "The AI wrote it" is never an excuse. The engineer owns the output.

**What's the single most important habit?**
**Review the diff** on every AI change — look at exactly what it changed before you accept it.

---

## 8. AI Design & App Builders

**What is Claude Design?**
A tool that turns a description into a UI prototype, wireframe, or slides. You then hand that off to Claude Code to build the real thing.

**What is Lovable?**
A tool that builds a full app — front end, database, auth — from a single prompt. Good for getting a working full-stack MVP fast.

**What's the difference between Claude Design and Lovable?**
Claude Design focuses on the **look** (UI/prototype). Lovable builds the **whole working app**. They're often used together: design first, then build.

**What are v0, Bolt, Replit?**
Other "describe it and get an app" builders. Same principle, different products. We showed them as landscape so you know the options.

**Can I keep working on what they generate?**
Yes. Export the code to GitHub and continue in Cursor or Claude Code, adding your own rules and logic.

**Are these enough for production?**
Often for an MVP, yes. For a serious production app you usually graduate to a real editor and proper testing/deployment. (See [MVP vs production](03-deployment-strategies.md).)

---

## 9. Vision Models & OCR

**What is a VLM?**
A Vision Language Model takes **images plus text** and returns structured output. You can show it a photo or diagram and ask questions about it.

**How is this different from old OCR?**
Old OCR just pulls out raw text. A VLM *understands* the image — it can read a messy diagram, find specific tags, and return clean structured data like JSON.

**What can it read?**
Things like P&ID engineering diagrams, handwritten field reports, forms, and photos. You ask for exactly the fields you want.

**Zero-shot vs few-shot for images?**
Zero-shot works for clear, standard images. For your specific naming conventions or messy handwriting, give a few examples (few-shot) so it follows your format.

**Cloud vs local for vision?**
**Gemini** (cloud) is strong and easy. **LLaVA** via Ollama runs locally for private documents. Trade accuracy and ease against privacy.

---

## 10. Databases & MCP

**What are the main database types?**
**SQL** (tables, structured data), **vector** (for AI search by meaning), and **time-series** (data over time, like sensor readings). Pick by what your data looks like.

**Can AI design my database?**
Yes. Describe your data and rules in plain English and the AI proposes an optimised schema (tables, columns, relationships). You review it.

**What is MCP?**
Model Context Protocol — a standard way to connect an AI agent to your tools and data. It's like a universal adapter so the AI can fetch live data instead of you pasting it in.

**What is the "MCP wrapper pattern"?**
You hide the database behind a set of named operations (like "get latest reading"). The agent calls those operations — it never sees or writes raw SQL. Safer and simpler.

**Why is that safer?**
The schema stays hidden and the agent can only do the specific actions you allow. It can't run arbitrary, dangerous queries.

**Why connect a live DB instead of CSV files?**
CSVs are a snapshot that goes stale. A live DB via MCP means the agent always works with current, real data — no manual exports.

---

## 11. Local LLMs (Ollama)

**What is Ollama?**
A tool that lets you download and run AI models on your own computer — no internet, no sending data away.

**Why run a model locally?**
**Privacy.** Your data never leaves your machine. Essential for sensitive or regulated information.

**What's the catch?**
Local models are smaller and weaker than the top cloud models, and you need decent hardware (enough RAM/GPU). You also maintain it yourself.

**How do I pick a local model?**
By your hardware. More VRAM means you can run a bigger, smarter model. Small machine = small model.

**Is it hard to switch from a cloud model to Ollama?**
Often no. Ollama offers an OpenAI-compatible API, so you can frequently switch by changing one URL in your code.

**What is the Continue extension?**
A VS Code extension that gives you a Copilot-like assistant powered by your local Ollama model — a private coding assistant.

---

## 12. RAG (Retrieval-Augmented Generation)

**What is RAG?**
A way to make the AI answer from *your* documents. You fetch the relevant pieces of your data and feed them to the model with the question, so it answers from facts instead of guessing.

**Why use RAG instead of just asking the model?**
The model doesn't know your private manuals or latest data. RAG grounds its answer in your actual documents, which cuts hallucination.

**What is chunking?**
Splitting documents into smaller pieces so they fit and are easy to search. You can split by fixed size or by meaning (semantic), usually with a little overlap so context isn't cut off.

**What are embeddings?**
A way to turn text into numbers that capture its meaning. Similar meanings get similar numbers, which is how the system finds relevant chunks.

**What is a vector database?**
A database built to store embeddings and quickly find the chunks closest in meaning to your question. (ChromaDB is one we used.)

**What is hybrid search?**
Combining two search styles: **vector** (by meaning) and **keyword/BM25** (exact words). Together they catch more than either alone.

**What is reranking?**
A second-pass model that re-sorts the search results so the most relevant ones go to the LLM. It sharpens accuracy.

---

## 13. Fine-Tuning & Advanced RAG

**What is fine-tuning?**
Further training a model on your own data so it specialises in your domain. Use it when you need the model to deeply "know" your style or knowledge.

**RAG or fine-tuning — which?**
**RAG** when facts change often or you just need the model to look things up. **Fine-tuning** when you need a consistent style or behaviour baked in. Many setups use both.

**What is LoRA / Q-LoRA?**
Cheap, efficient ways to fine-tune. Instead of retraining the whole model, you train small add-on pieces. Q-LoRA shrinks memory use further so it runs on smaller hardware.

**What is Graph RAG?**
RAG that uses a **knowledge graph** (connected facts) instead of flat text chunks. It's better when answers need relationships between things.

**What is multi-hop reasoning?**
When the answer needs several lookups chained together — find A, which leads to B, which gives the answer. Graph RAG handles this well.

**What does temperature do?**
Controls randomness. **Low** temperature = focused, predictable answers (good for grounded facts). **High** = more creative and varied (good for brainstorming).

---

## 14. Multi-Agent Systems

**What is an AI agent?**
An AI that *does things*, not just chats. It can use tools, call APIs, query databases, and take actions to complete a task.

**Agent vs chatbot — what's the difference?**
A chatbot answers. An agent acts — it can carry out steps, not just describe them.

**What is the "council" model?**
One **coordinator** agent receives the task and routes parts to **specialist** agents (e.g. a document agent, a data agent, a report agent). Each does its bit and the coordinator combines the results.

**Why is a council better than one big agent?**
Each specialist has a small, focused job, so it makes fewer mistakes, is easier to debug, and several can work in parallel.

**Do I need a heavy framework to build one?**
No. You can build a working multi-agent system in plain Python with an LLM API, tool definitions, and a simple loop that routes the work.

**What is a human-in-the-loop checkpoint?**
A pause where the agent must get human approval before doing something risky — like writing to a database or sending a message. It keeps a person in control.

---

## 15. Testing AI-Generated Code

**Why test AI code at all?**
Because AI code can look right and still be wrong. Tests are how you prove it actually works. You're accountable for it.

**What should I test?**
All layers: the **database**, the **APIs**, the **UI**, and the AI-generated logic itself. Cover normal cases and the awkward edge cases.

**Can AI write the tests too?**
Yes, and it's a great use — it has your code and context. Ask it for unit, integration, and edge-case tests, then review them.

**What is Playwright?**
A tool that drives a real browser like a user — clicking and typing — to test that your app works end to end. The AI can run it and you watch it test the app live.

**What are Snyk and Bandit?**
Security scanners. **Snyk** flags vulnerabilities right in your editor as you code. **Bandit** is a one-command security checker for Python.

---

## 16. CI/CD & Deployment

**What is CI/CD?**
An automated pipeline that takes your code from commit to live: **lint → test → security scan → deploy**, with no manual steps.

**What is Docker?**
A way to package your app with everything it needs, so it runs the same on any machine. "Works on my laptop" stops being a problem.

**What are GitHub Actions?**
GitHub's tool for running your pipeline automatically on every push — run tests, scan, and deploy without lifting a finger.

**How do I pick where to deploy?**
Ask four questions: scale, security, cost, and who maintains it. Then match to a platform — Streamlit/Railway/Vercel for simple, self-hosted Docker for control. (See [deployment guide](03-deployment-strategies.md).)

**What is a rollback strategy?**
A plan to undo a bad release fast — using tagged releases or blue-green deploys, so you can switch back to the working version instantly.

**How do I handle secrets like API keys?**
Never hard-code them. Put them in environment variables or the platform's secrets manager. This applies everywhere, always.

---

## 17. Cost & Hardware

**MVP or production — how do I decide?**
If a tool like Lovable gets the job done and the stakes are low, ship the MVP. Move to a proper production build when scale, reliability, or cost demand it.

**What is the KV cache?**
A speed-and-cost trick: the model reuses the work it already did on the repeated start of a prompt instead of redoing it. Big savings on prompts with a large fixed part.

**What decides which GPU I need?**
The model's size — its layers and attention heads — sets how much **VRAM** it needs. Bigger model, more VRAM.

**How do I size for many users?**
Take the model's memory need and multiply by how many sessions run at the same time. That tells you the GPU (or GPUs) required.

**Why calculate cost before building?**
Because token and GPU costs can dwarf everything else at scale. Doing the maths early stops nasty surprises later.

---

## 18. Automation (n8n)

**What is n8n?**
A workflow automation tool. You connect apps and steps visually so jobs run automatically — no manual clicking.

**What would I use it for?**
Things like: every morning, pull new data, run an AI step, and email a report — automatically, on a schedule.

**How does AI fit into n8n?**
You add an AI step into the workflow — for example, summarise incoming text or extract fields — as one part of a larger automated chain.

**How is it different from Make or Zapier?**
Same idea — connect apps and automate. n8n can be self-hosted (more control, privacy); Make and Zapier are hosted services. We taught n8n and showed the others as alternatives.

**Can I combine automation with a live database?**
Yes. An n8n workflow can read and write your live DB (via MCP or a direct connection), so the whole loop runs with real, current data.
