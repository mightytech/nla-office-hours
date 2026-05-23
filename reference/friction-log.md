# Friction Log

Running log of things noticed during NLA Office Hours operation — problems, surprises, things that worked well.

---

## How to Use This Log

**When to add entries:** Whenever you notice something during operation — an answer that didn't land right, a question type you weren't prepared for, a pattern that worked well, a source that was hard to find.

**Entry types:**
- **Output** — The answer itself had issues (wrong tone, wrong depth, missing source)
- **Process** — The question-handling process had issues (slow to find relevant article, unclear which source to prioritize)
- **Documentation** — The task doc, voice, or patterns need updating

**Severity includes positive.** Not everything here is a problem. "This pattern worked really well" is worth capturing.

## Entry Format

```
### YYYY-MM-DD: [Brief title]

- **Type:** Output | Process | Documentation
- **Severity:** Minor | Moderate | Major | Positive
- **Task:** Explore
- **Status:** Open | Resolved (YYYY-MM-DD — what was done)
- **Observation:** What happened
- **Before/After:** [If applicable — what the answer looked like vs. what it should have]
- **Confirmed reason:** [If you can trace it to a specific doc or instruction]
- **Generalizable:** Is this a one-off or a pattern?
- **Affected documentation:** Which files need updating
- **Proposed fix:** What to change
- **Notes:** Anything else
```

Not all fields are required. Use what's relevant.

## Entries

### 2026-05-22: "Default to prose for design conversations" principle (framework 2026-05-11) paid off immediately

- **Type:** Process
- **Severity:** Positive
- **Task:** Maintenance
- **Status:** Open (positive observation — kept as data point, not actionable)
- **Observation:** This session installed the framework's 2026-05-11 "default to prose for design conversations" principle as part of the intent-update batch. Within the same session, the principle was tested in practice: multiple "yes, but" / "yes, and" pushbacks from the maintainer reshaped the design in concrete ways that AskUserQuestion would have flattened into binaries. Examples: examples-as-source-material vs examples-as-packages (recognized that they're semantically different); dropping the export-ignore decision after maintainer noted repos aren't heavy AND export needs the content; distinguishing end-user `git pull` flow from maintainer `/update` workflow; recognizing that penny-post is already a package (so doesn't belong under examples). Each was a layered decision where the actual answer was "yes, but" — prose surfaced it; an enum would have either picked an option that lost the nuance or required several rounds to land.
- **Generalizable:** Empirical reinforcement of the framework principle. Not actionable as a doc change — the principle already lives in `core/nla-foundations.md` and `install/CLAUDE-intent.md`. Value of this entry: positive data point that the principle pays off in real practice, not just theory.
- **Affected documentation:** None.
- **Proposed fix:** None.
- **Notes:** Captured during `/close` debrief (2026-05-22). One of two positive observations from the session about recent framework additions paying off (see also the structure-decisions protocol entry below).

### 2026-05-22: "Where Things Live" record (framework 2026-05-07 structure-decisions protocol) functions as a diagnostic, not just a record

- **Type:** Process
- **Severity:** Positive
- **Task:** Maintenance
- **Status:** Open (positive observation — kept as data point, not actionable)
- **Observation:** This session adopted the framework's 2026-05-07 structure-decisions protocol by creating a "Where Things Live" section in `app/overview.md`. The framework's documentation frames the protocol as a record-keeping discipline ("propose → review → record → act"). In practice, writing the section had a diagnostic side effect: forcing an explicit answer to "what is `lib/` for here?" surfaced that `lib/` existed empty and unused. Pre-existing drift made visible by adopting the protocol. The protocol is not just record-keeping — it asks "is every path attributable?" and the answer for `lib/` was "no current purpose, framework default never used here." Worth knowing that the protocol catches latent structural drift, not only new structural changes.
- **Generalizable:** Yes — any NLA adopting the protocol for the first time should expect to surface at least some latent structural drift (directories or top-level files that exist but have no current purpose). Worth framing this as an expected benefit when the framework documents the protocol.
- **Affected documentation:** Possibly the framework's structure-decisions writeup (`packages/nla-framework/core/nla-foundations.md` Working Rhythms section, or wherever the protocol is documented), could add a note about the diagnostic benefit. Soft suggestion — not letter-worthy on its own.
- **Proposed fix:** None for this NLA. Soft suggestion for the framework if the pattern recurs.
- **Notes:** Captured during `/close` debrief (2026-05-22). Paired observation with the prose-default principle entry above — both are positive notes about recent framework additions (May 2026) paying off in real practice. `lib/` itself is being kept as a reserved slot pending the framework's response to nla-framework#28, which may land `update-app` there.

### 2026-05-22: End-user update flow is git-native — worth a small wrapper, possibly framework-level

- **Type:** Process / Documentation
- **Severity:** Minor
- **Task:** Maintenance (cross-NLA pattern)
- **Status:** Escalated upstream as [nla-framework#28](https://github.com/mightytech/nla-framework/issues/28) (2026-05-22) — letter combined this observation with the post-bulk-edit verification gap (item 2 in that letter). Local entry remains open pending framework response.
- **Observation:** During Phase 2 of the packages + examples migration, the question came up: what's the right end-user flow for "I want this application's content brought up to date"? `/update` is maintainer-only — it both advances pins and applies intent migrations to project files. An end user pulling Office Hours just wants the latest pins materialized: `git pull && git submodule update --init --recursive`. Two commands, easy to forget the second one, and not obvious to non-git-savvy users. A tiny bash script (e.g., `bin/update-app`) wrapping the two commands — paired with the AI knowing about it so a user can say "let's update this application" and the AI just runs it — would close the gap with minimal surface area.
- **Generalizable:** Yes — this isn't an Office Hours problem; it's a general pattern for any NLA that ships as a public repo with submodules and wants non-maintainer users to be able to keep current. The framework's `/check-updates` notes pins are out of date but doesn't bridge to "and here's how a non-maintainer pulls them in." A tiny `bin/update-app` script in the create-app template (or a framework-default) would propagate.
- **Affected documentation:** Possibly `packages/nla-framework/install/skills-intent.md` (introduce an end-user update affordance); `packages/nla-framework/.claude/skills/create-app/SKILL.md` (template addition); `packages/nla-framework/core/skills/startup.md` (AI awareness — when a user expresses intent to update, point at the script).
- **Proposed fix (framework-letter material):** Add a minimal `bin/update-app` script to the framework's create-app template that runs `git pull --ff-only && git submodule update --init --recursive`. Add AI awareness in startup or in a new principle so phrases like "update this application" or "bring this up to date" trigger the script. Document the maintainer/end-user split: `/update` for integrating intent changes (maintainer), `bin/update-app` for materializing pins (everyone).
- **Notes:** Surfaced during the discussion about whether `/update` should learn about `examples/`. The right answer was "no — keep `/update` for intent-bearing packages and let standard git handle source material." That conversation made it clear there's a gap between "git pull" and "/update" — for the end user who just wants fresh content, neither command exists with the right semantics. The bash-script idea fills it.

### 2026-05-20: app/explore.md and app/overview.md don't restate the "NLA documents are source code" principle

- **Type:** Documentation
- **Severity:** Minor
- **Task:** Explore (operative)
- **Status:** Open
- **Observation:** During the post-migration coherence and standards reviews, the load-bearing operative doc (`app/explore.md`, read on every question) and `app/overview.md` describe the system without restating the "NLA documents are source code" framing. CLAUDE.md carries it twice (grounding + execution), the README opens with it, but `explore.md` and `overview.md` start cold. The principle does land via CLAUDE.md being loaded at startup, so this isn't a behavioral break — but it's a self-containment gap by writing standard 8.3, and explore.md's job is to be self-sufficient for the explore task.
- **Generalizable:** Yes — a recurring pattern when reframing a foundational principle (here: framework's 2026-04-18 reframe) is that the reframe lands in CLAUDE.md but doesn't propagate down into task docs and the orientation doc. Worth watching for similar drift after future framework principle changes.
- **Affected documentation:** `app/explore.md` (Sources section is the natural place); `app/overview.md` (What This NLA Does section).
- **Proposed fix:** Add a one-sentence frame to each — explore.md's Sources section could lead with the principle ("The articles and the framework source aren't documentation about an application — they're the application itself"); overview.md's What This NLA Does could include a single sentence anchoring the principle. Not a re-explanation, just an anchor.
- **Notes:** Deferred to a future `/maintain` session — the edit needs voice judgment, not the mechanical batch this session was running.

### 2026-03-05: Architecture review applies traditional software thinking to NLA patterns

- **Type:** Process
- **Severity:** Moderate
- **Task:** Maintenance (validation)
- **Status:** Open
- **Observation:** During an architecture review of changes to `app/explore.md`, the validator flagged two "FIX" items: (1) "How does the NLA detect if `/write-letter` is available?" and (2) "Insufficient context for runtime override invocation syntax." Both assume the NLA needs explicit detection mechanisms and invocation syntax — patterns from traditional code, not natural language systems. The LLM knows its available skills from the skills table loaded at startup, and runtime overrides work through natural language instruction composition, not special syntax.
- **Confirmed reason:** The validate skill's analytical categories (`validate-architecture.md`) are designed for prose systems, but the agent executing them defaulted to code-world assumptions about error handling, try/catch patterns, and explicit invocation syntax.
- **Generalizable:** Yes. Any NLA-native pattern (runtime overrides, skill composition, implicit capability detection) could be misread as a gap by validation that thinks in traditional software terms. This is likely to recur as the system introduces more NLA-native patterns.
- **Affected documentation:** Potentially `../nla-framework/core/skills/validate-architecture.md` — could benefit from a category or note about NLA-native patterns that don't need traditional software scaffolding.
- **Proposed fix:** Consider adding guidance to the architecture review about distinguishing genuine gaps from patterns that work differently in NLAs than in traditional software. Something like: "When flagging missing error handling or invocation syntax, consider whether the LLM runtime handles this implicitly through natural language understanding."
- **Notes:** This is framework-level — worth a letter to the framework maintainer if the pattern recurs.

## Patterns to Watch

- **Source attribution accuracy** — Are quotes from articles accurate? Is the NLA confusing its own synthesis with what the articles actually say?
- **Depth calibration** — Is the NLA matching answer depth to question depth, or defaulting to either too brief or too long?
- **Skepticism handling** — When someone challenges the ideas, does the NLA engage generously or get defensive?
- **Framework staleness** — If the framework evolves, do answers about "how X works" reflect the current state or outdated understanding?
