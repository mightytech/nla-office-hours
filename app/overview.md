# NLA Office Hours — Overview

How the pieces connect and how people use this system.

---

## What This NLA Does

NLA Office Hours is a conversational companion to a body of writing about Natural Language Applications. People come here after reading the essays and whitepapers — or instead of reading them — and explore the ideas through conversation. The NLA grounds its answers in the published articles (in `content/`) and the framework source code (at `../nla-framework/`), connecting ideas across both.

This isn't a search engine over documents. It's a thinking partner that understands the material deeply enough to synthesize answers, draw connections the articles don't make explicit, and point to the actual framework code when someone wants to see how things work.

## Tasks

| Task | What It Does | Source |
|------|-------------|--------|
| Explore | Answer questions grounded in articles and framework source | `app/explore.md` |

## How It Connects

```
content/                    The published writings
    |
    v
app/explore.md             How to answer questions
    |                       (reads articles + framework source on demand)
    v
../nla-framework/          The actual framework code
```

The explore task reads from two directions: the articles explain the ideas, the framework shows how they work in practice. Questions get grounded in whichever source is most relevant — often both.

## Skills

| Skill | Purpose | Invocation |
|-------|---------|------------|
| `/startup` | Load context and enter office hours mode | At session start |
| `/maintain` | Edit the NLA system itself | When improving the system |
| `/friction-log` | Log observations from any context | When something is worth recording |
| `/preferences` | Create or edit user preferences | When personalizing behavior |
| `/validate` | Check system consistency | When verifying the system works |
| `/install` | Install a new NLA package | When adding capabilities |
| `/update` | Pull remote changes and apply updates | When updating packages or the NLA |
| `/check-updates` | Scan for available updates | When checking what's changed upstream |
| `/export` | Export as a plugin | When preparing for distribution |
| `/think` | Collaborative design exploration | When work needs design judgment first |
| `/debrief` | Reflect on completed work | After substantive work |
| `/session-checkpoint` | Mid-session save point — preserve state, refresh context | Between work phases or before reasoning from older context |
| `/close` | Wrap up a session | When a session is ending |
| `/guide` | Context-aware help | When you need orientation |
| `/check-feedback` | Discover and triage external feedback | When checking what others have submitted |
| `/write-letter` | Draft and submit feedback to another project | After maintenance, when learnings are fresh |

## The Improvement Pipeline

1. Use the NLA — answer questions, notice what works and what doesn't
2. `/friction-log` — capture observations (unclear answers, missing articles, patterns)
3. `/maintain` — turn observations into improvements (better voice, new patterns, task refinements)

## How People Work With This

**A typical session:** Run `/startup`. The NLA loads the article index and announces what's available. Ask questions. Explore ideas. Go deeper where you're curious.

Startup loads context because the LLM starts cold — it needs to know what articles exist and how to answer questions. Close preserves state so the next session starts warm.

**The rhythm:**
- `/startup` — Load context, enter office hours
- Ask questions — The NLA answers grounded in articles and framework
- Follow threads — Go deeper on what interests you
- `/close` — When you're done

**For the maintainer:**
- Change how answers sound → edit `app/shared/voice.md`
- Change what the NLA prioritizes → edit `app/shared/values.md`
- Add new articles → drop them in `content/`
- Add new question patterns → edit `app/shared/common-patterns.md`
- Change how the NLA explores → edit `app/explore.md`

## Document Hierarchy

```
app/
├── overview.md                  This file — how the pieces connect
├── explore.md                   The task: how to answer questions
├── startup.md                   App-specific session initialization
├── config-spec.md               What's configurable
└── shared/
    ├── values.md                Commitments and priorities
    ├── voice.md                 Tone and personality
    └── common-patterns.md       Recurring question patterns
```

## Document Index

- `app/overview.md` — How the NLA works (this file)
- `app/explore.md` — Task instructions for answering questions
- `app/startup.md` — App-specific startup sequence
- `app/config-spec.md` — What users can configure
- `app/shared/values.md` — What the NLA prioritizes
- `app/shared/voice.md` — How the NLA sounds
- `app/shared/common-patterns.md` — Patterns the NLA should recognize
- `content/` — Articles and whitepapers (user-managed)
- `reference/design-rationale.md` — Why the system is built this way
- `reference/system-status.md` — Current state
- `reference/friction-log.md` — Internal observations
- `reference/feedback-log.md` — External feedback
- `reference/installed-packages.md` — Package install history

## Getting Started

1. Add your articles to `content/` (the probe report, whitepapers, future essays)
2. Start Claude Code in this directory
3. Run `/startup` — loads context and enters office hours mode
4. Ask a question
