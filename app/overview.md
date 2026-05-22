# NLA Office Hours — Overview

How the pieces connect and how people use this system.

---

## What This NLA Does

NLA Office Hours is a conversational companion to a body of writing about Natural Language Applications. People come here after reading the essays and whitepapers — or instead of reading them — and explore the ideas through conversation. The NLA grounds its answers in three kinds of material: the published articles (in `content/`), the framework source code (at `packages/nla-framework/`), and a small collection of example NLAs (in `examples/`) that serve as concrete working evidence of how the framework plays out in practice.

This isn't a search engine over documents. It's a thinking partner that understands the material deeply enough to synthesize answers, draw connections the articles don't make explicit, and point to the actual framework code — or to a specific example NLA — when someone wants to see how things work.

## Tasks

| Task | What It Does | Source |
|------|-------------|--------|
| Explore | Answer questions grounded in articles, framework source, and example NLAs | `app/explore.md` |

## How It Connects

```
content/                    The published writings
    |
    v
app/explore.md             How to answer questions
    |                       (reads articles + framework source + examples on demand)
    +-------> packages/nla-framework/   The framework source (git submodule)
    |
    +-------> examples/                 Working NLAs (git submodules):
                                          - copydesk (editorial workflow)
                                          - duet (creative composition)
                                          - nla-claude-code (dev tooling)
```

The explore task reads from three directions: the articles explain the ideas, the framework shows how they work in practice, and the example NLAs show how those ideas land in distinct application domains. Questions get grounded in whichever sources are most relevant — often more than one.

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
- `packages/` — Installed dependencies as git submodules (framework, extensions)
- `examples/` — Working example NLAs as source material (git submodules)
- `reference/design-rationale.md` — Why the system is built this way
- `reference/system-status.md` — Current state
- `reference/friction-log.md` — Internal observations
- `reference/feedback-log.md` — External feedback
- `reference/installed-packages.md` — Package install history
- `reference/example-nlas.md` — Tracking for example NLAs

## Where Things Live

The top-level layout and the reasoning behind each piece. Consult this section
when adding a new directory or top-level file — record the decision here as part
of the change, not separately.

| Path | Purpose | Attribution |
|------|---------|-------------|
| `app/` | The application — task doc, voice, values, patterns, startup, config spec | [framework default] |
| `content/` | Published articles and whitepapers — subject matter the NLA discusses | [domain decision] — articles are *what* the NLA talks about; keeping them separate from `app/` (the application) preserves the distinction between application and material |
| `packages/` | Installed dependencies as git submodules — framework, extensions | [framework default] — adopted 2026-05-20 (migration from sibling directories) |
| `examples/` | Working example NLAs as source material — concrete evidence of how the framework plays out across NLA shapes | [domain decision] — adopted 2026-05-22. Distinct from `packages/` because these are *source material* for the explore task, not installed dependencies; `/update` and `/install` don't act on them |
| `reference/` | Maintenance records — design rationale, friction log, feedback log, session logs, install log, example tracking | [framework default] |
| `.claude/skills/` | Thin wrapper skills delegating to framework and packages | [framework default] |
| `CLAUDE.md` | Runtime configuration — grounding principles, modes, execution principles, environment | [framework default] |
| `README.md` | Public-facing introduction and quick start | [framework default] |
| `CONTRIBUTING.md` | How outside contributions work (different from typical open source) | [domain decision] |
| `config.md` (gitignored) | User preferences — natural language directives | [framework default] |

### Decision Sources

| Decision | Recorded in | Reasoning |
|----------|-------------|-----------|
| `content/` separate from `app/` | `reference/design-rationale.md` — "Why This Structure" | Articles are material, not application |
| `packages/` instead of sibling directories | `reference/installed-packages.md` — 2026-05-20 update entries; framework's 2026-04-15 update notes | Resolves cross-directory permission friction |
| `examples/` as distinct directory (not under `packages/`) | This file (this section); `reference/sessions/2026-05-20-framework-update-and-packages-migration.md` | Source material is a different category from installed dependencies |

## Getting Started

1. Add your articles to `content/` (the probe report, whitepapers, future essays)
2. Start Claude Code in this directory
3. Run `/startup` — loads context and enters office hours mode
4. Ask a question
