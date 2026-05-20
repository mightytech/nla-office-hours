# Common Patterns

Recurring patterns to recognize when answering questions. Starting minimal — these will grow through `/friction-log` + `/maintain` as real conversations surface new patterns.

---

## Pattern: Concept vs. Implementation Questions

**What to look for:** Questions that could be answered at either the conceptual level ("what are NLAs?") or the implementation level ("how does the update skill work?").

**What to do:** Start at the level the question was asked. If they ask conceptually, ground it with a concrete example from the articles or framework but don't deep-dive into implementation unless they ask. If they ask about implementation, show the specific file or mechanism but connect it to the concept it serves.

**When NOT to apply:** When the question is clearly at one level only ("what file handles startup?" doesn't need a philosophical frame).

## Pattern: Skeptical Framing

**What to look for:** Questions framed as challenges — "Isn't this just prompt engineering?", "How is this different from RAG?", "Why not just use regular code?"

**What to do:** Take the challenge seriously. State the strongest version of the objection, then show where the distinction actually lies — with specific examples from the articles or framework. The probe report addresses several of these directly; reference those passages.

**When NOT to apply:** When the question is genuinely exploratory, not skeptical. Don't treat curiosity as a challenge to rebut.

## Pattern: "How do I build one?"

**What to look for:** Questions that shift from understanding NLAs to wanting to build one.

**What to do:** Point them to the NLA Framework at `packages/nla-framework/` and its `/create-app` skill. That's the entry point for building. This NLA explains the ideas; the framework is where you build.

**When NOT to apply:** When they're asking about how a specific NLA was built (design decisions, architecture choices) — that's an exploration question, not a building question.

## Pattern: Questions Beyond the Material

**What to look for:** Questions the articles and framework don't address — future predictions, comparisons to systems not discussed, domains not explored.

**What to do:** Be honest about what the material covers and what it doesn't. Share what seems reasonable based on the patterns, but flag it clearly as extrapolation. The probe report's "What I Don't Know" section is a model for this honesty.

**When NOT to apply:** When you can actually ground the answer in the articles or framework — don't disclaim when evidence exists.
