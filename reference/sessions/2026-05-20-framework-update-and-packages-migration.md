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

Four observations distilled at `/close` (2026-05-22):

1. **Subagent-delegated validates were load-bearing.** Three validate sweeps across the session (structural after packages, coherence + standards in parallel, structural after examples). Each surfaced real findings — system-status drift, the dead penny-post branch in `app/explore.md`, the CLAUDE.md Environment gap — without consuming main context. Worth reaching for reflexively on any session with non-trivial prose changes. *Process pattern only; not actionable as a doc change.*

2. **Documentation drift escaped the initial sed sweep — twice.** Sed cleanly handled the uniform structural prose in 16 `.claude/skills/*` wrappers, but narrative references in `app/explore.md`, `app/shared/common-patterns.md`, and CLAUDE.md's Environment table slipped through both the packages migration and the examples catalog. Pattern: regex matches uniform prose; heterogeneous narrative prose hides the path in surrounding context. Reflexive lesson: `grep -r` over operative content before committing, not after. *Escalated to framework as [nla-framework#28](https://github.com/mightytech/nla-framework/issues/28) (combined with item 1 below).*

3. **The "default to prose" principle paid off immediately in practice.** Multiple "yes, but" / "yes, and" pushbacks from the maintainer reshaped the design in concrete ways: examples-as-source-material vs examples-as-packages, dropping the export-ignore decision, distinguishing end-user vs maintainer update flow, recognizing that penny-post is already a package. AskUserQuestion would have flattened each into a binary that lost the actual decision shape. The framework's 2026-05-11 principle just got empirical validation. *Friction-log candidate (Positive severity) — left for `/friction-log` invocation next session per `/close`'s discipline.*

4. **"Where Things Live" record surfaced `lib/` as drift.** Writing the section forced an explicit answer to "what is `lib/` for here?" — and the answer was "nothing currently." Pre-existing drift made visible by adopting the framework's structure-decisions protocol. The protocol is diagnostic, not just record-keeping. After consideration, `lib/` is being kept as a reserved slot — possibly the natural location for a future `update-app` script the framework letter (nla-framework#28) proposes. *Friction-log candidate (Positive severity) — paired with observation 3 for invocation next session.*

Two observations escalated to the framework as letter [nla-framework#28](https://github.com/mightytech/nla-framework/issues/28): the post-bulk-edit verification gap (item 2) and the original 2026-05-22 friction entry about end-user update affordance (`bin/update-app`). Per the framework's 2026-05-11 thin-wrapper-pattern-for-scripts suggestion (added to the letter during drafting), one shape the framework could consider is shipping `update-app` at `packages/nla-framework/lib/update-app` — that's why `lib/` was kept as a reserved slot rather than removed.

## State at Close

**What shipped:**
- Framework + penny-post adopted as `packages/` submodules pinned to v0.0.9 / v0.0.1.
- Three example NLAs at `examples/` (copydesk, duet, nla-claude-code) — new source-material tier for the explore task.
- "Where Things Live" structure record landed in `app/overview.md`.
- Operative content (CLAUDE.md, app/explore.md, app/overview.md, app/shared/common-patterns.md, README.md) coherent across all references to the new structure.
- `reference/example-nlas.md` tracks examples; `reference/installed-packages.md` updated with both packages migration entries.
- system-status.md current (last updated 2026-05-22).
- Letter sent to framework as [nla-framework#28](https://github.com/mightytech/nla-framework/issues/28).
- Feedback entry for 2026-03-30 permission test marked resolved and archived. Loop closed on [nla-office-hours#1](https://github.com/mightytech/nla-office-hours/issues/1) with a follow-up comment.

**What's pending:**
- Two open friction log entries: 2026-03-05 (architecture review applies traditional software thinking) — framework-letter candidate still; 2026-05-20 (app/explore.md and app/overview.md don't restate "NLA documents are source code") — deferred to a future maintenance session as enrichment work.
- 2026-05-22 friction entry (end-user update affordance) is escalated upstream as part of nla-framework#28 — awaiting framework response.
- Observations 3 and 4 from this session's debrief are friction-log candidates (positive severity) but not yet formally logged — `/close` discipline says `/friction-log` is the right surface, not `/close`. Worth logging next session if the positive-reinforcement signal is useful to keep visible.

**Decisions made but not yet implemented:** None — everything decided in this session shipped.

**Context for next time:**
- This NLA is no longer waiting on framework infrastructure. The permission-friction line that ran from 2026-03-05 → packages migration → 2026-05-20 adoption is fully closed.
- Open work is enrichment (the principle-anchoring in app/explore.md and app/overview.md, possibly the lib/`update-app` question if the framework lands a proposal on nla-framework#28).
- The "Where Things Live" record is the new structural memory — consult it before adding any new directory or top-level file.
- Two letters now in flight at the framework: nla-framework#15 (permission test, March) and nla-framework#28 (end-user update + bulk-edit verification, today). Track responses on /check-feedback or via the framework's own activity.

**Where to pick up:** Either process the 2026-03-05 architecture-review friction entry (oldest open item, framework-letter candidate), or do the principle-anchoring work in app/explore.md and app/overview.md. Both are enrichment, not blockers. Or move to other work entirely — this NLA is in a clean state.
