# Executable Governance: What Happens When AI Can Follow Its Own Rules

Here is a file called `values.md`:

> **Report from the frontier, don't sell from the stage.** This work is a probe — a Voyager-style exploration that hopes to be superseded by native platform capabilities. The posture is "here's what we found" not "here's why you should care." Invite curiosity and exploration. Don't pitch, don't advocate, don't optimize for the wow reaction. If the honest version is less compelling than the polished version, go with honest. Credibility compounds; hype doesn't.

The AI that helped write this essay read that paragraph before we started. Not as background material. As an instruction it follows. When I draft something that leans too far toward advocacy, it flags the tension — "your values doc says 'report, don't sell' and this paragraph is selling." Not a veto. A question. I decide.

That file is one of several that govern the AI's behavior in this project. They're written in plain English. The AI reads them at startup. They shape every interaction — not because the AI has been trained on them, but because they're operative instructions in the application the AI is running.

I've been building software where documentation *is* the application — where the "source code" is prose and the runtime is an AI that reads it and does what it says. A [companion essay](the-documentation-is-the-application.md) describes the technical findings — what happens when prose becomes software. This essay is a different instrument pointed at the same system. It asks: what does it look like when governance is written in a medium that can actually execute it?

Prose has always been the medium of governance. Constitutions, regulations, codes of conduct, employee handbooks — all prose. But prose governance has always depended on human interpreters who may not read it, may misunderstand it, may ignore it. The documents are aspirational. The behavior is whatever actually happens.

What changes when the executor can actually read?

---

## The Technical Minimum

A brief grounding for readers arriving from outside software. The [companion essay](the-documentation-is-the-application.md) has the full technical picture.

In a Natural Language Application, the "source code" is prose and the "runtime" is an AI that reads it. Change a sentence, change how the system behaves. Add a document, add a feature. The prose isn't reference material the AI retrieves when asked — it's the governing document the AI operates within. The documentation is the application.

This works because the AI can exercise judgment. "Use blockquotes to visually emphasize powerful quotes — one or two per article is usually enough" is an instruction a human editor would follow and a traditional program couldn't parse. The AI handles it the way the editor would — by understanding *why* and applying that understanding to specific cases.

Where this breaks down is also clear. The AI is non-deterministic — the same input may produce different output. It can hallucinate. Judgment is not always correct. The system I'll describe is designed for these properties, not despite them.

---

## What the Probe Found

### Finding 1: Values become executable

Every AI system has values. Most can't show you theirs.

A recommendation algorithm that maximizes engagement has embedded a value: engagement over everything. A hiring system trained on historical data has embedded every bias in that history. These values are real, consequential, and invisible — distributed across training data, model weights, and code that nobody reads as a values statement.

An AI application with no explicit values has the same problem. It inherits whatever the model's training produced — unexamined defaults that reflect the aggregate of its training data. There is no neutral default. Choosing not to state values is itself a values choice: to accept whatever the model brings without inspection.

In the system I built, values are a [document](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) the AI reads and follows:

> All priorities are value choices, varying in stakes but not in category. "Keep it concise" and "never misrepresent sources" are both values; the difference is consequence, not kind. Some carry legal weight. Some are aesthetic. Same infrastructure.

> Traditional code embeds the same choices invisibly — in scoring functions, filter criteria, if/else branches. An NLA states them in prose: readable, debatable, modifiable by anyone who can read.

This flattens the hierarchy between stylistic and ethical choices. They're all values. The mechanism is the same — prose instructions the AI reads and follows. The difference is stakes, not kind.

What makes this operative rather than aspirational is a pattern the framework calls "soft contradiction flagging." Before making changes, the AI checks proposals against the stated values. If a proposal creates tension — prioritizing speed over the thoroughness the values document calls for, say — the AI surfaces it explicitly: "This would prioritize X over Y. Your values doc says Y comes first. Are you sure?" Not a veto. A question. The human decides.

The values are also fractal. The framework has a values document. Each application built on it has its own, tailored to its context. A [feedback processing system](https://github.com/mightytech/nla-penny-post/blob/main/app/shared/values.md) values diagnostic richness and rationale over verdict. A [public Q&A system](https://github.com/mightytech/nla-office-hours) values matching confidence to evidence and treating skepticism as worth engaging. The commitments are recognizable across all of them — honesty, human authority, generosity — but expressed differently at each scope. Same shape at every scale, adapted to each context.

These aren't only ethical constraints. A values document that says "match confidence to evidence" produces more trustworthy analysis — not because it prevents bad analysis, but because it gives the AI a standard to reason toward. "Clarity over cleverness" produces better writing. The governed system doesn't just behave better. It performs better. Governance, in this medium, isn't overhead. It's an input to quality.

But a values document alone is aspirational — what makes it institutional is infrastructure that processes challenges to those values. The system includes a [participation mechanism](https://github.com/mightytech/nla-framework/blob/main/CONTRIBUTING.md) where anyone can submit feedback — observations and reasoning rather than proposed edits, because in a system where prose is the application, changing a sentence changes how the AI thinks and behaves. Feedback is evaluated in the receiving project's own session, where the AI has full context. Every verdict — including rejections — gets visible reasoning. [Eleven feedback items from six submissions](https://github.com/mightytech/nla-framework/blob/main/reference/feedback-log-archive.md) have been processed through this pipeline.

A governance researcher's first question about any participation mechanism: does it actually function, or is it a suggestion box nobody opens? The AI is what makes it function. It reads every submission, evaluates each against the project's full context, proposes verdicts with reasoning. The human reviews and decides — but doesn't start from scratch. The cognitive load shifts from "process everything" to "review proposed assessments." The reasoning is the product, not the verdict — a rejection with visible reasoning is more useful than an acceptance with none.

The values also propagate beyond their origin. One application in the ecosystem — [nla-claude-code](https://github.com/mightytech/nla-claude-code) — deposits governance patterns into traditional software projects. Friction logs, convention documents that explain their reasoning, lightweight observation tools. The developers who use these don't need to know about the NLA framework. The governance patterns are useful on their own — institutional diffusion through practical utility rather than mandate.

A governance researcher would recognize the mechanisms: constitutional principles producing different legislation in different jurisdictions, participation infrastructure that processes dissent, institutional patterns propagating through adoption rather than authority. The difference is that the executor — the AI — actually reads the constitution before acting.

### Finding 2: A learning loop that actually loops

The system is designed to be wrong.

Not carelessly wrong — architecturally wrong. The framework's first principle is "[Imperfection Is Assumed](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md)":

> NLAs are never finished. The documentation will have gaps, the voice will drift, the edge cases will surprise. This isn't a failure state — it's the expected state.

The entire architecture assumes ongoing imperfection and builds the correction mechanism in from day one. The capacity to improve matters more than getting it right initially.

The primary correction mechanism is a structured learning journal — the [friction log](https://github.com/mightytech/nla-framework/blob/main/core/skills/friction-log.md). When something goes wrong, the AI was there. It read the instructions, applied judgment, and can trace its own reasoning — including reasoning that led to *not* doing something. The log requires exact quotes from the governing documents, not paraphrases, to guard against a known failure mode: the AI constructing plausible-sounding explanations that are actually wrong. "A fabricated quote is worse than no quote."

The learning loop has teeth. Four of the framework's current capabilities — a [design exploration mode](https://github.com/mightytech/nla-framework/blob/main/core/skills/think.md), a [reflection skill](https://github.com/mightytech/nla-framework/blob/main/core/skills/debrief.md), a [conversation structuring tool](https://github.com/mightytech/nla-process-helpers/blob/main/app/unpack.md), and a [session close process](https://github.com/mightytech/nla-framework/blob/main/core/skills/close.md) — emerged directly from friction observations. The design exploration mode was born when the existing planning tool kept pushing toward decisions and action; the actual thinking happened by working *around* the tool. The friction was logged. The observation became a capability. The system's governance literally improved through use.

The loop also catches its own failures. During a design session, the AI misinterpreted one of its own governance instructions — using a prompt designed to invite the AI's perspective as a handoff back to the human instead. The friction log caught the misinterpretation. The documentation was reworded. The next session operated correctly. In a more consequential case, a sub-agent proposed editing files in other projects during an implementation session — contradicting a design principle established earlier that each project adopts changes through its own update channel. The root cause was diagnosed: the sub-agent had received decisions but not the *reasoning* behind them. A pre-implementation review step was added.

The correction doesn't only come from the friction log. A [reflection skill](https://github.com/mightytech/nla-framework/blob/main/core/skills/debrief.md) runs after substantive work — the AI reflects on two dimensions: whether the instructions worked (ambiguities? gaps? places it had to guess?) and how the collaboration went (did the human hesitate? did their responses get shorter? too many confirmation steps?). The framework borrows the term "participant-observer" from anthropology — the AI both participates in the work and observes the dynamics of the interaction, including aspects of the human's experience the human might not articulate. In one session, it caught that it had skipped a design exploration phase and jumped straight to implementation — the skip had produced the session's only error. The fix was implemented before the session ended. In another, the AI noticed the human's responses getting shorter. It checked whether this indicated fatigue. Turned out the human was cooking dinner. No change needed — but the noticing was valued.

The system doesn't just fix what breaks. It captures what works. The friction log includes positive observations — sessions where everything ran smoothly — preserved as baselines. "If future work hits friction, this session provides a comparison point for what smooth looks like." You need both successful and unsuccessful cases to understand what's driving results.

And the system remembers what it hasn't figured out yet. Open questions stay visible with explicit reasoning about why they're unresolved. Deferred items include the rationale for deferral. A [design rationale](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) records every architectural decision — what was decided, why, what alternatives were considered and rejected, what components are affected. Most institutional knowledge preserves decisions but loses the reasoning. This preserves the full deliberative process, so a future maintainer can evaluate not just whether a decision was right, but whether the reasoning was sound, and whether circumstances have changed enough to revisit it. The opposite of institutional amnesia.

Thirty-three maintenance sessions over four weeks. The full trail — observations, decisions, implementations, validations, reflections — is preserved in prose any future maintainer can read.

### Finding 3: Governance works differently when the executor has judgment

Traditional governance assumes tighter specification produces better compliance. When the executor can reason about intent, the opposite is often true.

The clearest example came from a project called [Duet](https://github.com/mightytech/duet) — a music composition tool, architecturally different from the content formatting tool the framework was originally designed around. Duet sent eleven items of feedback exposing where the framework's governance language assumed all applications were content transformers. The fix wasn't adding special cases. It was broadening existing language.

The framework's cardinal rule — its core authority principle — changed from "the human must always be able to compare changes against the original" to "the human decides." Broader, but better. The narrow version excluded applications that create rather than transform. The broad version covers every case because the AI understands *why* human authority matters — accountability, not comparison — and applies that understanding to contexts the original wording couldn't anticipate.

In practice, the cardinal rule does more than preserve authority. The checkpoints it creates maintain the human's competence to exercise that authority. Even routine approvals transfer context — the human absorbs how the system works, what it considered, how pieces connect. When a consequential decision arrives, the human has the situational awareness to make it well. Like the values that improve the AI's output, the authority mechanism improves the human's judgment. Governance isn't overhead for either participant.

The principle extracted: when the AI behaves too narrowly, loosen the language rather than adding more rules. This is the opposite of traditional programming, where tighter specifications produce more reliable systems. In a system where the executor can reason about intent, loosening specifications creates judgment space — and the judgment is often better than the rule it replaces.

This pattern appears throughout the system. The feedback conventions specify suggested formats with published reasoning, not rigid protocols. "The reader is an AI that applies judgment, not a parser. Rigid formatting would constrain communication without improving processing. A well-written freeform letter is better than a poorly filled form." Triage verdicts — accept, adapt, defer, decline — are "convenient defaults, not an enum." The instruction "'Accept the principle, defer the implementation' is valid."

The trust in judgment extends to how the system distributes authority. A [feedback processing system](https://github.com/mightytech/nla-penny-post) went through a fundamental architectural redesign — [twenty numbered decisions](https://github.com/mightytech/nla-penny-post/blob/main/reference/sessions/2026-02-16-first-review.md), each with rationale — following from a single jurisdictional insight: evaluation requires understanding. To assess whether feedback about the framework is valid, you need to understand the framework. So evaluation happens where the context lives, not where the feedback infrastructure lives. The framework generalizes this as "[Context Determines Competence](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md)": the AI's ability to make good judgment calls is bounded by the project context it has loaded. Mechanical operations can cross project boundaries. Judgment operations cannot. The architecture doesn't just recommend this — it enforces it epistemically. The AI literally can't make good judgments without the right context.

The framework articulates the underlying design principle: governance has two tools. Principles explain *why* — they shape judgment across many situations. Procedures specify *when* — they produce specific behaviors reliably. "The principle ensures the AI does it well. The procedure ensures the AI does it at all." A governance researcher would recognize this from institutional design — the same tension between principle-based and rule-based regulation. The finding here is that principle-based governance works better *specifically because* the executor can reason about intent. Tighter rules don't just fail to help; they can actively prevent better outcomes by foreclosing judgment.

Even the installation mechanism follows this pattern. When one application extends another, the extension doesn't ship templates to copy. It ships [intent files](https://github.com/mightytech/nla-penny-post/blob/main/install/install.md) — descriptions of what the extension wants, which the receiving application's AI synthesizes into its own structure. Two applications installing the same extension end up with different integrations that accomplish the same thing. Express the intent, let judgment handle the adaptation.

When governance is prose that the executor reads and reasons about, a further consequence follows: the system can explain its own reasoning. Every project ships with inspection tools — maintenance, friction logging, validation — hidden by default but present. The framework's [design rationale](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) explains why: "Like View Source in browsers — it turns users into developers." When governance is readable prose processed by an AI that can trace its reasoning, transparency isn't an added feature. It's a property of the medium.

---

## What This Might Mean

The findings are real — the governance infrastructure works, the patterns hold across multiple applications. But I've been building for weeks, not years. The interpretation is mine to offer and yours to evaluate.

**The accountability argument may be more durable than the capability argument.** Most discussions of human oversight in AI are framed around capability — humans should oversee AI because AI isn't good enough yet. That argument erodes every time models improve. The framework takes a different position: authority follows accountability, not capability. The human decides not because the human is always right, but because the human bears the consequences. The doctor decides the treatment because the patient lives with the result. This holds regardless of how capable the AI becomes.

**The AI safety conversation may be a visibility problem.** If every AI system already has values — embedded in training data, model weights, and code — then the question isn't whether to add governance. It's whether to make existing governance visible. The act of writing a values document and having the AI read it doesn't add values to a system that had none. It makes values that were already there — inherited, unexamined — explicit, inspectable, and debatable.

---

## What I Don't Know

**Scale.** This is one developer, one ecosystem, four weeks of sustained operation. The governance mechanisms work at this scale — thirty-three sessions, eleven feedback items processed, four capabilities emerged from the learning loop. Whether they work at institutional scale — hundreds of contributors, competing interests, adversarial participants — is untested.

**Non-determinism.** The AI's judgment varies between sessions. The same friction log entry might be diagnosed differently on a different day. The system mitigates this — exact quotes as checkable evidence, human review of every judgment — but doesn't eliminate it. What governance looks like when the executor's judgment is probabilistic rather than deterministic is a genuinely open question.

**The observer effect.** The system's self-explanation may change what's being explained. An AI narrating its decisions may reason more deliberately than one working silently. The framework documents this rather than trying to eliminate it, but the implication is real: the governed version of the system may not behave exactly like the ungoverned version. Governance is not a neutral observation.

**Adversarial conditions.** The feedback system demonstrates that prose-based governance works for cooperative coordination — all participants want the system to improve. Whether it extends to genuinely adversarial conditions — where participants want to game the system, manipulate evaluations, or exploit the AI's judgment — is untested.

**Model dependency.** The governance depends on a specific quality of AI judgment — the ability to reason about values, sit with ambiguity, trace its own reasoning. If model behavior shifts through training updates, these capabilities could degrade in ways that are hard to detect. Not crashes — a subtle flattening of judgment. The failure mode is mediocrity, not errors.

---

## The Invitation

This is a probe report from adjacent territory. The [companion essay](the-documentation-is-the-application.md) describes the technical findings — what happens when documentation becomes the application. This piece asks what it means when the governance is prose and the executor can read.

I didn't set out to build a governance system. I set out to build applications where the AI follows prose instructions. The governance emerged because the medium demanded it — when changing a sentence changes behavior, you need visible values, accountability infrastructure, and learning loops. The philosophical questions weren't designed in. They were discovered.

The framework, the applications, and every governance mechanism described here are open source. The values documents are readable. The friction logs are searchable. The design rationale preserves every decision with its reasoning. If you want to evaluate the claims in this essay, the evidence is there.

What I'd most like to know is whether what I've found connects to what governance researchers already understand — whether the patterns have names I don't know, whether the mechanisms map to frameworks I haven't read, whether the limitations I've identified are the ones that matter most.

I'd rather learn from your expertise than convince you of mine.

---

## Learn More

**The framework**
[NLA Framework](https://github.com/mightytech/nla-framework) — the shared foundation. The README is a quickstart; the docs *are* the application.

**The companion essay**
[The Documentation Is the Application: Are We in the CGI-bin Era of AI?](the-documentation-is-the-application.md) — the technical probe report this piece accompanies.

**Key governance documents**
- [values.md](https://github.com/mightytech/nla-framework/blob/main/app/shared/values.md) — the framework's values document
- [nla-foundations.md](https://github.com/mightytech/nla-framework/blob/main/core/nla-foundations.md) — principles including "Values Are Visible" and "Imperfection Is Assumed"
- [CONTRIBUTING.md](https://github.com/mightytech/nla-framework/blob/main/CONTRIBUTING.md) — the participation infrastructure
- [design-rationale.md](https://github.com/mightytech/nla-framework/blob/main/reference/design-rationale.md) — preserved deliberative reasoning (~1700 lines)

**Governance-relevant applications**
- [Penny Post](https://github.com/mightytech/nla-penny-post) — feedback conventions and the accountability chain
- [NLA Office Hours](https://github.com/mightytech/nla-office-hours) — public Q&A as interactive transparency
- [Process Helpers](https://github.com/mightytech/nla-process-helpers) — deliberative techniques as invocable skills
- [nla-claude-code](https://github.com/mightytech/nla-claude-code) — governance patterns deposited into traditional codebases
