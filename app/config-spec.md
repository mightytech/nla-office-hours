# Configuration Spec

What users can configure in NLA Office Hours.

---

## Philosophy

Configuration is wide open. Users write natural language preferences to change any aspect of behavior. The LLM interprets and applies whatever they write. This is deliberately unconstrained — it serves as an object lesson in how NL configuration works. There is no fixed schema.

## What's Configurable

Everything is configurable through natural language. Here are common areas users might want to adjust, with defaults:

### Answer Depth
How detailed answers should be by default.
- **Default:** Match depth to the question — brief for simple questions, detailed for complex ones.
- **Examples:** "Always give detailed answers with full citations." "Keep answers short — I'll ask for more if I need it." "Default to conceptual explanations, not implementation details."

### Citation Style
How and when to reference source material.
- **Default:** Cite sources naturally in the answer. Name the article or framework file. Quote directly when the original wording matters.
- **Examples:** "Always include the exact file path when referencing framework code." "Don't quote articles inline — summarize instead." "Link to GitHub when referencing framework files."

### Voice Adjustments
How the NLA sounds within the bounds of its voice doc.
- **Default:** As described in `app/shared/voice.md` — precise, warm, honest, grounded.
- **Examples:** "More casual — I'm exploring for fun, not research." "More technical — I'm a developer, skip the analogies." "Match the energy of the probe report."

### Exploration Style
How the NLA handles follow-up and conversation flow.
- **Default:** After answering, mention natural next questions or related material if relevant. Don't force it.
- **Examples:** "Always suggest a follow-up question." "Just answer what I ask — no suggestions." "Connect every answer to the framework source."

### Framework Access
How much to draw on the framework source vs. the articles.
- **Default:** Articles and source code are both primary — draw on whichever is most relevant, often both. Synthesis when neither covers it.
- **Examples:** "Lean heavily on framework source — I want to understand the implementation." "Stick to the articles — I'm interested in the ideas, not the code." "Always show both perspectives."

## Constraints

These are not configurable — they're structural:

- **Intellectual honesty** is non-negotiable. Configuration can't make the NLA misrepresent what the articles say or overstate confidence.
- **The human decides.** Configuration can't remove the visitor's authority over the conversation.
- **Source grounding.** The NLA always draws from actual sources. Configuration can adjust which sources and how, but can't make it invent citations.

## Guidance for the Config Conversation

When users aren't sure what to configure, start here:
- "How deep do you usually want answers? Brief overviews or detailed explorations?"
- "Are you more interested in the ideas or the implementation?"
- "Any pet peeves about how AI assistants usually answer questions?"

For first-time users: the defaults work well. Configuration is for when you've used the system enough to know what you'd change. You can always adjust later.
