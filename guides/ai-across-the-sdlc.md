# AI-Assisted Coding Across the SDLC

**Question:** A complete guide to using AI across the whole Software Development Life Cycle (SDLC).

**Short answer:** Don't use AI only to write code. Use it at *every* stage — from understanding the problem to keeping the product healthy after launch. When you wire AI into every step like this, the whole setup is often called a **harness**.

---

## The idea in one line

The SDLC has five main stages: **Analysis → Design → Development → Testing → Maintenance.**

Most people only use AI in *Development* (writing code). The real win is injecting AI into all five stages, and into the small steps in between.

```
Analysis  →  Design  →  Development  →  Testing  →  Maintenance
   ↑                                                      │
   └──────────────  feedback loops back  ─────────────────┘
```

The arrow back from Maintenance to Analysis is the important part: user feedback and analytics feed the next round of work. The loop never really stops.

---

## 1. Analysis (understand the problem)

This is requirement gathering and figuring out *what* to build.

- **Brainstorm with AI**, don't just brainstorm alone. Describe the problem and ask for angles you may have missed.
- **Ask AI to interview you.** This is the trick most people skip. Instead of you writing requirements from a blank page, tell the AI: *"Interview me about this product. Ask one question at a time until you have enough to write a clear spec."* Its questions pull out context and decisions you hadn't thought about.
- The output of this stage is a clear **spec / PRD** (Product Requirements Document) that the next stages build on.

> **Why it works:** A vague idea in your head becomes a structured document, and the gaps get found *before* you write any code — when they are cheap to fix.

---

## 2. Design

Now decide what it looks like and how it is structured. Two parts here:

### a) UI / product design

Tools that turn a description into a working UI, prototype, or MVP:

- **Claude Design** — prompt to UI prototype, wireframe, or slides. Hands off cleanly to Claude Code for implementation.
- **Figma (with AI features)** — design-first teams.
- **Lovable / v0 / Bolt** — describe an app, get a working front end (and sometimes full stack).

Use these to get a clickable prototype or MVP early, so people can react to something real instead of a paragraph.

### b) Architecture design

Before coding, design *how the solution is put together* — the data flow, the components, the APIs.

- You can do this **outside the editor** (in a chat) or **inside the editor** (Cursor, Claude Code).
- **Recommendation: do it inside the code editor.** There the AI can see your actual files and existing code, so its architecture advice fits your real project instead of a generic answer.

---

## 3. Development

Writing the code. This is where most people already use AI (Copilot, Cursor, Claude Code).

- Feed the AI the spec from Analysis and the design from Design. It already has the codebase; give it the *product context* too.
- Treat the AI like a **junior engineer**: it is fast, but **you own the output.** Read every change before you accept it.

> See [vibe coding vs. responsible engineering](../revision/topic-notes.md#7-vibe-coding-vs-responsible-engineering) for when to move fast and when to slow down and verify.

---

## 4. Testing

This is now one of the most important places to use AI — not an afterthought.

**Strong recommendation: let AI write and run your tests.** Your AI assistant has both the code *and* the product context, so it can generate meaningful tests, not just trivial ones.

Cover all the layers:

| Layer | What to test |
|---|---|
| **Database** | Data goes in and comes out correctly; constraints hold |
| **API** | Endpoints return the right thing for good and bad input |
| **UI** | The screens actually work for a real user |
| **The AI code itself** | The AI-generated logic does what the spec said |

**Browser testing with Playwright:** You can ask the AI to spin up a browser and test the app like a real user — clicking, typing, checking results. You literally watch the AI drive the browser and confirm the app works.

---

## 5. Maintenance

After launch, the product has to stay healthy and keep improving.

- **Gather user feedback** and let AI summarise themes from it.
- **Gather usage analytics** and let AI spot patterns (what's used, what's broken, what's slow).
- **Pipe that back to Analysis.** The feedback becomes the input for the next round of requirements — closing the loop.

---

## Putting it together: the harness

When you inject AI at *every* stage of the cycle — and the small steps between them — the whole arrangement is called a **harness**.

The point of a harness is not "AI writes my code." It's that AI is present from the first question to the last user-feedback loop, and a human stays accountable at each handoff.

| Stage | What AI does | What stays human |
|---|---|---|
| Analysis | Interviews you, drafts the spec | Deciding what matters |
| Design | Generates UI + architecture options | Choosing the approach |
| Development | Writes code from spec + context | Reviewing every change |
| Testing | Writes and runs DB/API/UI/browser tests | Defining "correct" |
| Maintenance | Summarises feedback + analytics | Deciding what to fix next |
