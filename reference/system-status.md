# System Status

Last updated: 2026-05-22

## Tasks

| Task | Status | Notes |
|------|--------|-------|
| Explore | Active | Default mode — answers questions from articles and framework source |

## Skills

| Skill | Status | Notes |
|-------|--------|-------|
| `/startup` | Active | Framework wrapper — loads context, enters office hours |
| `/maintain` | Active | Framework wrapper |
| `/friction-log` | Active | Framework wrapper |
| `/preferences` | Active | Framework wrapper |
| `/validate` | Active | Framework wrapper |
| `/install` | Active | Framework wrapper |
| `/update` | Active | Framework wrapper |
| `/check-updates` | Active | Framework wrapper |
| `/export` | Active | Framework wrapper |
| `/think` | Active | Framework wrapper |
| `/debrief` | Active | Framework wrapper |
| `/session-checkpoint` | Active | Framework wrapper |
| `/close` | Active | Framework wrapper |
| `/guide` | Active | Framework wrapper |
| `/check-feedback` | Active | Penny post wrapper |
| `/write-letter` | Active | Penny post wrapper |

## Recent Changes

- 2026-05-22: **Example NLAs catalog added.** New `examples/` directory with three working NLAs as git submodules (copydesk, duet, nla-claude-code) — source material for the explore task. Distinct from `packages/`: not installed dependencies, no `/update` involvement. `app/overview.md` gains a "Where Things Live" structure record per framework's 2026-05-07 structure-decisions protocol.
- 2026-05-20: **Packages/ migration** — framework and penny-post moved from sibling directories to git submodules at `packages/nla-framework/` (v0.0.9) and `packages/nla-penny-post/` (v0.0.1). Resolves nla-framework#15 permission friction.
- 2026-05-20: Applied framework intent updates — "NLA documents are source code" reframe, new "Default to prose for design conversations" execution principle, new `/session-checkpoint` skill, `/validate` and `/export` description refresh.
- 2026-03-30: Updated framework to `b63ed87` (log-only — no intent changes)
- 2026-03-30: Permission behavior test for framework; results sent as nla-framework#15
- 2026-03-12: Git repo initialized, README cleaned up
- 2026-03-09: Installed penny post extension (`/check-feedback`, `/write-letter`)
- 2026-03-09: Updated framework (validate wrapper — added coherence review mode)
- 2026-03-05: Project created via `/create-app`
