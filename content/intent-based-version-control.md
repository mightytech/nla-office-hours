# What Version Control Looks Like When Your Source Code Is Prose

I didn't set out to build a version control system. I was building a feedback mechanism — a way for one AI to send observations to another project's AI, packaged as a prose letter in a GitHub issue. The receiving AI would read the letter, evaluate each item against its own project's goals, and act on the ones that made sense.

It wasn't until someone pointed out the full pipeline that I saw what I'd actually built.

---

## The observation

After Duet — a music composition NLA — ran its first real maintenance session, the AI had eleven observations about the framework it was built on. Things like: the framework assumes every NLA transforms input into output, but Duet creates things that didn't exist before. The startup sequence doesn't have extension points. The cardinal rule is framed around transformations when it should be universal.

These weren't bug reports. They were behavioral observations with reasoning — the kind of thing a thoughtful colleague would raise in a code review, except they were about prose, not code.

The observations became a letter. The letter was filed as a GitHub issue against the framework. The framework's AI read it, triaged each item against the project's loaded context — its values, its design rationale, its history — and proposed verdicts.

One of those verdicts surprised me. Item 1 proposed that the framework should formalize its package installation pattern with an `install/` directory. The AI's initial assessment: **defer** — only one extension exists, it's premature to generalize. I pushed back: the penny post package already ships an `install/` directory, and NLAs need a way to consume it now. Deferring would mean ad hoc workarounds that cost as much as doing it properly. The verdict changed to **accept**.

That exchange — the AI proposing a reasoned judgment, the human overriding it with context the AI didn't weigh heavily enough, the verdict updating with new rationale — that's code review. But the "code" being reviewed is intent, not text.

---

## What the pipeline actually does

Here's what happens when someone wants to change an NLA, traced through what actually happened with that Duet letter:

**The letter arrives.** Eleven items of behavioral feedback, each with observations and reasoning. Not "change line 47 of foundations.md" but "the framework assumes transformation NLAs — here's where that shows up and why it matters for other shapes." The person sending the letter doesn't need to know which files to edit. They describe what they observed. The receiving AI figures out what that means for actual documentation.

**Triage.** The AI evaluates each item against the project's full context, using evidence thresholds — one observation is a data point, two from different contexts is a signal, three is strong. For the Duet letter, the framework AI assessed each item and proposed verdicts: accept, adapt, defer, or decline. Every verdict carried reasoning. I reviewed each one and adjusted where my judgment differed.

**Implementation.** Accepted items landed in the feedback log — a queue for the maintain skill to process. The maintain session turned those items into actual documentation changes: broadening the cardinal rule from transformation-specific to universal, adding NLA shapes (stateless, persistent, tool-using) to the foundations, making the output spec conditional instead of mandatory. The AI did this with full project context, understanding how each change interacted with everything else in the system.

**The session log.** This is where it gets interesting. [The session log](https://github.com/mightytech/nla-framework/blob/main/reference/sessions/2026-02-19-duet-feedback-and-update-notes.md) from that maintenance session captured intent ("broaden the framework beyond its transformation-NLA origins"), decisions with rationale ("Cardinal Rule reframed as 'the human decides' — universal, not transformation-specific"), blast radius (which downstream projects would be affected), what emerged during the work (the voice/values splitting question was deferred as "bigger design, needs its own session"), and what was still open for next time. Three new friction log entries were added during the session itself — observations about the work that became fuel for future improvements.

---

## Why this is version control

I didn't see it at first because I was looking for the wrong shape. Git tracks text changes. This tracks intent changes. But the functions map:

| Traditional VCS | NLA Equivalent |
|---|---|
| PR / patch | Penny post letter |
| Code review | Triage (with evidence thresholds and reasoned verdicts) |
| Merge | Maintain session (judgment-based synthesis) |
| Commit message | Session log (intent, rationale, alternatives, what didn't work) |
| Blame / history | Feedback log + design rationale |
| Branch | Rollback branch (safety net, not workflow) |

The reason diffs don't work here is that NLA source code is prose an AI interprets, not text a machine executes literally. Change "clarity over cleverness" to "precision over accessibility" in a values document. The text diff is one line. The behavioral change propagates through every judgment the AI makes — every interaction sounds different. Git tracks the trivial part. The session log tracks the part that matters.

That's also why the "merge" is fundamentally different. Two NLAs receiving the same feedback letter implement it differently, because the AI synthesizes the intent against each project's own voice, values, and structure. The merge is judgment, not a patch. A diff algorithm can't do that. But it also means the merge can be *wrong* in ways that are harder to detect — behavioral regressions that don't show up as test failures because there are no behavioral tests yet. More on that below.

---

## What this makes possible

**Feedback from people who can't read the codebase.** A traditional PR requires understanding the code well enough to propose a specific text change. A penny post letter requires only that you can describe what you observed and what you think should be different. A user who notices the AI sounds defensive when questioned can contribute that observation without knowing anything about voice documents. The AI bridges the gap between observation and implementation.

**Audit trails that explain behavior.** Six months later, you want to know why the NLA handles skeptical questions the way it does. In an NLA, you trace the chain: someone sent a letter, the triage accepted it with reasoning, the maintain session adjusted the documentation, the session log explains why those changes were chosen over alternatives. The full reasoning chain is preserved in prose anyone can read. In traditional code, you'd read git blame, find the commit, read "updated voice.md," and try to reconstruct the reasoning from memory.

**A hint at multi-user coordination.** Everything I've built is single-user. But the triage system already handles competing intents. Two maintainers both think the NLA should change? Each sends a letter, each is triaged independently, and if the intents conflict, the triage surfaces the conflict with reasoning rather than silently creating an inconsistent state. The human resolves the conflict at the intent level — "we want both warmth and precision, here's how to balance them" — rather than at the text level — "which version of line 47 do we keep?" That's not a complete answer to multi-user NLAs. But the infrastructure might already exist in a system that was built for something else.

---

## What I don't know

**Session logs are AI-generated.** The audit trail I'm describing — intent, rationale, decisions, what didn't work — is produced by the same runtime that might hallucinate. The probe report already flags [the confabulation risk](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md) explicitly: "You might construct a plausible-sounding explanation that's actually wrong." If your commit messages can confabulate, what does that mean for your audit trail? Exact quotes help — they're checkable. But the tension is real and unresolved.

**Silent bad synthesis might be worse than merge conflicts.** Traditional merge conflicts are annoying but honest — they force a human decision at the point of conflict. Intent-based merging could produce subtle behavioral regressions. The AI synthesizes two changes in a way that satisfies the text of both intents but misses the spirit of one. You wouldn't see a merge conflict. You'd see slightly wrong behavior, eventually, maybe. The failure mode is mediocrity, not errors — the same risk the probe report identifies for model dependency.

**Scale.** This has been tested with single letters between two projects. What happens at twenty letters? A hundred? Does triage quality degrade as volume increases? Does the AI start pattern-matching verdicts instead of reasoning about each item? I don't know. The evidence thresholds help — they're designed to prevent premature convergence on small samples — but they haven't been stress-tested.

**Whether intent-based change management generalizes.** I've seen it work for prose-based systems where behavior is mediated by AI judgment. I have not seen evidence that it works — or needs to work — beyond that context. Traditional version control is excellent at what it does. This isn't a replacement. It's a response to a specific gap: when your source code is prose, text diffs don't capture behavioral change. If your source code isn't prose, you probably don't have that gap.

---

## The pattern underneath

What I actually built was a change management pipeline where the unit of change is intent rather than text. Git is still underneath — it tracks which files changed, provides rollback branches, handles the mechanical versioning. But the layer that captures *meaning* — what changed behaviorally, who proposed it, why it was accepted, what alternatives were considered — that layer operates in prose, mediated by AI judgment.

Whether that's "version control" or something else, I'm not sure the label matters. The trail from the Duet letter through triage, implementation, and session log is traceable in documents anyone can read. That's more than most commit histories offer. It's also more fragile, in ways I've only started to understand.

*This is one of several explorations of [Natural Language Application](the-documentation-is-the-application.md) patterns applied to specific domains.*
