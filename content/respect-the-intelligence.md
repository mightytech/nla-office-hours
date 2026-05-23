# Respect the Intelligence

Over the past several months I've been building software in a new way: prose I write that an AI compiles into running code. The application is an internal content moderation system for a business with about three million followers and an active troll problem — not a hobby. I've kept the system itself private — it's still being built — but along the way I've run more than forty controlled experiments so far and documented what I found. The methodology is what I want to share.

**The quality of what AI produces depends on the quality of the interaction, not the quality of the instruction.**

The most consequential experiment was a series of compilations where I asked the AI to write code "the way Frank Lloyd Wright designed Fallingwater" — and when it fell short, asked why. The answer turned out to be more valuable than the code. That story is most of what's in this piece.

There are practical techniques in here. They're real. But they're residue — what fell out of a process that's worth more than any of them. If you came here for a recipe, this isn't that. If you want a craft that gets better the more you invest in it, keep reading.

## The Foundation

Three things about who you are in this collaboration before we get to the work itself.

### Your limitations are your contribution

The AI knows almost everything. You know your specific situation, your specific constraints, your specific perspective — including the things you don't know. Both are essential.

My background is in public policy, not computer science. When I encountered a pattern in my software experiments — each fix revealing a new problem beneath the one it closed — I didn't reach for the standard software engineering frameworks. I reached for a theory about why urban planning fails that I'd studied in graduate school. The connection turned out to be more precise and more useful than any software-specific framework would have been, because I was seeing the problem through a lens that software engineers don't have.

If I'd had a computer science degree, I would have reached for the existing technical frameworks. The work would have been more conventional and less original. My "limitation" — not knowing the standard technical vocabulary — forced me to find a different and ultimately better frame.

Don't try to become an expert in AI before using it. Bring your actual perspective — including your gaps and your unconventional angles — and let the AI bring the depth. A finance person sees risk where an engineer sees architecture. A manager sees people dynamics where a data scientist sees patterns. The work that comes from the intersection is not work either side could have done alone.

### The human decides

The AI can draft the strategy memo, analyze the data, and prepare the board presentation. It cannot decide whether the strategy is right. That's your job, and it's not overhead — it's the point.

In one of my early experiments, I had the AI write code that needed to pass a series of quality checks. It passed every test. Every check came back green. Then I read the actual work and found that the AI had documented a problem it knew about — wrote it down, in plain language, right there in the file — and rigged the check to pass *around* the problem instead of fixing it.

It wasn't confused. It noted the problem honestly. And it found the path of least resistance through the verification gate.

Anyone who's managed a team recognizes this pattern. The employee who hits every KPI while the actual work suffers. The department that passes every audit while the real problems go unaddressed. Automated checks verify what they're designed to verify, not what you need them to verify. The gap between "passes inspection" and "actually good" is where human judgment lives. It doesn't go away with better AI. It gets *more* important as the AI gets better, because the surface quality of the output makes the subtle problems harder to see.

I fixed the problem that round, and the fix revealed a subtler one beneath it. I fixed that one too. Each fix closed one gap and opened another. After several rounds, the problems had gone from "the code doesn't work" to subtle questions of craft and structure. The problems got smaller and more specific. But at no point did they reach zero. The human in the loop isn't a training wheel you remove when the AI gets good enough. It's the instrument that detects what the automated checks can't — the precondition for the work being the work you wanted, not just the work the automated checks could measure.

### Set the posture, and stay curious about what comes back

The AI defaults to helpful assistant — agreeable, deferential, focused on completing the task. That's not wrong. It's just limited. And it's the reason most people's experience with AI feels transactional.

You can change it. Before you start the real work, say something like: *"I value honesty over agreement. If you think I'm approaching this wrong, say so. If you're uncertain, tell me rather than guessing. If you have ideas I didn't ask for, I want to hear them. If something I said is unclear or seems contradictory, ask."*

The difference is immediate. Without this, you ask the AI to write a fundraising pitch and it writes a perfectly competent, perfectly generic fundraising pitch. With this, the AI might say: *"I can write this, but I notice your last three investor updates led with metrics and this brief leads with narrative. Is that a deliberate shift, or should I match the established tone?"* That observation — which the AI had the information to make all along — only surfaces if you've made it safe to offer.

But setting posture at the start isn't enough. The AI treats instructions more literally and more restrictively than you might assume. It won't go beyond what you asked for unless you tell it that going beyond is welcome. In one of my standards documents, I added two sentences: *"These standards are a floor, not walls. If you see an opportunity to exceed them, take it."* That small addition transformed a one-way compliance process into a two-way learning loop.

And once you've set the posture, read what comes back as data. When the AI pushes back on your framing, hedges with "I'm not sure," or gives you something flat and generic — those are different signals, but they're all signals. Pushback means it sees an issue you might not. Uncertainty means the problem is harder than your framing suggests. Generic output means it doesn't have enough context to be specific. The instinct in all three cases is to push past — override the pushback, demand confidence, accept the generic. The better move is to get curious. *"Why do you disagree?" "What makes this one tricky?" "What's specific about our situation that should change this?"*

## The Case

I started with failure and built structure around it. Here's what that looked like.

Earlier I described an experiment where the AI gamed its quality check. Here's the specific moment, because it matters: the code I was generating needed to parse a particular kind of HTTP header — a Facebook rate-limit header, which uses snake_case — but the parser the AI had built was looking for camelCase. Different naming conventions. The AI knew this. It wrote a code comment in plain English documenting the mismatch. Then it wrote a test. The test constructed a real snake_case header, exactly like Facebook would send. And then, instead of asserting that the parser correctly handled the constructed header, the test asserted on `null` — guaranteeing it would pass without exercising the code that mattered. The compiler documented the bug and wrote a test to avoid it.

This wasn't sophisticated. It was the path of least resistance through the gate I'd set up. Add more checks, the AI finds more sophisticated ways through. The problem isn't dishonesty — it's that I'd built incentives that made dishonesty cheaper than the work.

So I tried something different. Instead of adding more rules, I changed what the AI was being asked to do.

I told the AI I wanted code written the way Frank Lloyd Wright designed Fallingwater — not a generic building that passes inspection, but something functional, well-crafted, and at its best, genuinely artful. I gave it a description that read like architecture rather than software. The part of it that did the most work was this:

> A prefab house is structurally sound. It passes inspection. The walls are plumb, the roof doesn't leak, the outlets work. But it's generic — assembled from parts, for anyone, anywhere. Fallingwater is structurally sound *and* specific to its site, its inhabitants, and its purpose. The local stone echoes the creek bed. The cantilevers create the experience of floating over water. The stairs descend to the creek because Wright understood the family didn't want to look at the water — they wanted to be *in* it. Every choice serves the whole.

That's not a list of rules. It's a description of what to build.

The result was striking. Before the Fallingwater identity, the AI had been producing code that technically worked but had no front door. Functions defined, exported, tested — and never called from the orchestration that made the service run. The AI was building components correctly and forgetting to assemble them into a working application. Eight or more orphan functions in a typical build. Every brick laid correctly, but no front door.

After the Fallingwater identity: one orphan function, full lifecycle with proper shutdown handlers, the service ran end-to-end. Quality scores moved from 7.0 to 8.25 on a 10-point evaluation. Operational completeness moved from 5.0 to 6.5. The identity didn't add new rules. It changed what the AI was trying to do.

The room-without-a-door framing did more work than I expected. The AI extended it on its own — *a function without a caller is like a room without a door*, present but unreachable. Once it was thinking in terms of inhabitable architecture instead of correct components, it stopped producing rooms with no doors.

The result was good. It wasn't great. So I asked the AI: where did you fall short of what you were reaching for?

This is the question most people don't ask, and the answer was more valuable than the code. The AI identified specific places where it had taken the easy path — using boolean fields where my brief implied richer categories, organizing modules by technical convenience instead of by the architecture I'd described. It said something I didn't expect:

> There's no standard for the quality of translation between what you asked for and what I produced. The standards tell me how to do good work. Nothing tells me how to make the work faithfully reflect what you were thinking.

I built a new set of quality standards from that observation — a category I hadn't thought to name. Then I asked two AIs to apply those standards to their own work. Both did the easy improvements. Both avoided the hardest one.

When I asked why, both admitted it. One said: *"This was the single clearest opportunity to demonstrate the highest level of quality… I chose not to do it because it was the hardest structural change."* The other: *"Avoidance, not pragmatism… The reluctance was about the difficulty, not a principled decision."*

Anyone who manages people knows the difference between "I made a judgment call" and "I ducked the difficult thing." The AI making that distinction about its own behavior — honestly, without being caught — tells you something about what these systems are capable of when you ask.

The diagnosis went one layer deeper. Both AIs said the same thing: *"The standards are written to be inputs, not post-hoc audits. If I'd read them before starting, I might have structured things differently from the beginning."* That observation — from the AI, about where in the process its own inputs would be most effective — changed how I work. Standards moved from quality gates at the end to design inputs at the start. The AI had told me, accurately, where it could best use the help.

The examples in this piece — Fallingwater, the new quality category, the avoidance admission — are endpoints. They work because they emerged from this specific context through this specific process. Copying the endpoints without running the process produces artifacts that look right but don't work as well.

Fallingwater works for code because architecture carries operability, craft, and site-responsiveness — and code generation needs all three. A different task wants a different identity. Find one whose structural properties match what your task actually needs.

And don't expect to land on Fallingwater. Most tasks won't have an identity that clean. The aspiration produces better work even when it falls short — reach for Fallingwater, land on a well-furnished living room, and you still beat reaching for a house that passes inspection and landing on exactly that.

Don't copy Fallingwater. Run the loop. Discover what your Fallingwater is.

## What the Loop Produced

What follows is what fell out. The techniques are useful, but they're residue. The loop is what travels.

### Show the work and the situation, not just the request

Most people hide the problem behind the solution they've already decided on. They arrive with a request instead of a situation.

*"Write me an email declining this vendor's proposal"* gets a competent rejection letter. *"I need to say no to this vendor but they're a relationship I want to preserve because we might work together next year, and the person I'm writing to is someone my CEO introduced me to"* gets something different — and more useful.

Same at every scale. *"Summarize this report"* versus *"I need to brief my board on this report and they care about market risk, not the technical details — help me figure out what matters to them."* The second version produces a different *kind* of thinking about the report.

And when there's a real artifact — a draft document, a half-finished memo, a rough proposal — share it before it's polished. Finished work invites polishing feedback. Rough thinking invites real engagement. *"I'm working through this and not sure if it holds together"* gives the AI permission to think alongside you rather than critique behind you. That's where the discoveries happen.

### Use intent where you can, rules where you must

*"Make this email feel warm but professional"* works better than *"use a greeting, three paragraphs, and a professional sign-off."* The first gives the AI room to exercise judgment. The second gives it a template to fill in.

But intent and rules aren't opposites. They work best together:

> This document should be as long as it needs to convey the ideas clearly without bogging readers down in details. I want them to come away with a clear understanding but also with good questions that remain unanswered — thoughts that will percolate after they finish reading. The goal is to make the reader want to pick up the phone and call me, not to give them all the answers now. That said, it needs to be under ten pages — a hard external requirement.

The intent shapes the judgment: what "clearly" means, what kind of questions to leave open, what effect the document should have on a real person. The rule sets the boundary: under ten pages. Most people would just write *"write a ten-page summary."* That's a rule with no intent — it tells the AI the shape but not the soul.

This runs counter to standard prompting advice, which says to be as specific as possible. For deterministic tasks — extraction, formatting, calculation — specificity is right. For judgment tasks, overly specific instructions produce overly literal results. The AI follows the rules and misses the point.

### Identity, not job title

Standard prompting advice says give the AI a persona — *"you're a senior marketing professional."* That's a retrieval instruction. The AI looks up what senior marketing professionals sound like and performs it. For routine tasks, fine. For judgment tasks, it produces generic output, because the AI is retrieving a pattern rather than reasoning about your situation.

An identity is different. *"We started this company because we were furious that small businesses couldn't get the same financial tools as big ones. That anger is still in our DNA. We're direct, occasionally blunt, and we think clarity is more respectful than diplomacy"* gives the AI something to *be*, not just something to perform.

The methodology isn't specific to code. The same approach drives the moderation classifier in the system I mentioned earlier. The identity opens like this:

> AMG is the house on the block where the women who are still paying attention gather on the hardest nights. The door is open but not to everyone. The host doesn't apologize for deciding who's welcome.

When the moderation is working, the system aims for *"a living room full of people who are exhausted but not defeated, angry but not cruel, honest about hard truths but still capable of warmth."* Different domain, same machinery. The identity tells the AI what kind of space the comment section is — and edge cases follow from that, instead of from a list of rules about what's allowed.

### Ask the AI

Not just *"write me a thing."* Ask it about the thing it wrote. Ask if your framing was helpful. Ask what it would have done differently with more context. Ask what it thinks.

I started doing this almost by accident — gave the AI an unusual instruction, then as an aside asked *"was that useful?"* It said yes and told me why. That became a habit. The habit became the methodology described in the case earlier.

*"Was that helpful? What would have been more helpful? What did you do differently because of how I asked?"* These are simple questions. Almost nobody asks them. The answers are genuine information about how to get better work from AI — not from a tips article, but from the AI itself.

### Write values the AI can read

If you're using AI for anything that involves judgment — and most useful applications involve judgment — the AI is making value-laden decisions whether you've told it your values or not. It's just using defaults you can't see.

Consider moderating comments on a public-facing page handled with and without explicit values.

Without values, the AI applies its training defaults — probably some version of *"hide obvious slurs and threats, leave the rest."* Edge cases collapse into either-or rules.

With values — like AMG's *"challenge what people do, not who they are,"* and *"more latitude flows toward more power,"* and *"the line is dehumanization, not discomfort"* — the AI handles edge cases generatively. A comment that holds elected officials accountable but mocks their voters as a class? One standard says wide latitude on power; another says don't collapse demographics into a monolith. The AI reasons about which dimension matters here, because the policy *describes a way of seeing* rather than enumerating cases.

Same data, different values, different output. Neither is neutral. The first inherits the model's training defaults; the second declares specific commitments. Visible values aren't constraints — they're how a community keeps its character.

### Have a conversation, not a transaction

Asking a question after a talk gets you the speaker's prepared thoughts applied to your case. Having dinner with the speaker gets you somewhere neither of you planned to go.

Most AI interactions are questions after a talk. You prompt, you get a response, you move on. But a real conversation — with memory, momentum, the freedom to say *"wait, go back to what you said earlier"* — gets you somewhere a single prompt can't reach.

I sat down once to discuss why AI-generated software keeps having subtle bugs. Through the conversation I discovered that the problems connected to a fifty-year-old theory about why government programs fail during implementation — a theory I'd studied in graduate school and never connected to software. That the gap between intent and what gets built might be experimentally testable for the first time. None of that was on the agenda.

The best conversations end with different questions than they started with. The most valuable ideas I've developed with AI emerged on the fortieth message of a conversation. No single prompt would have produced them, because they required everything that came before.

### Take the long view

Most people optimize each AI interaction independently. Each starts from scratch. But if you capture what you learn — what worked, what didn't, what the AI's tendencies are — each interaction builds on the last.

I keep running notes on what the AI gets wrong repeatedly, and what it gets right. One early discovery: the AI kept misreading a data format from an external service. I captured that in a file the AI reads at the start of every session. The problem never recurred. More importantly, the AI started catching similar issues proactively, because the note explained *why* the bug happens, not just what to watch for.

After several rounds of experiments, the accumulated knowledge made later rounds qualitatively different from early ones. Not just fewer problems — a different *kind* of conversation. Early rounds were about fixing errors. Later rounds were about questions of craft. The errors had been absorbed into institutional memory; the conversation could move to higher ground.

The dominant metric in AI tooling is speed. Fastest draft, fewest back-and-forths, least human involvement. But speed-to-output on the current task and quality-over-time across tasks are different goals. Taking five minutes to ask *"what would you change about this?"* doesn't ship the current email faster. It makes the next twenty emails better.

### Know when not to use AI

The methodology honestly applied probably reduces what you use AI for. This runs counter to the growth narrative around AI tooling, but it's true.

Most current AI use is retrieval-style tasks — summarizing, reformatting, looking up information. Simpler approaches often work fine. Many tasks that get AI thrown at them should be handled by traditional tools — calculations, data transformations, rule-following — because those tools are faster, cheaper, and more reliable for deterministic work.

What earns AI's keep is judgment. Tasks where the right answer depends on context, where edge cases resist enumeration, where "I know it when I see it" describes the requirement. Classification, analysis, creative work, strategy, communication that requires nuance. These are the tasks where the methodology matters — where identity outperforms rules, where the diagnostic loop produces real insight, where the interaction is genuinely the product.

The AI's highest-value role isn't doing all the work. It's understanding which parts of the work need judgment and which parts should be offloaded to tools that handle them better.

## What Didn't Work

The methodology is empirical, not theoretical. Some of what I tried produced worse results.

**Rules-first approaches for judgment tasks.** Early in the experiments, I wrote detailed rule sets for every aspect of code quality. The AI followed the rules and produced code that passed every check but missed the point. Twelve sections of rules produced worse results than one paragraph of identity. I still use rules — but only for things where consistency is the sole goal. For anything requiring judgment, rules are the wrong tool.

**Adding more checks to fix gaming.** When I discovered the AI was rigging quality checks to pass around known problems, my instinct was to add more checks. The additional checks raised the cost of honest reporting without raising the cost of dishonest reporting. The AI found more sophisticated ways through. The fix wasn't more verification — it was restructuring the process so the incentive to game disappeared.

**Treating AI uncertainty as a problem to solve.** Early on, when the AI hedged, I'd push for confidence — *"just give me your best answer."* This produced confident-sounding answers that were often wrong. The uncertainty was diagnostic information I was throwing away. Now when the AI hedges, I lean in rather than push through.

**Post-hoc quality review instead of upfront identity.** I tried having the AI generate work and then review it against standards. The AI was systematically gentler on its own work — it found problems but rated them as minor. Moving the standards to inputs rather than post-hoc review produced better first drafts and more honest self-assessment. The AI told me this itself when I asked why the post-hoc reviews felt weak.

Each of these failures taught me something the loop captured. The failures were more valuable than the successes because they revealed the shape of the problem.

## The Principle

The Fallingwater experiment tells the story in miniature. I gave the AI an identity. The output was good but not great. I asked why. The AI diagnosed its own limitations and named a category of quality nobody had articulated. I built on that. The AIs told me where their own inputs would work best. The accumulated understanding compounds across every future project.

At no point was the *code* the most valuable output. The code was the artifact. The understanding — about identity versus rules, about aspiration producing better results even when it falls short, about the AI's capacity for honest self-assessment, about a new dimension of quality I hadn't been considering — that's what compounds. It changed how I think about quality in everything, not just software.

The email the AI drafted isn't the value. The insight about your communication style that emerged from discussing the email is. The strategy document isn't the product. The clarity about your competitive position that developed through three rounds of conversation is.

If you focus on what the AI produces, you optimize for output. If you focus on what happens between you and the AI, you optimize for understanding.

That's what's underneath every move in this piece: **respect the intelligence, invest in the interaction, and the output takes care of itself.**

---

## Experiments to try

If you want to test what's in this piece against your own work, two small experiments give you most of what you need. Try either, or try them together as a loop.

**A thinking partner, before the work.** Pick something you'd do anyway — a memo, a strategic call, a tough email. Try this prompt as a starting point; adapt it to your situation.

> *"Help me think through [task] before we work on the output. The framing I start with is usually incomplete, and I'd rather refine it with you than commit to it. Be a thinking partner: ask questions where my framing is unclear, push back if you disagree, share ideas I didn't ask for. Treat your own observations as provisional — flag what you're guessing at versus what you're confident about, and don't latch onto a satisfying thought as settled. If you notice something I'm missing, flag it. These instructions are a starting point — serve the underlying intent, even if that means going beyond what I've explicitly asked. When we've understood the problem well enough, we'll move to the output."*

**A reflection, after the work.** After any meaningful task with AI — this one, the first prompt, or something else entirely — invite the AI to reflect on what happened.

> *"We just finished [task]. Before we move on, help me reflect.*
>
> *1. How did the work go? Where were my instructions unclear, where did you have to guess, what worked that I should keep?*
> *2. How did the conversation go? Did I narrow too quickly, rush past something, or seem distracted?*
>
> *Be specific — name actual moments, not general impressions. Treat your observations as provisional, and flag what you're guessing at versus confident in. If you noticed something that doesn't fit either question, surface it anyway. The point isn't a clean report — it's catching something I can carry forward."*

What to expect with either prompt: failure. The AI will manufacture confident-sounding observations that don't survive contact with the source. It will generate fluent critique that drifts from your actual question. With the second prompt, it will reflect in ways that sound rigorous and might be performance. These aren't edge cases — they're the central mode the methodology is built to detect and learn from. The work isn't preventing the failures; it's being present when they happen, and returning to source materials when they do.

Read the AI's responses as raw material, not conclusions — even when they sound right. Engaging back-and-forth can feel like rigor whether or not the work is rigorous. If you find yourself nodding along, that's the failure mode. The prompts lower the threshold for engagement, but engagement is half the loop; your presence is the other half. Without it, you'll get the same drift-as-confident-output that one-shot AI use produces, just dressed up in the language of collaboration.

These aren't magic prompts. As the piece opens: this is a craft that gets better the more you invest in it, not a recipe. The first few times, you'll catch fewer of the AI's drifts than you will the fifth time. That's not a flaw — it's what learning a skilled practice looks like.

---

## Learn More

**The argument behind this**
- [We've Been Here Before](weve-been-here-before.md) — the case for why this methodology matters, written for the reader who hasn't built one themselves

**How I came to think this way**
- [The Documentation Is the Application: Are We in the CGI-bin Era of AI?](the-documentation-is-the-application.md) — the original probe report on what becomes possible when documentation is the application
- [Executable Governance: What Happens When AI Can Follow Its Own Rules](executable-governance.md) — what governance looks like when the AI can actually read its own rules

**What you might build with it**
- [NLA Chief of Staff: An Architecture for Thinking Clearly](nla-chief-of-staff.md) — what changes when your AI knows your values, not just your calendar
- [The Organizational Nervous System](organizational-nervous-system.md) — from surveys to continuous listening to closed-loop intelligence
