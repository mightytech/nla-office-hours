# Maintenance Session: Framework Update and Packages Migration

**Date:** 2026-05-20
**Status:** In Progress

## Intent

`/update` session covering ~7 weeks of framework evolution since the last update (2026-03-30, framework `b63ed87` → `3fed474`). Two distinct decision tracks:

1. **Apply the smaller intent changes** — wording refresh, new bullet, new `/session-checkpoint` skill, two table description updates.
2. **Adopt the packages/ migration** — retire the sibling-directory convention (`../nla-framework/`, `../nla-penny-post/`) in favor of git submodules at `packages/nla-framework/` and `packages/nla-penny-post/`. This is the framework's response to the permission-friction letter this project sent on 2026-03-30 (nla-framework#15) — it's the structural fix for the problem we've been living with.

Splitting them so each lands as its own coherent commit and the diff stays reviewable.

## Changes Made

### Step 1 — smaller intent changes (committed separately from the migration)

- **CLAUDE.md** — "Documentation is the application" / "Documentation is source code" → "NLA documents are source code" (two bullets, matches framework principle #2 reframe of 2026-04-18).
- **CLAUDE.md** — new Execution Principles bullet: "Default to prose for design conversations" (framework intent change 2026-05-11; condensed for the project's terser voice).
- **CLAUDE.md + app/overview.md** — added `/session-checkpoint` row in skills tables, between `/debrief` and `/close`.
- **`.claude/skills/session-checkpoint/SKILL.md`** — new thin wrapper delegating to `../nla-framework/core/skills/session-checkpoint.md` (path will be updated to `packages/nla-framework/` in step 2).
- **`.claude/skills/validate/SKILL.md`** — description updated to include "standards review" mode (framework change 2026-05-04).
- **`.claude/skills/export/SKILL.md`** — description updated to match the framework's view-source export rewrite (2026-04-16).

### Step 2 — packages migration (pending)

To do:
- `git submodule add` for framework and penny-post (with tagged-release prompt for each).
- Verify all 14 thin wrappers are still thin delegates (no ejected customization).
- `sed` sweep on `.claude/skills/*/SKILL.md` to rewrite `../nla-framework/` → `packages/nla-framework/` and `../nla-penny-post/` → `packages/nla-penny-post/`.
- Targeted edits to `CLAUDE.md` (Environment section, penny post note), `README.md`, `reference/installed-packages.md`, `app/overview.md`.
- Remove `Read(../nla-framework/**)` and `Read(../nla-penny-post/**)` from `.claude/settings.local.json` if present.
- Run `/validate` structural check.

## Decisions Made

- **Split smaller changes from packages migration.** Two independent commits — easier to revert either if needed, easier to review.
- **Keep "Default to prose" bullet condensed.** Framework template's second sentence is helpful in framework context but redundant once the first sentence lands; this NLA's voice prefers terseness.
- **Adopt the packages migration now rather than defer.** It's the structural fix for nla-framework#15 (the permission-friction letter from 2026-03-30). Two months of living with the friction is enough.
- **Use the sed sweep for thin wrapper path rewrites.** Mechanical pattern substitution across many files — exactly the case `/maintain` calls out for `Bash`-based bulk edits.

## What Didn't Work

(Nothing abandoned yet.)

## Friction Log Entries Processed

- (None processed this session — the 2026-03-05 entry about architecture review remains open. Migration will likely close out the permission-friction line indirectly.)

## Debrief

(Pending — captured at session close via `/close`.)

## State at Close

(Pending — will be filled in at `/close`.)
