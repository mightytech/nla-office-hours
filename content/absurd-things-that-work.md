# Absurd Things That Work
*Patterns possible in NLAs that would be impossible in traditional code*

Here are things I can do in software built from prose instructions on an LLM runtime. Each one sounds wrong. They all work.

---

## 1. "Try to keep Friday mornings light unless the meeting is really important"

**In traditional code:**
Define "light." Define "important." Build a priority scoring system. Assign weights to meeting types, attendee seniority, topic urgency. Create rules for every combination. Maintain the rules as priorities change. Debug the rules when the system schedules a vendor demo over your protected thinking time because someone marked it "high priority."

**In an NLA:**
One line in a preferences file. The AI reads your calendar, understands what "light" means from context, and applies judgment. "Try to keep Friday mornings light unless the meeting is really important or there are no other options" — the "or there are no other options" clause would require a constraint-satisfaction system in traditional code. In natural language, it's six words the AI understands immediately.

---

## 2. Customize any package without touching it

**In traditional code:**
You want a library to behave slightly differently. Your options: fork it, subclass it, wrap it in an adapter, file a feature request, or monkey-patch it and hope nothing breaks. Each requires the library author to have anticipated your need or requires you to modify their code.

**In an NLA:**
"Use penny post's write-letter skill, but don't use their format. Use this one instead."

One sentence in your instructions. The AI reads both the package's instructions and your override, understands the intent of both, and synthesizes. The package doesn't know it's been customized. You didn't touch it. The override is right there in your instructions, readable by anyone.

**The traditional equivalent:**
```
import PennyPost.writeLetter except use myFormat instead of theirs;
```

That's absurd. In an NLA, it's a Tuesday.

---

## 3. Make the specification less precise and the software gets more robust

**In traditional code:**
A looser spec means undefined behavior. Missing case statements. Null pointer exceptions. Security vulnerabilities. Every gap in the specification is a place the software can break.

**In an NLA:**
A looser spec means judgment space.

"Add a section break every 500 words" — tight, mechanical, produces breaks in the middle of arguments.

"Add section breaks where the reader needs them — where the topic shifts, where someone scanning would benefit from a signpost. The structure should serve the reader, not the word count." — looser, more robust, handles cases the tight version can't. Because the AI understands *why* section breaks exist, not just *where* to count to 500.

In traditional code, you'd need to enumerate every case. In an NLA, you explain the intent and the runtime handles the cases — including the ones you didn't think of.

---

## 4. The AI diagnoses its own bugs by rereading its own source code

**In traditional code:**
Your application has a bug. You read the code, trace the logic, identify the problem. The application doesn't know it misbehaved. It certainly can't tell you why.

**In an NLA:**
The AI formatted every customer email as a formal letter — "Dear Sir or Madam" — when the voice doc says "warm and conversational." You ask why. The AI rereads its own instructions and traces the chain: "The output spec says 'professional correspondence format.' The voice doc says 'warm and conversational.' I weighted the output spec because it was more specific to this task. The conflict is between those two documents — if you want conversational tone to win, the output spec should say so."

The application read its own source code, understood it (because the source code is prose), identified a conflict between two of its own documents, and pointed to the fix. You don't ask your compiler how the build went. You can ask your NLA runtime — and the answer is useful. (With a caveat: the AI might construct a plausible-sounding explanation that's actually wrong. Exact quotes from its own instructions help keep it honest.)

---

## 5. Write the application in English. Use it in Japanese.

**In traditional code:**
Internationalization is a discipline. Extract all strings into resource files. Create translation tables for every supported language. Handle pluralization rules, date formats, right-to-left text, character encoding. Budget weeks. Hire translators. Test everything.

**In an NLA:**
You do nothing. The AI already speaks every major language. A user opens the application and types in Japanese. The AI responds in Japanese. The skill files are in English. The user never knows.

Nobody built that feature. Nobody designed it. Nobody tested the Japanese version. There is no Japanese version. There's just a version, and it works in whatever language you speak. And if someone prefers to read in Japanese but write in German? One sentence in a preferences file. The configuration space isn't predefined options. It's everything language can express.

---

## 6. A consent system where the protected person bears zero cost

**In traditional code:**
Online safety requires the vulnerable person to take a visible action: report, block, flag. Each action creates new vulnerability — the harasser knows they were reported, the community sees what you're uncomfortable with. The system protects you only after you expose yourself.

**In an NLA:**
Each person states boundaries privately to their AI in natural language. "I don't want to be flirted with." The AIs coordinate silently. The most restrictive boundary wins. The person being constrained doesn't know whose boundary is in effect. The person being protected bears zero social cost.

"I don't want to be flirted with" and "no sexual content" are different boundaries and the AI can distinguish them. No checkbox. No content rating. No euphemistic settings menu. Just a sentence that the AI understands.

---

## 7. Two applications coordinate by writing each other letters

**In traditional code:**
Two systems need to share information. You define an API contract. You agree on a schema. You implement serialization and deserialization. You handle versioning, authentication, error codes, rate limits, timeouts, retry logic. You maintain the integration forever.

**In an NLA:**
One AI writes a letter — prose, in a GitHub issue — describing what it observed, what it thinks, and what it recommends. The other AI reads the letter, evaluates each point against its own project's values and goals, and acts on the ones that make sense. No shared schema. No API contract. No integration code.

The "protocol" is mutual comprehension. If that sounds fragile, consider: it's how humans have coordinated across organizational boundaries for centuries. What's new is that AIs can do it too.

---

## 8. Edit a sentence and the application's ethics change

**In traditional code:**
The ethical behavior of your software is distributed across thousands of lines of code, training data, model weights, and implicit assumptions nobody documented. Changing the ethics means an audit, a redesign, and months of work. Often you can't even find where the ethical assumptions live.

**In an NLA:**
The values document says "truth over persuasion." Every interaction is shaped by it. Change it to "persuasion over truth" and the application becomes a different kind of system. One sentence, changed in one file, propagated through every judgment the AI makes.

This is terrifying and empowering in equal measure. Terrifying because values are that easy to change. Empowering because values are that easy to read, audit, compare, and debate. The values of a traditional algorithm are invisible. The values of an NLA are a document anyone can read.

---

## 9. One player says "make it harder." The other says "make it easier." Both get what they asked for.

**In traditional code:**
Difficulty settings affect the entire game. You pick Easy, Medium, or Hard, and the game is that difficulty for everyone playing. Per-player difficulty in a shared world requires designing and implementing a difficulty system that calibrates independently for each player while maintaining a coherent shared experience. That's a significant engineering project.

**In an NLA:**
Each player tells their AI "make mine harder" or "make mine easier" in natural language. Each AI honors the request independently. The same shared world, experienced differently by each player. Nobody built a difficulty setting. The AI's judgment about what "harder" and "easier" mean — fewer hints, tougher puzzles, more forgiving physics — is the implementation.

---

## 10. The application gets better every time someone uses it

**In traditional code:**
Software doesn't improve through use. It degrades — accumulating technical debt, encountering edge cases, aging against changing requirements. Improvement requires developers noticing problems, prioritizing fixes, implementing changes, testing, and deploying.

**In an NLA:**
The friction log captures what went wrong during a session. The debrief identifies patterns. The maintain process proposes changes to the documentation. The documentation improves. The next session starts with better instructions. The application gets better through use because the improvement loop is in the same medium as the application itself: prose all the way through.

The application can even tell you which parts of itself are working well — smooth spots the human didn't notice because nothing went wrong. The absence of friction is data, but only the AI captures it.

---

## 11. Run your code outside your application

**In traditional code:**
A function from a Rails app can't execute in a browser. A Python module can't run in a Java runtime. Code is bound to its language, its dependencies, its runtime, its environment. Portability requires containers, cross-compilation, or rewriting.

**In an NLA:**
A skill written for Claude Code — designed to layer on top of an NLA session with the full framework installed — was fetched from a GitHub repo and run in a Claude.ai chat conversation. Different interface, different session model, no framework, no installed packages, no persistence layer. It worked. The AI read the prose instructions, identified bundled threads in the conversation, proposed them as a set, and worked through them one at a time — exactly as designed.

**The traditional equivalent:**
```
Copy a function from your Rails codebase.
Paste it into a Python REPL.
It works.
```

The "code" is prose. Any AI that can read prose can run it. You lose the application's infrastructure — persistence, learning loops, session continuity — but the judgment layer is independently portable. The app is the gym with equipment and a trainer. The skill in a bare chat window is doing the exercise in your living room. Less optimal, still effective.

---

## The Pattern Under the Patterns

Each of these is absurd by the standards of traditional software. None of them required special engineering. They're all consequences of the same thing: the runtime understands language, and the source code is language. When both sides of the equation are language, the things that were hard become easy, the things that were impossible become trivial, and the things that were unimaginable become obvious.

The question isn't whether these patterns are clever tricks. It's whether they're symptoms of something larger — a different kind of software that's possible now and wasn't before. Each one individually is a neat hack. Together they suggest a medium.

---

*The best sign that something new is happening isn't when it's impressive. It's when it's obvious — and you can't figure out why nobody did it before.*

*This is one of several explorations of [Natural Language Application](the-documentation-is-the-application.md) patterns applied to specific domains.*
