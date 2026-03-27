# Evidence Guide: The Documentation Is the Application

This document is for readers of [The Documentation Is the Application: Are We in the CGI-bin Era of AI?](probe-report-v9.md) who want to verify the claims against the actual artifacts. It maps the essay's key claims to specific files and repositories.

What you'll find when you open these repos isn't code — it's prose. That's the point. The documents you're reading *are* the applications the essay describes. The AI reads the same files you're reading and follows them.

---

## What You're Looking at

Every NLA repository follows a similar structure:

- **`app/`** — The application itself. Prose the AI reads and executes. Task instructions, behavioral specifications, values — all in markdown. Edit these files and you change how the application behaves.
- **`app/shared/`** — Context shared across all tasks: values, voice, patterns. The AI loads these at startup.
- **`reference/`** — Development history. Session logs, design rationale, friction logs, feedback archives. The deliberative trail behind the application.
- **`core/`** (framework only) — The shared foundation. Principles and skills that all NLAs inherit. The framework uses `core/` instead of `app/` because it's infrastructure, not an application.
- **`install/`** (where present) — Intent files for extending other systems. Descriptions of what the extension wants — the receiving AI adapts them to its own structure.

---

## Claim-to-Evidence Map

### Finding 1: Disciplines collapse into paragraphs

| The essay says... | Look here |
|---|---|
| A single sentence replaces an entire discipline (spam filtering, issue triage) | [check-feedback.md](https://github.com/mightytech/nla-penny-post/blob/main/check-feedback.md) — the feedback triage skill, including evidence thresholds and verdict reasoning |
| Prose carries full engineering complexity (the update system as package manager) | [update.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/update.md) — rollback branches, merge strategies, bootstrap mode, intent-based updates. All prose. |
| Loosening specifications creates judgment space, not undefined behavior | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — principle 4: "Judgment Over Rules," with the blockquote example |
| Knowing when prose is the wrong tool | The essay's bash script example; more broadly, [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — principle 7: "Hybrid Architecture" |

### Finding 2: Improvement through the medium itself

| The essay says... | Look here |
|---|---|
| The friction log captures observations and diagnoses | [friction-log.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md) (the skill) and [friction-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) (the evidence) |
| The AI diagnosed its own misinterpretation of "Thoughts? Concerns? Ideas? Questions?" | [friction-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) — the specific entry, with the ambiguous wording identified and the fix traced |
| Premature implementation → revert → process improvement | [friction-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) — the entry documenting the failure and the four-phase flow that emerged |
| Positive baselines preserved alongside failures | [friction-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) — entries with positive severity |
| The confabulation safeguard — exact quotes, not paraphrases | [friction-log.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md) — the "confabulation risk" section quoted in the essay |
| The debrief reflects on collaboration dynamics | [debrief.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/debrief.md) — the two dimensions: instruction quality and collaboration quality |
| Session logs preserve the full trail | [reference/sessions/](https://github.com/mightytech/nla-framework/tree/main/reference/sessions) — 33 sessions with decisions, reasoning, and reflections |

### Finding 3: AI as the application (the hybrid model)

| The essay says... | Look here |
|---|---|
| The AI is the application; traditional code is the plumbing | Any NLA's `app/` directory — the prose IS the application. Compare with `lib/` (where present) for the traditional code layer. |
| Context Determines Competence — mechanical operations cross boundaries, judgment operations can't | [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — the entry developing this principle |
| The boundary between judgment and determinism runs through documents, not between them | [update.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/update.md) — a single skill that interleaves git operations with judgment calls |
| The runtime occupies three roles simultaneously (instruction-following, perception, self-monitoring) | [think.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/think.md), [debrief.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/debrief.md) — skills that ask the AI to monitor its own process |
| The ChatGPT Health example — using the LLM for what code should do | [Washington Post article](https://www.washingtonpost.com/technology/2025/03/25/chatgpt-health-app-review/) — the counter-example showing the hybrid model's importance |

### Finding 4: Values as source code

| The essay says... | Look here |
|---|---|
| Values are a document the runtime reads | [Framework values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) — a working values document the AI reads at startup |
| Soft contradiction flagging — the AI checks proposals against values | [maintain.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/maintain.md) — the skill that evaluates changes against stated values |
| Values improve quality, not just safety ("clarity over cleverness" produces better writing) | [Framework values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) — values like "clarity over cleverness" and "match confidence to evidence" that shape output quality |
| Authority follows accountability, not capability | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — principle 6: "The Cardinal Rule" |
| No neutral default — an NLA without explicit values inherits unexamined model defaults | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — principle 5: "Values Are Visible" |

### Finding 5: Language as protocol

| The essay says... | Look here |
|---|---|
| Two AIs coordinated through prose letters | [Penny Post](https://github.com/mightytech/nla-penny-post) — the conventions, and [feedback-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/feedback-log-archive.md) — eleven items processed with visible reasoning |
| Evidence thresholds — one observation is a data point, two is a signal, three is strong | [check-feedback.md](https://github.com/mightytech/nla-penny-post/blob/main/check-feedback.md) — the evidence threshold framework |
| Intent-based installation — declare intent, let the AI synthesize | [install/](https://github.com/mightytech/nla-penny-post/tree/main/install) directories — intent descriptions, not templates |
| Two NLAs installing the same extension get different integrations | The mechanism is in the install files; the evidence is in comparing how different NLAs integrate the same package |
| "Not just prompt engineering" — persistence, learning loops, modularity | The full framework architecture — `app/` for the application, `reference/` for persistence, `core/skills/` for modularity, friction logs for learning |

### What This Might Mean / CGI-bin Analogy

| The essay says... | Look here |
|---|---|
| The framework manually shims capabilities the platform should provide | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) (teaching the AI to be a runtime), [close.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/close.md) (session continuity), [startup.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/startup.md) (context recovery) — workarounds for platform limitations |
| The export system produces standalone applications from prose components | [export.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/export.md) — the "compiler" that resolves dependencies and produces distributable NLAs |
| The pieces need each other — the system is the contribution | The full ecosystem: [NLA Framework](https://github.com/mightytech/nla-framework), [Penny Post](https://github.com/mightytech/nla-penny-post), [Process Helpers](https://github.com/mightytech/nla-process-helpers), [Duet](https://github.com/mightytech/duet), [nla-claude-code](https://github.com/mightytech/nla-claude-code) |

---

## The Applications

The essay describes several NLAs. Here's what each one is and what it demonstrates.

| Application | What it is | What it demonstrates |
|---|---|---|
| [NLA Framework](https://github.com/mightytech/nla-framework) | The shared foundation — principles, skills, and infrastructure all NLAs inherit | The constitutional layer: values, authority, learning loops, validation |
| [Duet](https://github.com/mightytech/duet) | Collaborative music composition with SuperCollider | Judgment in a creative domain; the feedback that broadened the framework's governance language |
| [Copydesk](https://github.com/mightytech/copydesk) | CMS content formatting with pluggable voice and platform packages | Discipline collapse — editorial judgment replacing hand-coded formatting rules |
| [Penny Post](https://github.com/mightytech/nla-penny-post) | Feedback conventions and inter-agent communication | Language as protocol; the accountability chain; evidence thresholds |
| [nla-claude-code](https://github.com/mightytech/nla-claude-code) | AI-managed developer tooling for traditional codebases | Governance patterns propagating outward into systems that aren't NLAs |
| [Process Helpers](https://github.com/mightytech/nla-process-helpers) | Facilitation techniques — brainstorming, steelmanning, devil's advocacy | Deliberative procedures as portable, installable prose |
| [Email Rewriter](https://github.com/mightytech/email-rewriter) | Tone-aware email rewriting | The simplest possible NLA — a single task, no persistence |
| [NLA Office Hours](https://github.com/mightytech/nla-office-hours) | Interactive Q&A grounded in published articles and framework source | A way to explore the system interactively rather than by reading files |

---

## Suggested Reading Path

**10 minutes — see the pattern:**
1. [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — the foundational principles. This is prose the AI reads and follows. That's the finding.
2. [Framework values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) — a values document the AI actually reads. Compare this with [Penny Post values.md](https://github.com/mightytech/nla-penny-post/blob/main/app/shared/values.md) to see how the same commitments express differently.

**30 minutes — see the mechanisms:**
3. [friction-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) — the learning loop in action: observations, diagnoses, fixes
4. [update.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/update.md) — a full package manager written in prose. This is where "disciplines collapse into paragraphs" gets real.
5. [feedback-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/feedback-log-archive.md) — language as protocol: prose feedback evaluated with visible reasoning

**One hour — see the architecture:**
6. [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — scan the first several entries. Every architectural decision with reasoning, alternatives, and affected components.
7. [think.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/think.md) — a skill born from friction. The AI kept pushing toward decisions when the work needed exploration. This is the fix.
8. [Penny Post](https://github.com/mightytech/nla-penny-post) — the feedback system that emerged when two AIs needed to coordinate
9. [Duet](https://github.com/mightytech/duet) — a different domain (music composition) using the same architecture. Look at `app/` to see how a creative NLA differs from a utility NLA.

---

## Or: Ask the System

[NLA Office Hours](https://github.com/mightytech/nla-office-hours) lets you explore the ecosystem interactively. It reads the framework's source code in real time and answers questions about it — which is itself a demonstration of the paradigm.

Some starting questions:

1. **Read the framework's nla-foundations.md. What are the design principles and how do they connect to each other?**
2. **Read the update skill. How does a package manager work when it's written in prose instead of code?**
3. **Compare the friction-log-archive entries with the design-rationale entries. How does an observation become an architectural decision?**
4. **Read Duet's app/ directory and NLA Writer's app/ directory. How do two very different applications share the same architecture?**
5. **What are this system's biggest unsolved problems? Where would you expect it to break?**
