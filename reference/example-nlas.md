# Example NLAs

Source material for the explore task. Each entry is a working NLA, included as a git submodule under `examples/`, that gives Office Hours concrete evidence of how the framework plays out across distinct application domains.

**Not packages.** These don't get installed via `/install` and aren't tracked in `installed-packages.md`. They're read-only source material for synthesis — the explore task may quote, paraphrase, or point to them when answering questions.

**Why a separate directory.** `packages/` is reserved for installed dependencies (framework + extensions like penny post) — things this NLA needs to function, with intent files that `/update` integrates. Example NLAs are a different category: source material, no intent files, no integration step.

---

## How They're Used

The explore task (`app/explore.md`) draws on examples when:
- A visitor asks comparative questions (e.g., "how do different NLAs handle state?")
- A visitor wants to see how an NLA they've heard of actually works
- A question is best answered by pointing at a concrete pattern in a working system, not by paraphrasing what the articles say

Examples are particularly valuable for questions where the articles describe and the framework defines — but the visitor wants to see the design *land* somewhere specific.

---

## Lifecycle

**Initial clone:** Examples come along automatically via `git submodule update --init --recursive` (or `git clone --recurse-submodules` on first clone).

**Refresh to newer state (maintainer only):** Examples don't have intent files, so `/update` doesn't touch them. To advance an example's pin manually:

```bash
git -C examples/[name] fetch
git -C examples/[name] checkout [new-commit-or-tag]
git add examples/[name]
git commit -m "Advance examples/[name] to <description>"
```

Or to advance all examples to their respective `origin/HEAD`:

```bash
git submodule update --remote examples/
git add examples/
git commit -m "Refresh all example NLAs"
```

End users pick up new pins on their next `git pull` + submodule update.

---

## Entry Format

```markdown
### [name]

- **Repo:** [URL]
- **Pinned at:** [commit hash] ([tag if any], [date])
- **Default branch:** main | master
- **One-line:** What kind of NLA this is and what makes it a useful exemplar
- **Notable for:** [Which kinds of questions this NLA is especially good evidence for]
```

---

## Entries

### copydesk

- **Repo:** https://github.com/mightytech/copydesk
- **Pinned at:** `022c3c5` (no tag, 2026-05-22)
- **Default branch:** master
- **One-line:** Editorial workflow NLA — applies a copy desk's review process to drafts.
- **Notable for:** Questions about transformation-shape NLAs, multi-stage review workflows, and how stated values shape editorial judgment.

### duet

- **Repo:** https://github.com/mightytech/duet
- **Pinned at:** `f23f7e6` (no tag, 2026-05-22)
- **Default branch:** master
- **One-line:** Creative composition NLA — collaborative writing partner.
- **Notable for:** Questions about persistent-shape NLAs, session continuity, creative collaboration, and the difference between transformation and creation.

### nla-claude-code

- **Repo:** https://github.com/mightytech/nla-claude-code
- **Pinned at:** `487b011` (no tag, 2026-05-22)
- **Default branch:** main
- **One-line:** Claude Code Manager — a tool-using NLA that drives Claude Code itself.
- **Notable for:** Questions about tool-using NLAs, dev tooling, hybrid architecture, and meta-NLAs (NLAs that drive other LLM systems).

---

## Not Currently Included

Considered but skipped:
- **facebook-moderation**, **nla-writer** — private repos. Skipped per maintainer direction (private for a reason).
- **copydesk-orig**, **duet-music**, **duet-plugin** — predecessor/variant/plugin-export of NLAs already included; would be redundant.
- **nla-archetypes** — meta-resource rather than an exemplar; reconsider if a question pattern surfaces that this would address.
- **nla-creative-helpers**, **nla-process-helpers** — extension packages, not standalone NLAs. Use `/install` if they're ever needed as installed extensions.
- **nla-template**, **test-nla-claude-code** — scaffolding/testing repos, not exemplars.

---

*Maintained by hand. Updated when example pins advance or new examples are added.*
