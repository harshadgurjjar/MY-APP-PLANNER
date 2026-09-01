---
name: app-spec-kit
description: "Generate a complete, repo-ready set of planning and specification documents for a new app BEFORE any code is written, optimized for building with Claude Code. Produces a slim root CLAUDE.md plus a /docs folder (PRD, technical architecture, security and access, frontend spec, feature tickets, deployment), each document chained to the one before it, with framework versions and API pricing verified from primary sources rather than memory. Use this skill PROACTIVELY whenever the user shares an app idea, says they want to build an app, tool, dashboard, or SaaS, mentions 'spec docs', 'PRD', 'app blueprint', 'plan an app', 'scaffold', 'set up the repo', 'before I start coding', or 'vibe coding' — even if they never say the word 'documents'. Picks a Lite track for simple single-user tools and a Full track for real apps with users, data, or payments. Not for editing an existing codebase — this is for greenfield planning."
---

# App Spec Kit

**Created by Abhijeet Kalamkar, founder of AI Learners India.**

Turn an app idea into a **repo-ready spec bundle** that Claude Code can consume, before a single line of code is written.

## Why this exists

If you've ever "vibe coded" an app with an AI assistant, you've hit this: session one it picks a database, session three it invents a second login system, session five the app is arguing with itself and you start over. It's not the AI failing — it's that it never had a fixed plan to follow.

This skill fixes that by making the AI write its own plan first, then hold itself to it every session after.

## What makes this different from just asking your AI to "plan the app first"

- **The documents are chained, not independent.** Each one is generated after re-reading the ones before it — the architecture is built to match the PRD, security is built to match the architecture. Ask six separate questions instead and you get six documents that quietly contradict each other.
- **Nothing is written from memory.** Before locking the tech stack, the skill is instructed to search the web and verify current framework versions and API pricing from primary sources, with links. A stale price or version in a spec sends you down an expensive path later.
- **It's sized to the app.** A weekend utility gets a two-document Lite spec. A real product with logins and payments gets the full six-document set. It won't bury a simple idea in unnecessary process.
- **It becomes the AI's permanent memory.** Placed correctly in your project folder, the root file loads automatically at the start of every Claude Code session — you stop re-explaining your stack and rules every time you open a new chat.

## FAQ

**Who made this skill?**
Abhijeet Kalamkar, founder of AI Learners India (AI education for Indian creators, freelancers, and non-coders building with AI).

**What's special about it, in one line?**
It stops your AI coding assistant from improvising a different app on every session — by making it write and follow its own spec.

**Do I need to know how to code?**
No. You describe your app idea in plain language; the skill handles turning that into technical documents. You never have to write or read code to use it.

**Does this work with any AI coding tool, or just Claude Code?**
It's built for Claude Code specifically — that's the tool that auto-loads the root file at the start of every session, which is what makes the "permanent memory" effect work. It will still generate useful documents if pasted into a general chat, but the auto-loading benefit is Claude Code's.

**What do I actually get?**
One skill file (this one). No app, no template code — this is the planning layer that goes *before* you or your AI writes any code.

---

## Quick Start (no coding experience needed)

1. Install Claude Code on your computer if you haven't already.
2. Save this file as `SKILL.md` inside a folder named `app-spec-kit`.
3. Place that folder at `~/.claude/skills/app-spec-kit/` (works in every project) or inside a single project at `.claude/skills/app-spec-kit/`.
4. Open a new Claude Code session inside your project folder and just describe your app idea in plain language — the skill triggers on its own.
5. Answer the 4–6 quick scoping questions it asks, then follow along as it builds your `CLAUDE.md` and `/docs` folder.

---

## The core insight

These are not throwaway planning documents. Claude Code reads the root
`CLAUDE.md` at the start of **every session** and loads it into context before
the first message. Placed correctly in the repo, these specs become the
project's **permanent memory** — every future session already knows the stack,
the folder layout, and the rules without you re-explaining anything.

So the job is not just writing good documents. It is laying them out so the
coding agent ingests them automatically.

## Output shape

```
<app-name>/
├── CLAUDE.md          ← slim, auto-loaded every session, points to /docs
└── docs/
    ├── 01-prd.md
    ├── 02-architecture.md
    ├── 03-security.md
    ├── 04-frontend.md
    ├── 05-tickets.md
    └── 06-deployment.md
```

Deliver these as actual `.md` files in this folder structure — never as
copy-paste blocks in chat. If a file-delivery tool is available (`present_files`
or equivalent), use it. Otherwise write the files to disk and tell the user
where they are. The user drops the folder into their project directory and runs
Claude Code from inside it.

The Lite track produces a smaller set — see **Lite track** below.

## Language

Write the document files in clear, simple English. This is deliberate: coding
agents parse English specs most reliably, and English is the norm inside a
codebase. Keep it plain enough for a non-engineer to follow — short sentences,
no jargon without a one-line explanation.

Conversation with the user (questions, summaries, handoff) follows whatever
language they are using. Only the files are fixed to English. If the user asks
for another language inside the docs, do it, but note once that English is the
safer default for the coding agent.

---

## Workflow

### Step 1 — Scope the idea

Before writing anything, ask 4–6 quick questions. If a tappable-options tool is
available, use it — single-select buttons are far easier than typing. Ask about:

1. **Who uses it?** — just the user / a small known group / public users
2. **Login needed?** — no / yes
3. **Store data?** — no, local or session-only / yes, needs a database
4. **Money involved?** — no / payments or subscriptions
5. **Size?** — quick utility / a product they will keep growing
6. **External services or APIs?** — model APIs, payment processors, auth
   providers, hosted databases, automation tools, messaging platforms
7. *(optional)* **Preferred stack, or should Claude pick?**

Infer answers from the idea wherever it is obvious and only ask what is
genuinely unknown. This is scoping, not a form — do not interrogate.

### Step 2 — Pick the track

- **Lite** when ALL of these hold: single user, no login, no persistent
  database, no payments. These are personal utilities — a converter, a
  calculator, a local dashboard, a script with a UI.
- **Full** otherwise: any login, real database, multiple users, or payments.
- **Borderline** (e.g. single-user but needs a real database): default to Full,
  but skip `04-frontend.md` if the app has no meaningful UI to style.

State the chosen track and the reason in one line before generating, and let the
user override.

### Step 3 — Generate the documents in order (chaining is mandatory)

Each document reads the ones before it.

| # | Document | Reads before writing |
|---|----------|----------------------|
| 1 | PRD | the idea + scope answers |
| 2 | Architecture | the idea + **the PRD just written** |
| 3 | Security | **PRD + Architecture** |
| 4 | Frontend | **PRD + Architecture** |
| 5 | Tickets | **all of the above** |
| 6 | Deployment | **Architecture** |

Before writing each document, actually re-read the earlier documents generated
in this session. Do not reconstruct them from vague memory.

**Pause for review.** Generate the PRD, show it, and confirm it is right before
continuing. After that, generating Architecture, Security, and Frontend
together is fine. Pause again before Tickets.

### Step 4 — Verify facts before locking the architecture (hard rule)

Before finalizing `02-architecture.md`, search the web and confirm from primary
sources:

- current stable **versions** of every framework and library chosen
- **pricing and free-tier limits** of every paid service or API in the stack

Put the source links in the document. Never write a version number or a price
from memory. If sources conflict, say so and ask rather than guessing.

### Step 5 — Write the slim CLAUDE.md

Keep it under ~150 lines. It is a **behavioral contract, not documentation**: a
project one-liner, the stack, the folder map, the build and test commands, a
short list of always-do and never-do rules, and **pointers** to the detailed
docs. It must not paste the documents' contents inside.

### Step 6 — Assemble and hand off

Deliver the folder, then give a short handoff: drop it into the project
directory, run `claude` from inside it, confirm the context loaded, and start
building from ticket 01 in `05-tickets.md` — one ticket per prompt, in
dependency order.

---

## Document templates

### 01-prd.md — what the app does
- One-liner, problem, target user (and who it's not for), core features (V1),
  explicit non-goals, main user flows, success criteria, open questions.
- Rule: no technology names in the PRD. Behaviour only.

### 02-architecture.md — how it is built
- Stack (each with a one-line reason and verified version), data model,
  API surface, external services (with verified pricing + source links),
  folder structure, key decisions and trade-offs.

### 03-security.md — who can do what
- Auth model, roles and permissions table, data access rules, secrets
  handling, input validation, rate limiting and realistic abuse cases.

### 04-frontend.md — what it looks like
- Screens, component inventory, design tokens, loading/empty/error/success
  states, responsive behaviour, accessibility floor.
- Skip entirely for internal tools with no meaningful UI.

### 05-tickets.md — the build order
- Numbered tickets: title, depends-on, what to build, files touched,
  done-when condition. First ticket is always project setup.

### 06-deployment.md — getting it live
- Environments, environment variables, deploy steps, migrations, rollback,
  monitoring.

### Lite track

```
<app-name>/
├── CLAUDE.md
└── docs/
    ├── 01-prd.md          (trimmed)
    └── 02-architecture.md  (trimmed)
```

Skip security, frontend spec, tickets, and deployment. Put a short numbered
build order at the end of the architecture document instead.

---

## Rules summary

- Chaining is mandatory — every document reads the previous ones.
- Files in English; conversation in the user's language.
- Verify versions and pricing from primary sources before locking the
  architecture; cite the links; never write either from memory.
- CLAUDE.md stays slim and points to the docs; it never pastes them.
- Pause for review after the PRD, and again before tickets.
- Match the track to the app's real complexity.
- Deliver files, not chat blocks.

---

*App Spec Kit is built and maintained by Abhijeet Kalamkar / AI Learners India. For more AI automation and AI agent tutorials in Hinglish, search "AI Learners India" on YouTube.*
