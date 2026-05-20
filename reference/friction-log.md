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
