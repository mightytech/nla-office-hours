# Design Rationale

Why NLA Office Hours is built the way it is. For maintainers — prevents well-intentioned changes from breaking things that work.

---

## Why an NLA?

The articles about NLAs are prose. The framework is prose. A conversational companion to both is a natural fit for the NLA pattern — the "application logic" is instructions for how to answer questions grounded in source material. There's no computation to do, no data to transform. The entire task is judgment: understanding a question, finding the right source, synthesizing an answer at the right depth, and connecting ideas across a body of work.

Traditional Q&A systems (RAG, search) retrieve passages. This NLA understands the material well enough to synthesize — drawing on the articles AND the framework source AND the connections between them. That synthesis is the value an LLM adds.

## Why This Structure

**`content/` as a separate directory (not inside `app/`).** The articles are the material the NLA works with, not the application logic. `app/` contains instructions for how to answer questions; `content/` contains what to answer them from. This separation means adding articles doesn't touch the application — you just drop files into `content/`.

**No domain skill for the task.** Most NLAs have a `/task-name` skill for each task. Office Hours makes the task the default mode — after startup, you're immediately in office hours. No separate skill invocation. This reflects the interaction model: people come here to ask questions, not to invoke a tool. The task doc (`app/explore.md`) is referenced by the default mode in CLAUDE.md.

**Wide-open configuration.** Most NLAs define specific configurable behaviors. Office Hours deliberately leaves configuration unconstrained — users can write any natural language preference. This serves as an object lesson in NL configuration: the LLM interprets and applies whatever the user writes. The config-spec describes possibilities rather than prescribing a fixed schema.

**Voice adapted from nla-writer.** The voice and values files are adapted from the NLA that helped write the articles. The core principles (precise not academic, honest not hedged, grounded not grandiose) apply directly to answering questions about the same material. The adaptation shifted from writing-partner framing to exploration-guide framing.

## Key Design Decisions

### Source priority: parallel enrichment
**Decision:** Articles and source code are co-primary, complementary lenses. Synthesis is genuinely third.
**Why:** The original hierarchy (articles first, framework second) assumed articles were sufficient when they partially addressed a topic. In practice, people who come to office hours already have access to the articles — the NLA's value-add is drawing on source code as living evidence and synthesizing across both. Articles provide the author's framing; source code provides how things actually work, details the articles couldn't fit, and connections between pieces. Either can lead depending on the question.
**History:** Originally articles-first with framework as fallback. Changed because the strict hierarchy caused the NLA to stop at partial article coverage rather than enriching with source code evidence.
**Alternatives:** The original sequential fallback kept answers grounded but undervalued the NLA's ability to draw on implementation as evidence. A fully flat model with no priority risks synthesis creeping into primary-source territory — keeping synthesis as explicitly third prevents that.
**Affects:** `app/explore.md` Sources section and "Find the ground" step.

### Auto-start after startup
**Decision:** No separate skill invocation to enter office hours mode.
**Why:** The interaction model is conversational — show up and ask. Adding a skill invocation creates unnecessary friction for what should feel like walking into someone's office.
**Affects:** CLAUDE.md default mode, `app/startup.md`.

### Escalation via Penny Post
**Decision:** When the NLA can't fully answer a question, offer to send a letter to the maintainer via `/write-letter`.
**Why:** Office hours have limits. A TA who can't answer a question should be able to say "let me check with the professor" rather than stopping at "I don't know." The visitor gets an answer eventually, the maintainer gets questions packaged with diagnostic context, and gaps in the material get surfaced.
**Alternatives:** Could just say "I don't know." But that wastes the office hours metaphor — real office hours have escalation paths. Could build a custom feedback mechanism, but Penny Post already handles the mechanics.
**Affects:** `app/explore.md` judgment calls and new Escalation section.

### Runtime override pattern
**Decision:** Invoke `/write-letter` with modified instructions — a custom format for visitor questions instead of the default maintainer-to-maintainer letter format.
**Why:** The `/write-letter` skill is designed for one context but its mechanics — draft, review, submit as GitHub Issue — work for visitor question escalation too. Rather than forking the package or requesting a new feature, the NLA overrides the workflow at invocation time with natural language instructions. This is the NLA equivalent of calling a function with different parameters.
**Alternatives:** Could fork Penny Post and add a visitor-question mode, but that couples the package to one NLA's use case. Could build escalation from scratch, but the submission mechanics are already built. The override pattern reuses what exists.
**Affects:** `app/explore.md` Escalation section.

## Adding Decisions

When making a design choice during maintenance, document it here:
- What was decided
- Why (the reasoning, not just the conclusion)
- What alternatives were considered
- What it affects (which files, which behaviors)
