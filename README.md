# NLA Office Hours

A thinking partner for exploring ideas about
[Natural Language Applications](https://github.com/mightytech/nla-framework).
You ask questions grounded in the published articles and the framework source
code — about what NLAs are, how they work, where they break down, and what
they might mean. The NLA synthesizes across both sources, draws connections the
articles don't make explicit, and points to the actual code when you want to
see how things work.

This isn't a search engine over documents. People who come to office hours
already have access to the articles — if they're asking here, they want the
synthesis and the evidence from the actual running system that reading alone
doesn't give them.

## What Is an NLA?

A Natural Language Application is software where the runtime is an LLM and the
source code is written in prose. The documents in `app/` aren't documentation
about the application — they *are* the application. When behavior needs to
change, you edit the prose. The LLM reads it and does what it says.

If that sounds unusual, two paths for the curious:

- **Read about it:**
  [The Documentation Is the Application](content/the-documentation-is-the-application.md)
  — a probe report exploring what software becomes when language is the runtime
- **Talk to one:** That's what this is.

---

## Getting Started

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [NLA Framework](https://github.com/mightytech/nla-framework) — pulled in as
  a git submodule at `packages/nla-framework/`. If you cloned without
  `--recurse-submodules`, run `git submodule update --init` once to fetch it.

### Quick Start

1. Start Claude Code in this directory
2. Run `/startup` — loads the article index, checks available sources, and
   enters office hours mode
3. Ask a question — the NLA answers grounded in the articles and the
   framework source

---

## Using It

**The rhythm:** Run `/startup`. Ask questions. Follow threads where you're
curious. Run `/close` when you're done.

**What kinds of questions work well:**

- **Conceptual** — "What are NLAs?" "What does 'values as source code' mean?"
- **Implementation** — "How does the update system handle user modifications?"
  "Show me how the feedback triage works."
- **Skeptical** — "Isn't this just prompt engineering?" "How is this different
  from RAG?"
- **Comparative** — "How do NLAs relate to MCP and A2A?" "Why not just use
  regular code?"
- **Building** — "How do I build one?" (The NLA points you to the framework's
  `/create-app`.)
- **Process** — "How was the /debrief skill designed?" "What do the
  framework's session logs reveal about how the LLM uses stated values
  during design work?" These aren't syslogs — they're design journals.
  The framework's friction logs, feedback logs, and session logs trace
  the *why* behind every significant change.

**Where answers come from:** The published articles provide the author's
framing — the arguments, the analogies, the conceptual architecture. The
framework source provides living evidence — how things actually work, details
the articles couldn't fit, connections between pieces. The best answers draw
on both. When neither source covers a question, the NLA says so — and can
escalate to the maintainer if the question is worth pursuing.

---

## How It Works

The documents in `app/` are the application:

```
nla-office-hours/
├── app/                          # The application
│   ├── overview.md               # How the pieces connect
│   ├── explore.md                # Task: how to answer questions
│   ├── startup.md                # App-specific session initialization
│   ├── config-spec.md            # What's configurable
│   └── shared/                   # Context shared across the system
│       ├── values.md             # Commitments and priorities
│       ├── voice.md              # Tone and personality
│       └── common-patterns.md    # Recurring question patterns
├── content/                      # Published articles and whitepapers
├── packages/                     # Git submodule dependencies (framework + extensions)
├── examples/                     # Example NLAs as git submodules — source material
├── reference/                    # Maintenance records
│   ├── design-rationale.md       # Why the system is built this way
│   ├── friction-log.md           # Internal observations
│   ├── feedback-log.md           # External feedback
│   ├── system-status.md          # Current state
│   ├── installed-packages.md     # Package history
│   └── sessions/                 # Session logs
├── config.md                     # User preferences (gitignored)
├── CLAUDE.md                     # Runtime identity
├── CONTRIBUTING.md               # How to contribute
└── .claude/skills/               # Skill wrappers
```

If you want to understand why the NLA makes the decisions it makes, start
with `app/shared/values.md`.

### Customization

| Want to change... | Edit this file |
|-------------------|---------------|
| How answers sound | `app/shared/voice.md` |
| What the NLA prioritizes | `app/shared/values.md` |
| How questions are handled | `app/explore.md` |
| Question patterns to recognize | `app/shared/common-patterns.md` |
| User preferences | Run `/preferences` |

### Configuration

Run `/preferences` to create or edit your personal configuration. Configuration
is wide open — write natural language preferences to change any aspect of
behavior. Your `config.md` is gitignored (it belongs to you, not the
application).

---

## Improving It

NLAs improve through use:

1. Use the application — ask questions, notice what works and what doesn't
2. Notice friction — an answer that missed the mark, a connection that wasn't
   drawn, a question type it didn't handle well
3. Log observations with `/friction-log`
4. Process them with `/maintain`

Outside contributions are welcome through observations and feedback. See
[CONTRIBUTING.md](CONTRIBUTING.md) for how this project thinks about
contributions — it's different from most open source.

---

## Upgrading

To pull the latest version of the project — including any newer pins on
framework, packages, and example NLAs:

```bash
git pull
git submodule update --init --recursive
```

`git pull` advances the parent repo (which may move submodule pointers).
`git submodule update --init --recursive` then checks out the new pointers
and initializes any submodules that weren't present before.

`/update` is a maintainer-only tool — it advances submodule pins to newer
remote versions *and* integrates intent changes from updated packages into
this project's own files. End users don't need it; pulling the parent repo
already gives them whatever pins the maintainer has integrated.

---

## Getting Help

Ask the AI. Run `/guide` for a contextual walkthrough, or just describe what
you're trying to do — the AI has read the documentation and can orient you.

---

## Learn More

- [NLA Framework](https://github.com/mightytech/nla-framework) — the
  foundation that NLAs (including this one) are built on
- [The Documentation Is the Application](content/the-documentation-is-the-application.md)
  — a probe report exploring the NLA paradigm
- [CONTRIBUTING.md](CONTRIBUTING.md) — how to contribute to this project
