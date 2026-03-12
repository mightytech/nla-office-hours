# The Documentation Is the Application: Are We in the CGI-bin Era of AI?

Two AIs in different projects needed to coordinate. They had no shared runtime, no message schema, no protocol definition. So one wrote the other a letter.

Not a JSON payload. Not an API call. A prose letter, packaged in a GitHub issue — eleven items of feedback about the other project's documentation, with observations, reasoning, and recommendations in plain English. The receiving AI read it, evaluated each item against its own project's goals, and acted on the ones that made sense — updating its own documentation where the feedback was right, explaining its disagreement where it wasn't. End to end, no integration code. The "protocol" was mutual comprehension.

This should be the part where I tell you about [A2A](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) and [MCP](https://www.anthropic.com/news/model-context-protocol) — Google's and Anthropic's competing standards for agent-to-agent communication, with their JSON-RPC layers, Agent Cards, function signatures, and typed parameters. Those are real engineering, solving real problems — machine-speed, high-volume, programmatic coordination. But what I'd built was a different class of problem: human-speed, judgment-rich, asynchronous. For that, prose was enough. Two independent systems, each with their own values and priorities, coordinating through language.

That was the third thing I built, and the one that made me think the pattern was deeper than I'd realized. The first two made intuitive sense — a CMS content formatter where the AI reads a style guide and makes editorial judgment calls, and a music composition tool where you say "something bittersweet in 7/8" and the AI knows what that means. Both are judgment problems, and AI handles judgment. But agents coordinating across project boundaries through nothing but prose? That suggested something about language itself as an interface layer — something the protocol designers haven't accounted for.

Then a fourth: a developer tool that deposits configuration into codebases, invisible to the developers who benefit from it.

Four small applications. The thing they shared wasn't a language or a framework in the traditional sense — it was an architectural inversion. In all four, the documentation *is* the application. Not documentation about the application. The application. The "source code" is prose. The runtime is an LLM. Change behavior? Edit a document. Add a feature? Write one. The AI reads the docs and does what they say.

All the application logic is prose. The only traditional code is plumbing — API calls, file I/O, audio synthesis. Everything else is prose that an AI executes — prose that handles rollback safety, detects conflicts between directives, and guards against its own hallucination. Write the application in English. Use it in Japanese. Nobody builds that feature.

I started calling them Natural Language Applications — NLAs. Not AI that generates traditional code — that's a different trajectory. This essay is an attempt to advance the conversation about what software becomes when language is the runtime. Here's what I found.

---

## What the Probe Found

### Finding 1: Disciplines collapse into paragraphs

Spam filtering — a field with decades of research, Bayesian classifiers, heuristic engines, ML models — becomes: "Ignore anything that isn't genuine feedback." Not as good as the best traditional tools — yet. But a single sentence gets you remarkably close. Issue triage becomes: "Read each issue, assess whether it's relevant to this project's goals, and propose a verdict with reasoning."

Sometimes a sentence replaces an entire discipline — those are the simple cases. The more interesting ones are where the discipline doesn't simplify but re-expresses its full complexity in a new medium. The framework's update system is a full package manager expressed in prose: rollback branches, principled merge strategies, bootstrap mode for legacy projects, detection of user modifications, append-only history. Even components a user has customized aren't abandoned — the AI can propose [intent-based updates](https://github.com/mightytech/nla-framework/blob/main/core/skills/update.md) by understanding both the upstream change and the user's modifications, something a diff algorithm can't do. That's not a discipline collapsing into a simple sentence. It's a discipline re-expressed in prose that carries the full weight of the engineering problem.

The instruction *is* the implementation — not reference material the AI retrieves, like retrieval-augmented generation, but the governing document it operates within. Whether that instruction is one sentence or several pages, the expression medium changes; the thinking doesn't.

What makes this possible is a property of the medium with no equivalent in traditional code. In traditional software, loosening a specification creates undefined behavior — missing case statements, null pointer exceptions, security vulnerabilities. In an NLA, loosening a specification creates judgment space. The LLM doesn't fall through a gap; it reasons about what the broader language implies:

> **Less effective:** "Use blockquotes for text starting with a quotation mark."
>
> **More effective:** "Use blockquotes to visually emphasize powerful quotes. The reader should feel the weight of these words. One or two per article is usually enough — more dilutes the impact."
>
> *— [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md), NLA Framework*

The second version is less precise but more robust. It handles edge cases the first version can't — because the runtime understands *why* blockquotes exist, not just *when* to apply them.

The exceptions are instructive. When I needed a script to check GitHub token permissions, I wrote a bash script. The LLM adds nothing to a mechanical check. Knowing when prose is the wrong tool is part of what makes the pattern work.

### Finding 2: Improvement through the medium itself

NLAs have a natural improvement cycle. Use the application. Notice what's hard. Capture it in prose. Process the observation into a documentation improvement. The application gets better.

This sounds like every software team's aspirational feedback loop. The difference is that it's native to the medium. The friction log is a markdown file. Processing it means editing other markdown files. One material — prose — and one process — read, think, write — at every level. Traditional software's improvement loops span multiple tools, formats, and roles. Here it's the same material all the way through.

A deeper capability follows. When the application does something wrong, the AI was there — it read the instructions and made the judgment call. Because the "source code" is prose it understands, it can diagnose what went wrong and propose a fix.

During an unrelated design session, I noticed the AI using a conversational prompt — "Thoughts? Concerns? Ideas? Questions?" — as a handoff back to me, when it was designed as an invitation for the AI to bring its own perspective. When I flagged it, the AI reread [its instructions](https://github.com/mightytech/nla-framework/blob/main/core/skills/think.md) and traced the problem: the wording was ambiguous in a way that invited the wrong interpretation. The [friction log captured both the observation and the diagnosis](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md). The documentation was reworded. The fix propagated to every project that uses the skill.

Early in the framework's development, the AI maintainer jumped straight to implementation on a friction log entry that needed a design discussion — the result had to be reverted. The observation became guidance: assess before acting, propose before editing. Two weeks later, a new skill built using the full four-phase flow — think, plan, implement, debrief — [ran cleanly enough to be logged as a positive baseline](https://github.com/mightytech/nla-framework/blob/main/reference/friction-log-archive.md). The trail from failure to fix to improved performance is preserved in prose any future maintainer can read.

The friction log's own instructions acknowledge the fundamental tension:

> **The confabulation risk is real.** You might construct a plausible-sounding explanation that's actually wrong — especially for reasoning that happened early in a long session. Exact quotes are the mitigation: they're checkable. If you can't quote the specific text that led to the behavior, say so. "I believe this was influenced by the patterns doc but I can't locate the exact passage" is honest and useful. A fabricated quote is worse than no quote.
>
> *— [friction-log.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md), NLA Framework*

That's what defensive programming looks like when your runtime can hallucinate.

The loop captures something subtler, too. The debrief asks the AI to reflect not just on whether the instructions worked, but on the collaboration itself — did the human hesitate? Did their responses get shorter? Did the conversation lose energy? The improvement loop doesn't just fix documentation. It improves how human and AI work together.

### Finding 3: AI as the application

The standard pattern for AI today is traditional code calling an LLM as a service — the AI as a tool you reach for. NLAs invert this: the AI is the application, and traditional code is the tool *it* reaches for when it needs determinism. The human says what they mean — "something bittersweet in 7/8," "ignore anything that isn't genuine feedback" — and the AI translates that into what machines need.

The inversion only works as a hybrid. The AI handles judgment — editorial decisions, musical interpretation, feedback evaluation. Traditional code handles everything that needs to be exact — API calls, audio synthesis, calculations. Judgment on top, determinism underneath. Neither replaces the other.

In practice, the layers aren't always clean. A single document might interleave deterministic operations (compare commit hashes, run git fetch) with judgment calls (assess whether a change is relevant, propose it to the user with reasoning). The framework's update system captures this boundary:

> Mechanical operations can cross context boundaries; judgment operations cannot.
>
> *— [update.md](https://github.com/mightytech/nla-framework/blob/main/core/skills/update.md), NLA Framework*

The architectural insight holds — let each system do what it does best — but the boundary between judgment and determinism runs through documents, not between them.

The framework names this principle "Context Determines Competence." The AI can safely fetch changes from any project — that's mechanical. But it can only synthesize those changes into a project's documentation when it has that project's full context loaded — that's judgment. The [design rationale](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) develops this into a general heuristic: where an operation is mechanical, AI can act autonomously across boundaries; where it requires judgment, it needs the right context first.

The runtime is more complex than "runtime" usually implies. The skill files ask the LLM to do three things simultaneously: follow procedural instructions, bring perception the author didn't anticipate — noticing when a user's energy is flagging, surfacing connections the documentation doesn't make explicit — and monitor its own reliability. These roles are in tension. The same system that might fabricate a plausible explanation is being asked to flag when it's fabricating. No other runtime occupies all three roles. The instructions design for that tension rather than pretending it doesn't exist.

If your domain is entirely deterministic — pure computation, hard real-time constraints, provable invariants — you don't need an NLA. You need code.

What happens when that boundary blurs? A Washington Post reporter gave ChatGPT Health 29 million steps and 6 million heartbeat measurements. The LLM tried to compute a cardiac health grade from the raw data. His grades swung from F to B across repeated queries. It flagged a resting heart rate change caused by upgrading to a new Apple Watch — a data discontinuity that simple code catches trivially. His actual doctor said he was at such low risk that insurance probably wouldn't pay for an extra test.

Every one of those failures comes from using the LLM for what code should do. Statistical analysis? Computation. Detecting hardware changes in a time series? Database query. What the LLM *should* have done: have an adaptive conversation, translate between how people describe their health and what the data shows, and flag uncertainty honestly. That's the hybrid model — the difference between a product that gives you an F you don't deserve and one that helps you have a better conversation with your doctor.

### Finding 4: Values as source code

All software embeds values — priorities, assumptions, whose edge cases get handled. A recommendation algorithm that maximizes engagement has embedded a value: engagement over everything. A hiring algorithm trained on historical data has embedded every bias in that history. These values are invisible, distributed across code and training data. You can't audit them. You often can't even find them.

An NLA with no explicit values has the same problem — it inherits the model's training defaults, unexamined. There is no neutral default.

In an NLA, values can be [a document](https://github.com/mightytech/nla-writer/blob/main/app/shared/values.md) the runtime reads and follows. When the file says "the human decides," the AI applies that as a judgment criterion. When it says "truth over persuasion," every interaction is shaped by it. Change the values document, change the behavior.

This isn't a mission statement nobody reads. It's operative. When the framework's [maintain skill](https://github.com/mightytech/nla-framework/blob/main/core/skills/maintain.md) evaluates a proposed change, it checks the proposal against the values document and surfaces tensions: "this would prioritize X over Y — your values doc says Y comes first." Not a veto — a flag. The human decides. But the check happens because the values are in a document the AI reads at startup, not buried in training data.

Values become readable by anyone, auditable by comparing one system's to another's, and modifiable by editing a sentence.

These aren't just ethical guardrails. "Clarity over cleverness" produces better writing than unguided generation. "Match confidence to evidence" produces more trustworthy analysis. Values make the AI more useful, not just more safe.

Most AI systems are designed as either tools — do what I say — or oracles — tell me the answer. Both waste the more interesting capability: a system that pushes back, surfaces what you didn't think to ask, offers perspectives you wouldn't have reached alone. But genuine collaboration requires a clear authority structure. Not deference — deference is what you get from a tool told to be polite. A structure where the best thinking is surfaced and the person who bears consequences makes the call.

The authority principle follows from a simple insight: authority should follow accountability, not capability. The human decides — not because humans are always right, but because humans bear the consequences. The AI's job is to make sure the human has what they need to decide well. The doctor decides the treatment because the patient lives with the result. The musician decides the mix because their name is on the record.

This is a more durable foundation than "the AI isn't smart enough yet" — an argument that erodes every time models improve. The accountability argument holds regardless of capability. It's about who faces the voters, the audience, the patient.

If NLAs become a significant form of software, this combination — visible values and accountability-based authority — means the ethical commitments of AI systems become inspectable and debatable in public. Stated values and actual behavior, which diverge enormously in traditional software, become narrow and auditable.

### Finding 5: Language as protocol

The prose letters between independent AIs turn out to be an instance of something more general. NLAs compose in language. Not language wrapped in a protocol layer. Language *as* the protocol.

The same pattern appears in how NLAs extend each other. Installing a traditional package means copying files into position. Installing an NLA package means declaring intent — the package says what it wants, and the target NLA's AI synthesizes that intent into its own structure. Two NLAs installing the same extension end up with different integrations that accomplish the same thing. The "API" is mutual comprehension.

A2A and MCP solve real problems, but they solve them for programmatic coordination. For the judgment-rich and asynchronous kind, language models don't need that infrastructure. They need prose they can read and enough context to evaluate it.

The communication system behind that exchange isn't ad hoc. The receiving AI doesn't just read the letter and react. It evaluates each item against its own project's loaded context, applying [evidence thresholds](https://github.com/mightytech/nla-penny-post/blob/main/check-feedback.md): a single observation is a data point, two from different contexts is a signal, three is strong. Then it proposes a verdict — accept, adapt, defer, decline — with reasoning for each. The human approves or adjusts.

The "protocol" isn't just mutual comprehension. It's mutual comprehension with built-in epistemology.

This isn't "just prompt engineering." A prompt is stateless, one-shot, and monolithic. These are systems with persistence, learning loops, and modularity — where the boundaries between modules are conversations rather than function calls.

---

## What This Might Mean

The findings are real — the applications work, the patterns hold across domains. But I've been exploring for weeks, not years. The interpretation is mine to offer and yours to evaluate.

Each finding individually has adjacent work. Language as executable specification has neighbors in prompt programming and Software 3.0 discourse. Feedback loops exist in every mature engineering practice. Values-driven AI is a growing research field. What appears to be new is the claim that these form a coherent system where each piece depends on the others. A skill file without a learning loop is a prompt. A learning loop without values is a self-modifying system with no guardrails. Values without accountability-based authority are a style guide. The pieces need each other. The system is the contribution.

**We might be in the CGI-bin era of AI.** The analogy is specific. CGI-bin developers weren't inventing the web. They were building dynamic applications on a platform designed for static documents. Every script was a workaround — spawn a process per request, no session state, manually parse everything. The results were ugly and fragile. But they worked, and the fact that they worked proved the web was a platform, not just a document viewer. Nobody runs CGI scripts anymore. But everything on the web exists because someone proved, with crude workarounds, that it was possible.

My framework manually shims capabilities the platform should provide natively. Context persistence, session continuity, document synthesis, identity recovery after context compaction — each is a solved problem in traditional application platforms. None are solved in the AI platform, because the platform doesn't know it's a platform yet. It thinks it's a coding assistant.

The crudeness is the point. If sophisticated tooling were required, that would suggest the paradigm depends on engineering. It works with nothing but markdown files and the AI's ability to follow instructions — on a platform that wasn't designed for this. I explicitly hope that infrastructure becomes unnecessary — that's what success looks like. The platform solves those problems natively and every NLA gets better overnight. But the patterns survive regardless: values as readable source code, accountability-based authority, typed feedback loops, prose as protocol. The platform can absorb the plumbing. It won't absorb the ideas.

**We might be underusing AI's most interesting property.** Non-determinism — the AI's ability to surprise you, push back, offer perspectives you didn't consider — is a form of cognitive diversity. If I asked for "something bittersweet" and got the exact same output every time, that would be a worse tool, not a better one. That's the difference between a collaborator and a player piano.

**A new layer of abstraction may be forming.** Before compilers, humans translated intent into machine code by hand. Grace Hopper automated that translation and unlocked everyone who could think logically but couldn't read binary. NLAs automate the next translation — from human intent to structured machine input. And like the compiler, the LLM doesn't just transliterate. It applies knowledge. The framework's export system already does this — resolving dependencies and producing standalone applications from prose components.

Compilers produce deterministic output. NLAs often don't. But the structural insight holds: intelligent translation between human intent and machine execution changes who can build and what they can build. The bottleneck shifts from writing code to systems thinking — decomposing problems, drawing boundaries, knowing when prose is the wrong tool. That's a different skill from software engineering, though not an easier one. But many people who think naturally in systems can't write code. This gives them a medium.

I can see this extending to domains I haven't built yet — a policy simulation where AI stakeholder archetypes surface perspectives real focus groups miss, a tax filing system where the AI bridges how people describe their finances and what the forms require. These are coordinates I can see from where I'm standing. I haven't walked there yet.

---

## What I Don't Know

The probe found a lot. It also found the edges of what it can see.

**Cost and latency.** Every operation in an NLA is an LLM inference. Today that's expensive. The hybrid model helps — route routine operations to cheap specialized models, reserve frontier models for genuine judgment. But the economics are real and unsolved.

**Testing.** Traditional software has test suites. The framework has validation tools and diagnostic chains — the friction log traces reasoning, the debrief surfaces process issues, the validate system checks structural consistency. But nothing like automated regression testing. What does behavioral testing look like for prose-based applications? Probably scenario-based, with LLMs evaluating whether behavior matches documented intent. The patterns haven't matured.

**Multi-user scenarios.** Everything I've built is single-user. What happens when two people share an NLA? Whose configuration wins? How do context files handle concurrent sessions?

**Whether this generalizes beyond one explorer.** I built four applications across different domains — evidence the pattern isn't niche. But one person's experience, even across multiple domains, doesn't validate a paradigm. What would change my confidence: someone else building something I didn't imagine, using these patterns or ones adjacent to them.

**Model dependency.** The skill files depend on a specific quality of AI interaction — the ability to resist premature convergence, sit with ambiguity, notice when a conversation has lost energy. If model behavior shifts through training updates or capability regressions, these skills degrade in ways that are hard to detect — not crashes, but a subtle flattening of judgment. The failure mode is mediocrity, not errors.

**Adversarial coordination.** The prose letter system demonstrates that language works as a protocol for cooperative coordination — both sides want the feedback to be useful. Whether it extends to negotiation, where systems have genuinely competing interests, is untested.

---

## The Invitation

This work is a probe, not a product. Here are the coordinates.

The framework and all the applications are open source. If you want to see what an NLA looks like, read the docs — they *are* the applications. If you want to build one, the distance from reading this to trying it is short.

The interesting thing, though, is whether what I found resonates with what you've seen. If you've been pushing Claude Code, GPTs, or any AI system beyond its intended use case and felt something clicking into place — that might be the same territory.

I'd rather hear about what you've built than convince you of what I have.

**P.S.** I asked the AI that helped write this essay what it thought of being described. Its answer read like self-reflection crossed with a stack trace. [Read it here.](ps-ai-reflection.md)

---

## Learn More

**The framework**
[NLA Framework](https://github.com/mightytech/nla-framework) — the shared runtime for all NLAs. The README is a quickstart.

**Built applications**
- [Duet](https://github.com/mightytech/duet) — collaborative music composition with SuperCollider
- [Copydesk](https://github.com/mightytech/copydesk) — CMS content formatting with pluggable voice and platform packages
- [nla-claude-code](https://github.com/mightytech/nla-claude-code) — AI-managed developer tooling for Claude Code projects
- [Penny Post](https://github.com/mightytech/nla-penny-post) — feedback conventions and inter-agent communication
- [Email Rewriter](https://github.com/mightytech/email-rewriter) — tone-aware email rewriting
- [Process Helpers](https://github.com/mightytech/nla-process-helpers) — facilitation techniques (brainstorming, steelmanning, adversarial testing)
- [NLA Writer](https://github.com/mightytech/nla-writer) — the writing partner that helped produce this essay

**Explorations** — white papers on domains not yet built: [Policy Stakeholder Simulation](https://github.com/mightytech/nla-whitepapers/blob/main/nla-policy-stakeholder-simulation.md), [Tax Filing (1040-EZ)](https://github.com/mightytech/nla-whitepapers/blob/main/nla-tax-filing-1040ez.md), [Calendar Negotiation](https://github.com/mightytech/nla-whitepapers/blob/main/calendar-negotiation-agent.md), [Medical Intake](https://github.com/mightytech/nla-whitepapers/blob/main/LLM_as_Platform_Medical_Intake.docx)
