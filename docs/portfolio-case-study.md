# Portfolio Case Study: Jarvis — A Personal AI Operating System on Hermes

## One-line summary

I built **Jarvis**, a personalized AI operating system on top of **Hermes Agent** that combines persistent memory, a git-backed Obsidian vault, reusable skills, scheduled automations, and Telegram-based execution into a practical chief-of-staff + builder workflow.

## Project snapshot

- **Project type:** Agent infrastructure / personal AI operating system
- **Core stack:** Hermes Agent, Telegram gateway, Obsidian, GitHub, cron, Python automation scripts
- **Primary role of the system:** Research assistant, execution partner, knowledge manager, and automation operator
- **What makes it interesting:** It moves beyond chat into memory, tools, delivery, and compounding operational workflows

## The problem

Most AI tools are impressive in isolated moments and forgettable over time.

They can answer questions, but they usually fail at the things that make a system genuinely useful day to day:

- remembering stable context across sessions
- turning work into reusable knowledge
- handling repeated workflows without constant re-prompting
- bridging from analysis into actual execution
- staying useful across messaging, files, repos, and scheduled tasks

I did not want another chatbot tab.
I wanted an AI operating layer that could function more like a persistent chief-of-staff and builder partner.

## The goal

Build a system that could:

- operate through Telegram, where I already work
- remember how I like to think and execute
- preserve durable context across sessions
- write into a long-term knowledge base
- accumulate reusable procedural knowledge
- run recurring jobs without manual babysitting
- safely interact with tools, repos, and external delivery channels

## What I built

Jarvis is my personalized runtime on top of Hermes Agent.

In practice, that means I combined:

### 1. A live agent runtime

The system runs on Hermes Agent and is configured with:

- primary model routing
- fallback providers
- tool access
- context compression
- checkpoints
- approval controls
- messaging gateway support

### 2. Persistent memory

I use Hermes' split memory model to separate:

- **user-profile memory** for preferences, tone, and working style
- **system memory** for environment facts, path realities, repo details, and lessons learned

That lets Jarvis remember the important things without turning permanent memory into a junk drawer.

### 3. A git-backed Obsidian vault

Instead of letting useful AI output disappear into chat history, I route work into an Obsidian vault that acts as a long-term knowledge surface for:

- reports
- research
- backlogs
- project notes
- operating context
- automation outputs

GitHub then becomes both backup and publishing infrastructure.

### 4. A skills layer

One of the most powerful pieces of Hermes is the ability to store reusable procedures as skills.

That means Jarvis does not only remember facts. It can also build up a growing library of how to do recurring tasks well, including workflows for:

- GitHub operations
- reporting
- portfolio writeups
- Hermes troubleshooting
- Google Workspace delivery
- research and QA tasks

### 5. Scheduled automation

I wired in cron-driven workflows so Jarvis can create value even when I am not actively chatting with it.

Examples from the live setup include:

- daily AI/agent brief generation
- weekly idea radar and backlog maintenance
- automatic vault git sync

### 6. Delivery bridges

The system is not trapped in a terminal.
It can bridge into:

- Telegram
- GitHub
- email attachments
- Google Docs / Calendar-related workflows

## Architecture decisions

### Why Telegram first

I wanted the system where I already think and operate, not hidden behind another local-only interface.

Telegram made Jarvis feel like an active collaborator rather than a tool I had to remember to open.

### Why Obsidian instead of a database-first knowledge layer

I optimized for:

- readability
- portability
- markdown-native workflows
- long-term ownership
- easy GitHub backup

A lot of AI systems over-index on novelty and under-index on legibility. Markdown notes in a vault are boring in the best possible way: durable, inspectable, and easy to work with.

### Why separate memory from skills

This is one of the biggest design wins in the whole system.

- **Memory** stores durable facts
- **Skills** store reusable procedures

That keeps the system cleaner, safer, and more extensible than trying to make one memory layer do everything.

### Why cron matters

A useful agent should not only react.
It should also monitor, prepare, sync, summarize, and deliver on a schedule.

That shifts the system from "assistant" to "operator."

## Proof this is a real system, not a concept deck

This repo is grounded in a live environment audit, not a hypothetical architecture.

Examples of verified proof points:

- a running Telegram gateway process
- a live Hermes install with versioned config
- a real Obsidian vault under Git
- persistent memory files with configured limits
- a substantial skills library
- stored session history
- cron job definitions and outputs
- Python helper scripts for sync, reporting, and Google Workspace delivery

I also explicitly documented what is **not** active in the current audited snapshot.
For example, the system contains migration scaffolding for `gbrain/qmd`, but those components were not active in this specific live container at audit time. I treated that honestly rather than inflating the story.

## Technical challenges

### 1. Making context durable without making it messy

The hardest part of agent systems is not raw model capability. It is deciding what should persist, where it should live, and how to keep it useful.

I solved that by separating:

- live conversation context
- durable memory
- session recall
- vault knowledge
- procedural skills

### 2. Making automation safe enough to trust

Tool-using agents are only useful if they are also controllable.

This setup includes:

- manual approvals for risky actions
- secret redaction
- explicit destructive-command caution
- non-interactive GitHub auth for unattended sync
- operational checks around stale locks and runtime drift

### 3. Turning AI output into assets instead of noise

A lot of AI-generated work evaporates because it never lands somewhere durable.

By routing work into notes, scripts, repo commits, reports, and scheduled outputs, I made the system compound over time.

## What I learned

### AI systems get much more interesting when they are treated like infrastructure

The interesting work is not just choosing a model.
It is designing the surrounding memory, tool, delivery, and knowledge architecture.

### Boring systems design beats flashy demos

Versioned markdown, scheduled sync, path discipline, process checks, and explicit delivery flows are not glamorous, but they are what turn a clever demo into a reliable system.

### Honest architecture stories are stronger than inflated ones

For portfolio work, saying "this piece is scaffolded but not active in the audited environment" is better than pretending everything is fully live.
It increases trust.

## Why this project matters to employers

This project shows that I can do more than call an LLM API.

It demonstrates:

- **product judgment** — choosing the right operating model for real use
- **systems thinking** — designing memory, skills, tools, and knowledge layers together
- **automation instincts** — building recurring workflows, not just on-demand helpers
- **operational rigor** — handling auth, state, sync, safety, and runtime details
- **clear technical communication** — documenting both capabilities and limitations honestly

If I were describing the value in one sentence:

> I built an AI system that behaves less like a novelty assistant and more like a durable operating layer for research, execution, and knowledge management.

## What I would build next

If I keep pushing this project forward, the next upgrades I would prioritize are:

- visual architecture diagrams and screenshots for faster recruiter scanning
- a public-facing demo walkthrough showing end-to-end workflows
- stronger evidence packaging around automations and outputs
- optional reactivation or modernization of the `gbrain/qmd` knowledge layer if it becomes strategically useful again

## Where to look in this repo

- `README.md` — system overview
- `docs/live-system-profile.md` — audited technical profile
- `docs/portfolio-case-study.md` — this recruiter-facing case study

## Final takeaway

Jarvis is valuable because it combines multiple layers that are usually isolated:

- model runtime
- memory
- procedural skills
- tool use
- messaging interface
- knowledge capture
- recurring automation
- versioned backup

That integration is the project.
And that integration is the skill I want this repo to showcase.
