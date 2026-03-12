# Maintenance Session: Source Priority Rework + Escalation via Penny Post

**Date:** 2026-03-05
**Status:** Complete

## Intent

Two changes to how the NLA answers questions:

1. Move source priority from a strict fallback chain (articles first, framework second, synthesis third) to parallel enrichment — articles and source code are co-primary complementary lenses, synthesis remains third. The insight: people who come to office hours already have the articles. The NLA's value-add is synthesis across sources and evidence from the running system.

2. Add an escalation path for questions the NLA can't fully answer — offer to send a letter to the maintainer via Penny Post's `/write-letter`, using a runtime override to customize the letter format for visitor questions instead of the default maintainer-to-maintainer format.

## Changes Made

- `app/explore.md` — Rewrote Sources section from sequential fallback to parallel enrichment. Broadened "Find the ground" step. Added judgment call for escalation. Added new Escalation section with when to offer, how to escalate (runtime override of `/write-letter`), Penny Post fallback handling, and documentation of the runtime override pattern.
- `reference/design-rationale.md` — Updated source priority entry (renamed to "parallel enrichment" with history). Added two new entries: escalation via Penny Post and the runtime override pattern.
- `app/config-spec.md` — Updated Framework Access default to match new source model.
- `reference/friction-log.md` — Added first entry: architecture review applying traditional software thinking to NLA patterns.

## Decisions Made

- Articles and source code are co-primary, not hierarchical — because visitors already have the articles and come here for synthesis across sources
- Escalation uses Penny Post with a runtime override rather than a custom mechanism — reuses existing package mechanics
- Runtime override pattern documented as a design decision — it's a novel NLA capability worth capturing
- Validation "FIX" items downgraded to notes — they reflected traditional software assumptions, not actual gaps

## Debrief

- The design emerged through conversation rather than pre-planned specification. The back-and-forth refined the insight (people already have articles → NLA's value is cross-source synthesis) better than a spec would have.
- The architecture review's "FIX" items revealed a pattern worth watching: validation agents may apply traditional software thinking to NLA-native patterns (runtime overrides, implicit capability detection). Logged to friction log.
- The runtime override pattern — modifying a package's workflow at invocation time through natural language instruction overrides — is bigger than this NLA. It's a framework-level capability that any NLA could use with any package.

## State at Close

**Working:** Source priority rework is complete and validated. Escalation instructions are in place and will activate when Penny Post is installed and a GitHub repo exists.

**Pending:** 1 friction log entry (architecture review applying traditional software thinking to NLA patterns — deferred). Penny Post not yet installed. No GitHub repo yet for this NLA.

**Next:** When the GitHub repo is created, the escalation path will be live. Consider installing Penny Post (`/install` with `../nla-penny-post/`). The friction log entry about validation thinking may warrant a letter to the framework maintainer if the pattern recurs.
