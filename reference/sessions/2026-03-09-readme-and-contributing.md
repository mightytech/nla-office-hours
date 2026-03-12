# Maintenance Session: README and CONTRIBUTING

**Date:** 2026-03-09
**Status:** Complete

## Intent

Update the README and create a CONTRIBUTING.md that feel aligned with the sibling projects (framework, penny post) — same structural patterns, same voice register, project-specific where it matters. The current README was functional but thin, missing the identity and energy of the other READMEs. No CONTRIBUTING existed.

## Changes Made

- **README.md rewritten** — Added thinking-partner identity and "not a search engine" framing in the opening. Added "What Is an NLA?" section with the two-path hook (self-reference handled: "Talk to one: That's what this is."). Added new "Using It" section covering the conversation rhythm, question types, and source dynamics. Renamed "Framework Updates" to "Upgrading" with expanded content. Added CONTRIBUTING callout in "Improving It". Aligned all shared sections (Getting Help, Learn More) with sibling language. Kept directory structure, customization table, configuration, and adding content sections.

- **CONTRIBUTING.md created** — Adapted from the framework/penny post template. Shared sections kept near-identical (why no PRs, simulation, appeals, what happens after, language, values). Customized the "more useful / less useful" example pair for conversation experience ("I asked about non-determinism and the answer only referenced the probe report but the framework's values files show this in practice..."). Customized "For Non-Developers" with Office Hours-specific examples (shallow answers, abstract vs. concrete, defensive vs. generous skepticism handling).

## Decisions Made

- **"What Is an NLA?" self-reference** — Kept the section for structural alignment (someone landing cold needs orientation) but acknowledged the circularity with "That's what this is." — confident, not cute.
- **CONTRIBUTING shares heavily with siblings** — The observations-over-PRs argument is paradigmatic, not project-specific. Only two sections needed Office Hours flavor (example pair, non-developer examples). Omitted the framework's blast-radius paragraph (not relevant — changes here affect conversation experience, not downstream projects).
- **"Using It" as a new section** — Unique to Office Hours. The siblings describe skill invocations; this project's "using it" is having conversations. Covers rhythm, question types, source dynamics, and escalation.
- **Audience: technical** — People who've read the probe report or are working with the framework. Not general public. This shaped the voice level and what we didn't need to explain from scratch.

## Debrief

- The `/think` session before planning was valuable — it surfaced the self-reference question, the audience question, and the structural alignment question before any writing happened. All three shaped the output.
- The probe report reading gave context that the existing README lacked. The "not a search engine" and "synthesis across sources" framings come directly from how the probe report describes the value NLAs add beyond document retrieval.
- The CONTRIBUTING template is stable enough across three projects now to feel like a genuine convention. The shared sections are paradigmatic; the customized sections are small and predictable (examples, non-developer audience framing). Future NLAs could follow the same pattern.

## State at Close

**Working:** README.md rewritten with aligned structure and voice. CONTRIBUTING.md created with shared template + Office Hours flavor. Both structurally aligned with framework and penny post siblings.

**Pending:** No git repo for this NLA — can't commit yet. 1 friction log entry still open (architecture review applying traditional software thinking). system-status.md `Last updated` date still stale.

**Next:** Initialize git repo when ready. The README's directory tree doesn't list `CONTRIBUTING.md` (it lists `CLAUDE.md` but not other root files) — minor, worth adding next session. The friction log entry about validation may be worth a letter to the framework maintainer. Consider updating system-status.md date.
