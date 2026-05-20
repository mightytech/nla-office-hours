# Installed Packages

Record of NLA packages installed in this project. Maintained by `/install` and `/update`.

---

## NLA Framework

- **Installed:** 2026-03-05
- **State at install:** commit `db32216`
- **What was done:** Project created via `/create-app`. Framework provides grounding principles, maintenance workflows, configuration infrastructure, and the shared skill library (13 thin wrapper skills).
- **Source:** `packages/nla-framework/` (git submodule, since 2026-05-20; originally `../nla-framework/`)

### Updated 2026-03-09

**Package state:** commit `86e68d4`

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `skills-intent.md` | Added coherence review mode to `/validate` purpose | Updated validate wrapper description to include coherence review |

**Notes:** Framework also added `validate-coherence.md` core file and updated `validate.md` dispatcher — both propagate automatically via thin wrapper delegation.

### Updated 2026-03-30

**Package state:** commit `b63ed87`

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| (none) | No intent file changes | No integration changes needed |

**Notes:** Three framework-internal commits since last update: example catalog additions (Office Hours, Claude Code Manager, revised complexity scale), friction log entry, session logs. No intent files modified — update is log-only.

### Updated 2026-05-20

**Package state:** `v0.0.9` (commit `b1d021b`) — pinned to tagged release as git submodule at `packages/nla-framework/`.

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `CLAUDE-intent.md` | Principle #2 reframed to "NLA documents are source code"; new "Default to prose for design conversations" bullet; environment path moved to `packages/nla-framework/` | Updated CLAUDE.md grounding principles, execution principles, and Environment section accordingly |
| `skills-intent.md` | All wrapper paths moved to `packages/nla-framework/`; new `/session-checkpoint` skill added; `/validate` and `/export` descriptions updated | Sed sweep across all `.claude/skills/*/SKILL.md` files; created `session-checkpoint` thin wrapper; updated `validate` and `export` wrapper descriptions; added `/session-checkpoint` row to CLAUDE.md and `app/overview.md` skills tables |
| `structure-intent.md` | Added `packages/` to directory tree; settings.local.json drift note | Added `packages/` entry to CLAUDE.md Environment table and README.md directory tree |
| `install.md` | Framework now a submodule, not a sibling; `Read(../nla-framework/**)` removed from declared permissions | Removed `Read(...nla-framework/**)` and `Read(...nla-penny-post/**)` from `.claude/settings.local.json` |
| `package-intent.md` | Shippability convention; package wrappers point at `packages/[name]/` | Carried into penny-post handling (see Penny Post entry below) |

**Notes:** This is the packages/ migration (framework change 2026-04-15). Both dependencies moved from sibling directories to git submodules pinned at their latest tagged releases. Resolves the long-standing permission-friction issue documented in feedback-log (`#1`, 2026-03-30) and reported to the framework as nla-framework#15. Four local-only framework commits (incl. `a57d225` foundations recalibration) remain unpushed in the framework maintainer's working tree at `../nla-framework/` (separate from this project's submodule, which reads from `packages/nla-framework/`); the submodule is pinned to origin's v0.0.9 per user direction.

---

## Penny Post

**Source:** `packages/nla-penny-post/` (git submodule, since 2026-05-20; originally `../nla-penny-post/`)
**Installed:** 2026-03-09
**Package state:** commit `68635f5`

### What was done

| Intent File | Integration Point | Changes Made |
|-------------|------------------|--------------|
| `CLAUDE-intent.md` | `CLAUDE.md` | Added `/check-feedback` and `/write-letter` to skills table. Added penny post environment note with feedback file locations. |
| `skills-intent.md` | `.claude/skills/` | Created thin wrappers `check-feedback/SKILL.md` and `write-letter/SKILL.md`, both delegating to `../nla-penny-post/app/`. |

### Notes

Downstream files updated for consistency: `app/overview.md` skills table, `reference/system-status.md` skills table and recent changes. The penny post manifest predates the permission declaration convention — no permissions section exists. Read access to `../nla-penny-post/` added to `settings.local.json` since the thin wrappers delegate there.

### Updated 2026-05-20

**Package state:** `v0.0.1` (commit `1ef501e`) — pinned to tagged release as git submodule at `packages/nla-penny-post/`.

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `CLAUDE-intent.md` | Penny post now a submodule, not a sibling | Updated CLAUDE.md Environment section accordingly (handled with framework migration above) |
| `skills-intent.md` | Wrapper paths moved to `packages/nla-penny-post/` | `check-feedback` and `write-letter` wrappers rewritten via sed sweep |
| `install.md` | New Permissions section declares only `Bash(gh:*)` (Read no longer needed under packages convention) | `Read(...nla-penny-post/**)` removed from `.claude/settings.local.json`; `Bash(gh:*)` already pre-approved |

**Notes:** Picked up alongside the framework packages/ migration. Pinned to v0.0.1 (the migration's Phase 2 commit); one internal session-log commit on origin beyond v0.0.1 is intentionally out of scope.
