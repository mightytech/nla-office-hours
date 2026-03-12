# Installed Packages

Record of NLA packages installed in this project. Maintained by `/install` and `/update`.

---

## NLA Framework

- **Installed:** 2026-03-05
- **State at install:** commit `db32216`
- **What was done:** Project created via `/create-app`. Framework provides grounding principles, maintenance workflows, configuration infrastructure, and the shared skill library (13 thin wrapper skills).
- **Source:** `../nla-framework/`

### Updated 2026-03-09

**Package state:** commit `86e68d4`

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| `skills-intent.md` | Added coherence review mode to `/validate` purpose | Updated validate wrapper description to include coherence review |

**Notes:** Framework also added `validate-coherence.md` core file and updated `validate.md` dispatcher — both propagate automatically via thin wrapper delegation.

---

## Penny Post

**Source:** `../nla-penny-post/`
**Installed:** 2026-03-09
**Package state:** commit `68635f5`

### What was done

| Intent File | Integration Point | Changes Made |
|-------------|------------------|--------------|
| `CLAUDE-intent.md` | `CLAUDE.md` | Added `/check-feedback` and `/write-letter` to skills table. Added penny post environment note with feedback file locations. |
| `skills-intent.md` | `.claude/skills/` | Created thin wrappers `check-feedback/SKILL.md` and `write-letter/SKILL.md`, both delegating to `../nla-penny-post/app/`. |

### Notes

Downstream files updated for consistency: `app/overview.md` skills table, `reference/system-status.md` skills table and recent changes. The penny post manifest predates the permission declaration convention — no permissions section exists. Read access to `../nla-penny-post/` added to `settings.local.json` since the thin wrappers delegate there.
