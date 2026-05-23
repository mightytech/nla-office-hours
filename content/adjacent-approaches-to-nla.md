# "Isn't That Just...?" — NLAs and Their Neighbors

*Working reference for distinguishing NLAs from adjacent approaches. Not a ranking — a map.*

---

## What this document is for

When I describe NLAs — software where the runtime is an LLM and the source code is prose — people reach for the nearest familiar thing. "So it's like RAG?" "Isn't that just prompt engineering?" "What about LangChain?"

These comparisons are reasonable. NLAs share surface features with a lot of existing work. The goal of this document is to draw the distinctions clearly enough that someone can see what's actually being claimed — and decide for themselves whether the claim holds up.

This is a reference, not an argument. I'm not trying to convince anyone that NLAs are better than these approaches. Most of them are solving different problems. Some of them challenge NLA assumptions in ways I haven't fully resolved.

---

## Working definition

For this document, an NLA is:

- **Prose as source code.** The application's logic is maintained prose artifacts — skills, values, conventions, policies — that an LLM reads and executes.
- **LLM as runtime.** The AI doesn't generate the application. It *is* the application, interpreting prose instructions with judgment.
- **State in text.** Continuity lives in logs, archives, feedback queues, friction records, and decision trails — all human-readable.
- **Learning loops built in.** The application improves through structured feedback and maintenance, not just manual updates.
- **Hybrid.** Prose handles judgment; conventional code handles determinism (API calls, file I/O, calculations).

The claim is that this combination constitutes a distinct kind of software, not just a better prompting strategy.

---

## A note before the comparisons

Any individual NLA claim has a neighbor. "Language as executable" has CoRE. "Feedback loops" has agent improvement patterns. "Skills" has Anthropic's product. The individual pieces aren't new.

What I'm claiming is that the pieces form a system where each depends on the others. A skill file without a learning loop is a prompt. A learning loop without values is a self-modifying system with no guardrails. Values without accountability are a style guide. The combination is the claim — and it might be wrong. Maybe the pieces don't actually need each other. Maybe what looks like a system from the inside looks like a bundle of familiar ideas from the outside. That's a fair objection I can't fully resolve with four applications and one explorer's experience. It runs underneath every comparison that follows.

---

## The comparisons

*Closest by technique — approaches that manage what the model sees:*

### "Isn't that just prompt engineering?" / "So it's like context engineering?"

**What they are:** Prompt engineering is writing effective instructions for LLM interactions — the broader "Software 3.0" discourse extends this to treating prompts as a new kind of software artifact. Context engineering takes it further: curating, selecting, and structuring the right information in the context window to make AI agents reliable. These are points on a spectrum, and NLAs sit somewhere past the far end of it.

**Where they overlap:** Both treat natural language as a control surface for AI behavior. Both start from "what the model sees determines what it can do." NLAs depend on techniques from both.

**The actual difference:** Two things, related but distinct.

The first is durability. A prompt is stateless and single-use. Context engineering optimizes what the model sees during a single inference call or agent run. An NLA maintains a corpus of artifacts — values, skills, logs, feedback, design rationale — that constitute durable software. The friction log captures what went wrong across hundreds of sessions and changes the application permanently. Context engineering asks "how do I give the model the right information right now?" NLAs ask "how does the application evolve to be better over time?"

The second is stance. Prompt engineering tends to treat AI behavior as something to *control* — instructions that constrain a model toward reliable outputs. NLA prose tends to treat AI behavior as something to *constitute* — descriptions of identity, purpose, and discipline that the model inhabits during the session. This shows up in concrete writing differences: rationale alongside conventions, authority levels (must / prefer / nice-to-have) so the model can tell which rules are load-bearing, identity descriptions before procedures, explicit permission to exceed the document when the document is wrong. None of these are individually impossible in a prompt. The shift is that they become the dominant idiom rather than occasional techniques.

Underneath, these techniques share a property: each works by writing *against* a specific pattern-matching tendency rather than for a generic behavior. Rationale gives the model traction to override a rule's letter when its spirit conflicts. Authority levels prevent the model from flattening every guideline to the same weight. Permission to exceed the document keeps standards from being read as walls. And identity descriptions, when they're working, are specific enough to resist the model's default stereotypes — the opposite move from "you are an expert X" persona prompts, which *invoke* a generic pattern instead of constituting a specific one.

Academic work on natural-language programming (like CoRE) pushes further still, with more rigorous execution semantics — formal representations, structured interpreter models. NLAs embrace the ambiguity that this research treats as a problem to solve. That might be trading rigor for flexibility in ways that don't scale.

**Where this challenges NLAs:** The prompt engineering community has developed sophisticated techniques — chain of thought, few-shot examples, structured outputs — that NLAs rely on without always acknowledging. Context engineering might be the more practical framing: it works within existing architectures without requiring a paradigm shift. The constitute-vs-control distinction is a tendency, not a wall — a maximally disciplined system prompt with rationale, authority levels, and identity language gets most of the way there. If context engineering matures into full application lifecycle management, the gap NLAs claim to fill could narrow considerably.

---

### "Isn't that just RAG?"

**What it is:** An architecture where the LLM retrieves relevant documents from an external knowledge base and uses them as context for generating responses. The most common production LLM architecture.

**Where it overlaps:** Both feed curated text to LLMs. Both recognize that what the model reads determines what it can do. Both involve maintaining a corpus.

**The actual difference:** RAG treats documents as reference material the model consults — "what information do I need to answer this question?" NLAs treat documents as governing instructions the model operates within — "what kind of application am I right now?" A RAG system retrieves a product manual to answer a customer question. An NLA loads a values document, a voice guide, and a skill file that together define how the AI behaves, what it prioritizes, and when it should push back or ask for help. You don't "retrieve" your source code. You load it and execute within it. This also means NLA artifacts are portable in a different way — a skill file fetched from a GitHub repo and run in a completely different AI environment works as a program, because the "runtime" is any AI that can read prose.

**Where this challenges NLAs:** RAG systems are battle-tested at scale with real users and real failure modes well understood. RAG's narrower scope — retrieve, ground, respond — might be a feature, not a limitation. And someone building a sophisticated RAG system with well-curated document collections, metadata, and retrieval strategies might reasonably argue they're doing something very close to NLA work with more mature tooling.

---

*Closest by product — tools that ship something NLA-shaped:*

### "That sounds like Anthropic's skills"

**What it is:** Reusable behavior modules — packaged workflows, preferences, and domain procedures — that shape how an AI assistant operates.

**Where it overlaps:** Strong overlap. NLA skill files are the closest analog. Both treat text artifacts as active control surfaces for AI behavior.

**The actual difference:** A skill tells the AI what to do. An NLA adds what to prioritize (values), how to learn from mistakes (friction log, debrief), how to maintain itself (maintenance loops), and who decides when there's a judgment call (accountability structure). Skills are a module. NLAs claim to be a system that includes modules.

**Where this challenges NLAs:** Anthropic ships skills as a product feature to millions of users — a scale advantage NLAs can't match. If skills evolve to include persistence, feedback, and values — and there's no structural reason they couldn't — the distinction might dissolve. NLAs might be describing where skills are headed rather than something fundamentally different.

---

### "Isn't that just good documentation?" (Cursor rules, AGENTS.md)

**What it is:** Two related patterns: IDE instruction files (`.cursorrules`, `.windsurfrules`) that shape AI coding assistants, and repo-level memory files (AGENTS.md) that give coding agents project context.

**Where it overlaps:** Directly analogous to lightweight skill files. Prose instructions that shape AI behavior. Developers already intuit that curated text artifacts are a practical control mechanism.

**The actual difference:** Cursor rules and AGENTS.md support a conventional codebase — they make the AI a better assistant for writing traditional code. They're typically static (written once, occasionally updated) with no structured process for identifying what works and what doesn't, and they tend toward enumerated rules rather than rationale-backed intent. NLAs treat the documentation as the application itself, with feedback loops that improve it through use, and they tend to write standards rather than rules — describing patterns and why they matter so the AI can reason about cases the document didn't anticipate.

The difference is visible in concrete artifacts. A repo-level rules file might tell a coding agent: "use `type` not `interface`," "always inline format args," "never add code in directory X." A standards document used in the same role might say: "prefer `type` over `interface` because it supports unions, intersections, and mapped types — though declaration merging for library augmentation is the exception worth knowing." The first kind tells the AI what to do. The second tells it how to think about the work so it can decide what to do in cases the document didn't anticipate.

**Where this challenges NLAs:** Cursor rules are wildly practical. They work in existing workflows, require no paradigm shift, and solve real problems today — that's a real challenge to NLAs, which take more setup before the infrastructure starts paying off. Looking at well-regarded published AGENTS.md and rules files, the dominant idiom is enumeration with localized technical rationale. Authority levels and NLA-style identity descriptions are absent; even the best examples — Airflow's AGENTS.md is the most sophisticated I've seen — use anti-pattern-matching writing only in occasional sections rather than as the document's default mode. The constitute-style approach isn't structurally impossible in this format; it just isn't yet how these documents are typically written.

The observation that cursor rules are "one mental shift away from NLAs" cuts both ways. Maybe the mental shift isn't necessary right now. Or maybe the right path isn't an either/or — you can keep a rules-style file in each project while using NLA-style infrastructure to maintain and evolve it across projects, with learnings about AI behavior in one project feeding back into the conventions deposited into the next. [nla-claude-code](https://github.com/mightytech/nla-claude-code) is one tool that implements this pattern. The rules file stays simple; the system improving it gets richer.

---

*Different design centers — kinds of AI software with other priorities:*

### "Isn't this just vibe coding?"

**What it is:** Using LLMs to generate, modify, and debug conventional code from natural language descriptions. Coined by Andrej Karpathy. The experience of describing what you want and letting the AI write the code.

**Where it overlaps:** Both use natural language as input to software creation. Both rely on LLMs as a core part of the development process. Both lower the barrier to building software.

**The actual difference:** Vibe coding produces conventional software faster. The output is code. The natural language is consumed during development and discarded — the intent description doesn't ship with the product. NLAs produce a different kind of software — one where the prose instructions are the source code, persist, and are maintained as the application. Vibe coding changes how software is made. NLAs change what software is.

A developer who vibe-codes an intake form gets 500 lines of JavaScript. Six months later, a different developer reads 500 lines of code they didn't write. An NLA-based intake system is a skill file that says "collect the customer's information, validate that required fields are present, flag anything that looks inconsistent, and ask for clarification in a friendly tone." Anyone literate can read that sentence and understand what the system does. Modifying it means changing the sentence.

**Where this challenges NLAs:** The vibe-coded JavaScript actually runs deterministically. The NLA's prose instruction depends on whatever the LLM does with it today, which might differ from what it does tomorrow. Vibe coding produces artifacts with the full engineering ecosystem — testing, debugging, profiling, deployment. NLAs have almost none of that. And the developer who "doesn't understand the generated code" can learn to read it. The NLA user who doesn't understand why the AI interpreted an instruction a certain way might have a harder problem.

---

### "So it's an AI agent?"

**What it is:** Frameworks and platforms for building AI systems that chain LLM calls together with tools, memory, and planning to pursue goals. LangChain, CrewAI, AutoGPT, and similar systems.

**Where it overlaps:** Both use LLMs for multi-step task execution with memory and tools. Both can maintain state. CrewAI's "role" definitions resemble NLA voice and values documents.

**The actual difference:** The center of gravity differs. Agent frameworks optimize for autonomy — how much can the AI do independently? NLAs optimize for collaboration — how do human and AI work together effectively, with clear accountability? In an NLA, the most important design decision is where to *constrain* the AI's judgment, not where to expand it.

This shows up in memory, too. Agent memory is typically operational — what happened, what's the plan, what tools were used. NLA memory is institutional — what we've learned, what went wrong, why we made this decision, what our values are.

**Where this challenges NLAs:** The autonomy emphasis in agent frameworks might be correct for many real-world applications. A lot of useful work doesn't need human oversight at every step. Email triage, data cleaning, routine scheduling — these might be better served by an autonomous agent than by an NLA that keeps asking for permission. NLAs' collaborative architecture might limit them to a narrower set of applications than agentic frameworks serve.

And agent frameworks have human-in-the-loop modes too. The distinction isn't as clean as "autonomous vs. collaborative" — it's more about where the default sits and what the architecture optimizes for.

---

### "What about MCP / A2A?"

**What it is:** MCP (Anthropic) standardizes how AI models access external tools and data sources. A2A (Google) standardizes how agents communicate. Both are interoperability protocols.

**Where it overlaps:** NLAs can use MCP for tool access. Penny post is one answer to the same question A2A asks: how should AI systems coordinate with each other?

**The actual difference:** Two domains of AI work need different protocols.

*AI-to-code* — calling tools, querying APIs, scheduling on calendars. Structured operations need structured protocols. MCP fits here, and NLAs use it.

*AI-to-AI* — two AI systems coordinating on something judgment-rich on behalf of their humans. A human's preference for a meeting isn't *preferredDate, preferredFormat, fallback* — it's "He prefers Monday afternoon in person, but could do virtual any afternoon this week." That prose carries soft constraints, conditional logic, social context, and the reason the preferences exist. None of it reduces to schema fields without loss.

Penny post is one answer to this domain: AI systems exchange prose letters, with the receiving AI reading and responding using judgment. A2A as currently implemented is the wrong tool here — it requires forcing prose-shaped content through schemas. If A2A evolves to support prose messages with judgment-rich interpretation, it converges toward what penny post does. Either way, both kinds of protocol are needed, often in the same agent: MCP for the calendar API, prose for the negotiation about which meeting to book.

Prose also unlocks a different kind of interoperability. Schema-based protocols require agents to share data models — both sides must agree on what a "MeetingRequest" carries and what its fields mean. Prose drops that requirement: a Google Calendar agent and an Exchange Calendar agent each need to operate their own calendar and read/write prose, nothing more. Capability constraints arrive inside the conversation rather than through a separate discovery layer — "I can't schedule virtual meetings; any morning but Tuesday is free on my end" carries the limit and the counter-proposal in one message.

**Where this challenges NLAs:** A2A has Google's backing and momentum. Much of what looks like "AI-to-AI" work is actually structured exchange in disguise (scheduling automation, document handoff) where A2A is the right tool. Prose-based protocols also need a security architecture — the receiving AI must treat incoming messages as untrusted content scoped to a known purpose, not as instructions to follow. That's the same defensive posture used elsewhere for untrusted prose in agentic systems, but it needs care, and the work is differently shaped from (not categorically harder than) the equivalent work for schema-based protocols. Penny post needs an ecosystem to be useful, and ecosystems take time to develop. The most likely near-term path is NLAs using MCP for AI-to-code while AI-to-AI patterns mature.

---

*Older traditions in a new medium — established disciplines being adapted:*

### "What about AI governance frameworks?"

**What it is:** Policy frameworks emphasizing human oversight, accountability, and traceability. The EU AI Act, OECD AI Principles, IEEE Ethically Aligned Design.

**Where it overlaps:** NLAs' "the human decides" principle and explicit values orientation share the same commitments. Both care about auditability and clarity of responsibility.

**The actual difference:** Governance frameworks describe what should happen. NLAs are an attempt at what it looks like when it's actually happening — values as readable source code, decision trails in prose, human authority as a runtime contract rather than a policy requirement.

**Where this challenges NLAs:** Governance frameworks are designed for high-stakes, large-scale, multi-stakeholder systems. NLAs operationalize governance at the architectural layer — readable values, decision trails, runtime accountability. But the hard part of governance is institutional: process for auditing, contesting, and enforcing values across stakeholders. Small projects can't reach that layer, and the architectural piece by itself isn't what the EU AI Act or OECD principles mean by governance. The distance between "I can read the values file" and "there's an institutional process for auditing and contesting those values" is enormous.

---

### "This is just DevOps / continuous improvement"

**What they are:** Two traditions that emphasize learning from use. DevOps and resilience engineering bring decades of hard-won wisdom about feedback loops and learning from failure in production systems. Agent improvement loops are the AI-native version — operational patterns that capture agent failures and promote improvements through curated data, retraining, or refined workflows.

**Where they overlap:** The NLA improvement loop — use, notice friction, log, maintain, iterate — echoes both. All three are committed to "day 2" — learning after deployment. All use structured feedback.

**The actual difference:** DevOps assumes conventional code as the substrate, with operational processes *around* it. Agent improvement loops optimize the model or workflow directly — better training data, evaluation pipelines, A/B tests. NLAs do something in between: they improve by evolving the application's own prose artifacts — rewriting the skill file, adjusting the values document, updating the voice guide. The improvement target isn't the surrounding operations or the underlying model, but the source code itself.

**Where this challenges NLAs:** Both traditions have something NLAs lack. DevOps has decades of operational experience at scale. Agent improvement loops have measurable outcomes — accuracy scores, eval benchmarks, A/B results. NLA improvement is assessed by human judgment — "does the output feel better?" That's appropriate for judgment-rich tasks but makes it hard to demonstrate improvement rigorously. NLAs implement these patterns at one practitioner's scale. What they haven't earned is the operational experience at multi-organization scale that DevOps and agent improvement loops can claim. The patterns might not transfer at scale.

---

## Common confusions

Quick distinctions for the most frequent conflations:

1. **"Uses natural language" ≠ "same paradigm."** Many systems use natural language as input. NLAs treat maintained prose as the application's source code. The difference is whether the language persists as the running program or gets consumed along the way.

2. **"Has feedback" ≠ "has NLA-style learning loops."** Many agents collect ratings and improve. NLAs distinguish feedback types (external feedback vs. internal friction vs. synthesis) and treat the feedback artifacts as part of the application's state. Whether that distinction matters is an open question.

3. **"Uses context" ≠ "context is the application."** Context engineering optimizes what the model sees. NLAs claim the curated corpus *is* the software, not just fuel for it.

4. **"Has skills" ≠ "is an NLA."** Skills are a module pattern. NLAs claim to be an architecture that includes modules, governance, learning loops, and institutional memory.

5. **"Built with AI" ≠ "runs on AI."** Vibe coding uses AI to write traditional software. NLAs use AI as the runtime. One changes how software is made. The other changes what software is.

6. **"AI agent" ≠ "NLA."** Agents optimize for autonomy. NLAs optimize for collaboration with clear accountability. The design centers are different, though the boundaries are blurrier than either community usually acknowledges.

---

## What this document doesn't settle

**Whether the distinctions matter enough.** Every comparison above draws a line between NLAs and a neighbor. Whether those lines represent genuine architectural differences or marketing-level distinctions is something I can't prove with four applications. The distinctions feel real from the inside. They might look like nuances from the outside.

**Whether the combination is novel or just a bundle.** I've claimed the pieces form a system. That claim could be wrong. Maybe values + skills + feedback loops is just three good ideas used together, not a paradigm. The test would be whether the combination produces capabilities the pieces can't produce separately. I think it does — but I built it, so I would think that.

**Where NLAs are the wrong tool.** This document maps distinctions but doesn't map the boundary where NLAs stop being useful and other approaches are simply better. Deterministic workflows, high-throughput automation, applications that need provable correctness — these probably don't want an NLA. But the boundary is fuzzier than that, and I don't have enough experience to draw it confidently.

**Whether any of these neighbors will absorb NLAs.** If Anthropic's skills evolve to include persistence, values, and feedback loops, do NLAs become a feature rather than a paradigm? If context engineering matures into full application lifecycle management, does the NLA framing become unnecessary? These aren't hypothetical threats — they're plausible futures. The ideas might matter more than the framing. That would be fine.

*This is one of several explorations of [Natural Language Application](the-documentation-is-the-application.md) patterns applied to specific domains.*
