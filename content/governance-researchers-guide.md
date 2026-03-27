# A Governance Researcher's Guide to the NLA Ecosystem

This document is for readers of [Executable Governance: What Happens When AI Can Follow Its Own Rules](philosophy-probe-v4.md) who want to inspect the system the essay describes. It maps the essay's claims to specific artifacts, orients you to what you're looking at when you open a repository, and suggests a reading path.

You don't need to read code. The operative documents are prose.

---

## The Ecosystem in Governance Terms

The system has a constitution, jurisdictions, a feedback channel, deliberative procedures, institutional memory, and a mechanism for depositing governance patterns into systems that didn't ask for them.

| Governance function | System component | Repository |
|---|---|---|
| Constitution | Foundational principles, including authority, values visibility, and assumed imperfection | [NLA Framework](https://github.com/mightytech/nla-framework) |
| Jurisdictions | Applications that inherit constitutional principles but write their own values and policies | [Penny Post](https://github.com/mightytech/nla-penny-post), [Office Hours](https://github.com/mightytech/nla-office-hours), [Duet](https://github.com/mightytech/duet) |
| External stakeholder input | Conventions for submitting feedback, with visible evaluation and reasoned verdicts | [Penny Post](https://github.com/mightytech/nla-penny-post) |
| Deliberative procedures | Facilitation techniques — structured brainstorming, devil's advocacy, steelmanning — that install into any jurisdiction | [Process Helpers](https://github.com/mightytech/nla-process-helpers) |
| Institutional memory | Design rationale, session logs, friction logs, feedback archives — the full deliberative trail. Each jurisdiction maintains its own. | [Framework reference/](https://github.com/mightytech/nla-framework/tree/main/reference) and `reference/` in each application |
| Outward diffusion | Governance patterns deposited into traditional software projects through practical utility | [nla-claude-code](https://github.com/mightytech/nla-claude-code) |

---

## What You're Looking at When You Open a Repository

Every NLA repository follows a similar structure. Here's what the directories mean in governance terms:

- **`app/`** — The operative governance. This is what the AI reads and follows. Values, policies, task instructions, behavioral specifications — all in prose. Changes here change how the system behaves.
- **`app/shared/`** — Values and commitments that apply across all tasks in this jurisdiction. The values document is here.
- **`reference/`** — Institutional memory. Session logs, design rationale, feedback archives, friction logs. This is where you find the deliberative trail — not just what was decided, but why, what alternatives were considered, and what was rejected.
- **`install/`** (where present) — Intent files for extending other systems. These describe what the extension wants, not how to implement it. The receiving system's AI adapts the intent to its own structure.

**Note on the framework itself:** The framework repository uses `core/` instead of `app/`. It's the constitutional layer — foundational principles and shared skills — not an application. The skills (friction logging, validation, reflection, session management) live in `core/skills/`. Applications built on the framework inherit these and add their own governance in `app/`.

---

## Claim-to-Evidence Map

The essay makes specific claims. Here's where to verify each one.

| The essay says... | Look here |
|---|---|
| Values are a document the AI reads | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) (principle 5: "Values Are Visible") and [framework values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) |
| Soft contradiction flagging | The mechanism is described in the values infrastructure; evidence of it operating appears in [session logs](https://github.com/mightytech/nla-framework/tree/main/reference/sessions) and [friction log archives](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md) |
| Fractal values — same commitments, different expression | Compare [framework values](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) with [Penny Post values](https://github.com/mightytech/nla-penny-post/blob/main/app/shared/values.md) and [Office Hours values](https://github.com/mightytech/nla-office-hours) |
| Participation mechanism with visible reasoning | [CONTRIBUTING.md](https://github.com/mightytech/nla-framework/blob/main/CONTRIBUTING.md) (the mechanism) and [feedback-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/feedback-log-archive.md) (the evidence — eleven items, each with verdict and reasoning) |
| Learning loop / friction log | [friction-log.md skill](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md) (the mechanism) and friction log entries in each project's `reference/` directory |
| Capabilities emerged from friction | [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — traces the origin of think, debrief, close, and unpack skills to specific friction observations |
| Design rationale preserves deliberation | [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) (~1700 lines — decisions, alternatives considered, reasoning preserved) |
| Debrief / participant-observer | [debrief.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/debrief.md) (the skill) and session logs showing it in use |
| The Cardinal Rule — "the human decides" | [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md), principle 6 |
| Context Determines Competence | [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — the entry explaining why judgment operations can't cross project boundaries |
| Loosening specs / broadening over adding | [Penny Post first review](https://github.com/mightytech/nla-penny-post/blob/main/reference/sessions/2026-02-16-first-review.md) — twenty numbered decisions showing broadening in action |
| Intent-based installation | [install/](https://github.com/mightytech/nla-penny-post/tree/main/install) directories in packages — intent descriptions, not templates |

---

## Three Directions of Propagation

The essay describes governance mechanisms working inside one ecosystem. But the architecture also shows governance propagating in three directions — inward, laterally, and outward. Each is demonstrated by a different system component.

### Inward: External Stakeholder Input (Penny Post)

[Penny Post](https://github.com/mightytech/nla-penny-post) defines conventions for submitting feedback from outside the system. What makes it a governance mechanism rather than a suggestion box: every submission is evaluated against the receiving project's full context, and every verdict — including rejections — gets visible reasoning. The architectural redesign documented in the [first review session](https://github.com/mightytech/nla-penny-post/blob/main/reference/sessions/2026-02-16-first-review.md) followed from a jurisdictional insight: evaluation requires understanding, so it must happen where the context lives. A governance researcher would recognize this as a due process mechanism — not just the right to be heard, but the right to a reasoned response.

### Laterally: Deliberative Capacity (Process Helpers)

[Process Helpers](https://github.com/mightytech/nla-process-helpers) are facilitation techniques — structured brainstorming, devil's advocacy, steelmanning, conversation structuring — expressed in prose and executable by the AI. They ship as a package that any NLA can install. The deliberative capacity doesn't live in any one project. It propagates through adoption.

This matters for a question the essay raises honestly: the current system has one developer. But the architecture doesn't assume a single author. Deliberative procedures that install into any jurisdiction, that structure how decisions get explored regardless of who's exploring — that's infrastructure for multi-stakeholder governance, even if it currently operates at a scale of one.

### Outward: Governance Patterns in Traditional Software (nla-claude-code)

[nla-claude-code](https://github.com/mightytech/nla-claude-code) deposits governance patterns into traditional software projects — friction logs, convention documents that explain their reasoning, lightweight observation tools. The developers who use these don't need to adopt a governance framework. They install a development tool that happens to carry governance patterns. The patterns are useful on their own terms — documenting conventions, logging friction, preserving rationale — so they propagate through practical utility rather than mandate.

The governance operates differently here than inside an NLA. In a natural language application, the AI reads `values.md` at runtime — the values are operative in every decision. In a traditional codebase, the Python interpreter doesn't read the values file. The governance operates through the developer: values inform design thinking and code review, friction logs capture observations, Penny Post feedback still flows. The values are operative when humans are thinking and writing code, not when the program is executing. That's a meaningful boundary — governance through the developer rather than through the executor — and it's worth understanding precisely because it clarifies what's different about the NLA case.

A governance researcher would recognize the broader pattern as institutional diffusion through professional practice: norms spreading not through top-down policy but because practitioners find them useful and carry them into new contexts.

---

## Suggested Reading Path

**15 minutes — the essentials:**
1. [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — the constitutional principles (especially 5: Values Are Visible, 6: The Cardinal Rule)
2. [Framework values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) — a values document the AI actually reads
3. [CONTRIBUTING.md](https://github.com/mightytech/nla-framework/blob/main/CONTRIBUTING.md) — the participation mechanism

**One hour — the governance trail:**
4. [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — scan the first several entries to see how decisions are preserved with reasoning
5. [feedback-log-archive.md](https://github.com/mightytech/nla-framework/blob/main/reference/feedback-log-archive.md) — see how external input is evaluated with visible reasoning
6. [Penny Post values.md](https://github.com/mightytech/nla-penny-post/blob/main/app/shared/values.md) — compare with the framework's values to see fractal governance in practice
7. One [session log](https://github.com/mightytech/nla-framework/tree/main/reference/sessions) — see what institutional memory looks like in this medium

**Deep dive — the architecture:**
8. [Penny Post first review](https://github.com/mightytech/nla-penny-post/blob/main/reference/sessions/2026-02-16-first-review.md) — twenty architectural decisions with rationale, following from a single jurisdictional insight
9. [Process Helpers](https://github.com/mightytech/nla-process-helpers) — deliberative techniques as portable, installable prose
10. [nla-claude-code](https://github.com/mightytech/nla-claude-code) — governance patterns in a traditional development context

---

## Or: Ask the System Directly

If you'd prefer to explore interactively rather than read files, [NLA Office Hours](https://github.com/mightytech/nla-office-hours) is a conversational companion that can read the framework's source code in real time and answer questions about it. It's an NLA itself — its behavior is governed by prose documents that define its values, voice, and how it handles sources. You're not just learning about the paradigm. You're using an instance of it.

Some questions worth asking:

1. **Read the framework's values document and the CONTRIBUTING.md. How do stated values connect to the participation mechanism? Where are the gaps?**
2. **Read the design rationale. Pick one decision and trace its reasoning. What alternatives were considered and why were they rejected?**
3. **Read the friction log archives. What patterns do you see in what went wrong and how it was fixed?**
4. **Compare the framework's values with Penny Post's values. How do the same commitments express differently in different contexts?**
5. **What are this system's weakest governance mechanisms? Where would a skeptical reviewer find the most to challenge?**
6. **How does this system map to Ostrom's eight design principles for governing commons institutions (defined boundaries, rules matching local conditions, collective-choice arrangements, monitoring, graduated sanctions, conflict resolution, right to organize, nested enterprises)? Where does the analogy hold, and where does it break?**

Watch how the AI handles sources — it distinguishes between what the documents say, what the source code shows, and what it's synthesizing on its own. That source attribution is itself a governance mechanism.
