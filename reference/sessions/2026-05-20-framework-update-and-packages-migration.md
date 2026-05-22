# Maintenance Session: Framework Update and Packages Migration

**Date:** 2026-05-20
**Status:** Complete (pending push + tag at `/close`)
**Session window:** 2026-05-20 → 2026-05-22 (mid-session decision to extend with example NLAs catalog landed on 2026-05-22)

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

### Step 2 — packages migration (complete)

Landed across three commits:

**Chunk A — `Add packages/ submodules`** (`69b95d7`):
- Added `packages/nla-framework/` as submodule pinned at `v0.0.9` (commit `b1d021b`).
- Added `packages/nla-penny-post/` as submodule pinned at `v0.0.1` (commit `1ef501e`).
- Verified all 15 existing wrappers were thin delegates before proceeding.

**Chunk B — `Rewrite paths from sibling-directory to packages/ submodule convention`** (`9370028`):
- Sed sweep over 16 thin wrappers (`.claude/skills/*/SKILL.md`): `../nla-framework/` → `packages/nla-framework/`, `../nla-penny-post/` → `packages/nla-penny-post/`.
- Updated CLAUDE.md (Modes section, build-NLA pointer, Environment section — added `packages/` row to directory table, refreshed framework + penny-post location notes).
- Updated README.md (Prerequisites note now describes submodule init; directory tree includes `packages/`).
- Updated app/overview.md (opening paragraph + ASCII diagram).
- Updated app/explore.md (Sources section + Penny Post install hint) and app/shared/common-patterns.md (build-NLA redirect).
- Updated reference/installed-packages.md (Source paths for both packages + new 2026-05-20 update records under each package's section).
- Removed now-redundant `Read(.../nla-framework/**)` and `Read(.../nla-penny-post/**)` from `.claude/settings.local.json` (gitignored — local edit only).

**Chunk C — structural validation + system-status refresh** (this commit):
- Ran `/validate` structural check via subagent. Found 2 issues, both outside the migration scope itself.
- Fixed: `reference/system-status.md` was stale (missing `/session-checkpoint`, old "Last updated" date, no Recent Changes entry for today's migration).
- Deferred: open 2026-03-05 friction entry still references `../nla-framework/...` path — will be updated when that entry is processed.

Net effect: every cross-directory `Read(...)` permission this NLA needed before now resolves in-project. The 2026-03-30 permission-friction feedback log entry is structurally resolved by the migration; will be marked resolved + archived at `/close`.

### Step 3 — example NLAs catalog (2026-05-22)

Phase 1 (design) decisions:
- **Catalog as source material, not packages.** Examples live at `examples/` (new top-level directory). Distinct from `packages/` because semantically different: source material the explore task synthesizes from, not installed dependencies with intent files. `/update` and `/install` don't act on them.
- **5 candidates considered, 3 included.** copydesk, duet, nla-claude-code added. facebook-moderation and nla-writer skipped (private repos — Office Hours is public; embedding private submodule URLs would break clones for anyone without credentials). Process helpers and penny post not in examples — they're packages, accessible via `packages/` already.
- **Pinned at commits, not tags.** None of the three have tags yet; pinned to current origin HEAD.
- **End-user update flow:** standard git (`git pull && git submodule update --init --recursive`). `/update` remains maintainer-only.
- **Adopted the framework's structure-decisions protocol.** New "Where Things Live" section added to `app/overview.md` recording attribution for all top-level paths (mostly `[framework default]`; `content/`, `examples/`, and CONTRIBUTING.md are `[domain decision]`). Includes a Decision Sources table.

Phase 2 (execute) landed:
- Three `git submodule add` operations for copydesk (`022c3c5`), duet (`f23f7e6`), nla-claude-code (`487b011`).
- Updates to `app/explore.md` Sources section (explicit examples callout), `app/overview.md` (opening paragraph, How It Connects diagram, Document Index, new Where Things Live section), `README.md` (directory tree, end-user upgrade docs that distinguish `/update` from plain `git pull`).
- New `reference/example-nlas.md` tracking file with one-line summaries, notable-for hints, and a "Not Currently Included" section documenting what was considered and why.
- New friction log entry queued for a framework letter: the gap between `git pull` (end-user) and `/update` (maintainer) deserves a tiny `bin/update-app` wrapper script, AI-aware, possibly at framework level.

## Decisions Made

- **Split smaller changes from packages migration.** Two independent commits — easier to revert either if needed, easier to review.
- **Keep "Default to prose" bullet condensed.** Framework template's second sentence is helpful in framework context but redundant once the first sentence lands; this NLA's voice prefers terseness.
- **Adopt the packages migration now rather than defer.** It's the structural fix for nla-framework#15 (the permission-friction letter from 2026-03-30). Two months of living with the friction is enough.
- **Use the sed sweep for thin wrapper path rewrites.** Mechanical pattern substitution across many files — exactly the case `/maintain` calls out for `Bash`-based bulk edits.

## What Didn't Work

- Initial `git add` for chunk B included `.claude/settings.local.json`, which is gitignored. Recovered with `git reset` and re-added without it. Worth noting that the structure-intent doc spells this out — settings.local.json is local-only by design.

## Friction Log Entries Processed

- **2026-03-05 (Architecture review applies traditional software thinking to NLA patterns):** still open. Path in the entry's "Affected documentation" field now stale (`../nla-framework/...`) but deferred — will be updated when the entry itself is processed. The entry is framework-level and remains a letter candidate.

## Friction Log Entries Added

- **2026-05-20 (app/explore.md and app/overview.md don't restate the "NLA documents are source code" principle):** logged for a future session. Real edit, deserves voice judgment.
- **2026-05-22 (End-user update flow is git-native — worth a small wrapper, possibly framework-level):** framework letter candidate. Names the gap between `git pull` (end-user) and `/update` (maintainer); proposes a tiny `bin/update-app` script + AI awareness as the bridge.

## Feedback Log Entries Pending Resolution

- **2026-03-30 (Permission behavior test — symlinks vs. direct sibling reads):** Should be marked resolved as part of this session's `/close`. The framework's packages/ migration (which this NLA just adopted) is the structural fix for the permission friction the test was investigating. Original feedback ask (run the test and report) was completed in March; the underlying friction is now resolved.

## Debrief

(Pending — captured at session close via `/close`.)

## State at Close

**What's working:**
- Framework + penny-post as packages submodules, pinned to v0.0.9 / v0.0.1.
- Three example NLAs as `examples/` submodules: copydesk, duet, nla-claude-code.
- "Where Things Live" structure record in `app/overview.md` captures all top-level path decisions with attribution.
- Operative content references the new paths consistently: explore.md sources, overview.md hierarchy + diagram, README directory tree + end-user upgrade docs.
- `reference/example-nlas.md` tracks examples separately from `installed-packages.md`.
- system-status.md current (will need one more refresh for the 2026-05-22 examples work, pending at `/close`).

**What's pending:**
- Final commit for Step 3 (this Phase 2 of the examples work).
- One more `/validate` structural pass (the previous pass was before examples landed).
- system-status.md update reflecting the 2026-05-22 examples work.
- Push to origin (with annotated tag) at `/close`.
- Mark feedback log entry for 2026-03-30 permission test as resolved.
- 2026-03-05 architecture-review friction log entry remains open.
- Framework-letter material accumulated: the bash-script idea + the 2026-03-05 architecture-review observation. Could be one letter or two.

**Where to pick up:** Two open friction entries are now framework-letter candidates. The structurally resolved permission line means this NLA isn't waiting on infrastructure improvements anymore — open work is enrichment (the example-NLAs source/principle-anchoring work in `app/`) rather than blockers.
