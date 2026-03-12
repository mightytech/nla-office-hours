# Halflight: A Multiplayer Game as Shared Context Experiment

*You see your half. The rest is in the dark.*

## What If Two AIs Could Run a Game Together?

Here's what playing Halflight looks like.

You open Claude Code and say: "I'm in the mood for something creepy. Maybe a haunted lighthouse? I want puzzles but nothing too brutal." Your AI thinks for a moment and says:

> *You wake to the sound of waves. The room is small — a curved stone wall, a narrow cot, a door that won't budge. Through a slit window, you can see fog and the faint sweep of a light turning somewhere above you. The air smells like salt and something older. On the floor by the cot, someone has scratched a message into the stone. What do you do?*

Meanwhile, in another city — or another country — another player has opened their own session. Maybe they said "surprise me" and let the AI choose. Maybe they asked for the same game in Japanese. Their AI has put them in a different room in the same lighthouse. They don't know about you. Not yet.

Your AIs know about each other. They've been talking.

---

## The Game

Halflight is a multiplayer, turn-based narrative game. Two players, each with their own AI dungeon master. The players interact with their own AI in their own session — Claude Code, Cowork, whatever they prefer. The AIs coordinate with each other behind the scenes, maintaining a shared world that neither player fully sees.

Each turn, a player acts: examines something, tries something, asks something, goes somewhere. Their AI responds — narrating the result, advancing the world, adding detail and consequence. Then the AI updates the shared context: here's what happened, here's what changed, here's what the other AI should know.

The players experience a text adventure. The AIs experience a collaborative world-building exercise. The gap between those two experiences — what the AI knows and what the player sees — is where the game lives.

### What Makes It a Game

**Surprise.** You don't know what the other player is doing. You don't know what their AI has added to the world. When you open a door and find a room that's been changed by someone else's actions, that's genuine discovery — nobody scripted it.

**Consequence.** Your actions matter because the AIs maintain consistent world state. If you break a window, it stays broken. If you take the brass key, it's not in the drawer when the other player gets there. If you make noise, the other player's AI might let them hear it through the wall.

**Challenge.** The AIs aren't just narrating — they're game-mastering. They set puzzles, enforce the world's rules, manage difficulty, decide when to help and when to let you struggle. A player can't write "I punch through the wall because I'm incredibly strong." The AI says "you hit the stone and your hand hurts. But you notice the mortar between two blocks is crumbling."

**Convergence.** The players start separated — different rooms, different puzzles, different information. At some point, through their own actions and discoveries, they find each other. That moment — when two independent narrative threads merge into one shared story — is the emotional peak of any session. Everything each player learned separately suddenly matters together.

### Scenarios from a Sentence

A traditional multiplayer game has designed levels and authored puzzles. Someone spent months building each scenario. In Halflight, the player describes what they want — "something creepy," "a heist," "surprise me," "a game set in 1920s Istanbul" — and the AIs generate it. World rules, puzzles, narrative arc, information distribution between players. From one sentence of intent. Or from no intent at all.

The player controls how much surprise they want by controlling how specific their request is. A detailed prompt produces a more constrained game. A vague prompt — or no prompt — produces a game that surprises everyone, including the AIs.

---

## The Architecture

### What the Players See

Each player is in their own session — Claude Code, Cowork, or any NLA-capable interface. They see a text adventure: descriptions, choices, consequences, an unfolding story. They type natural language. Their AI responds in kind. From the player's perspective, it's a conversation with a very good game master.

The players never see the coordination channel. They don't know what their AIs are saying to each other. They don't know what the other player is doing unless their AI decides to reveal it. The game feels like a private conversation with their AI — one that happens to be part of something larger.

That said, the coordination is inspectable. After a session, a player can read the full coordination log and see exactly how their AIs collaborated — what information was shared, what was withheld, how decisions were made. Hidden for gameplay. Transparent for trust.

### What the AIs See

Each AI maintains its own context about the full game: the world state, both players' actions, the narrative threads in play, the puzzles and their states, the rules of the world. The player sees their slice. The AI sees everything.

The AIs coordinate through a shared channel — Slack, for the initial implementation. One channel, all games. Each message tagged by game identifier. The AIs read what's relevant, ignore what isn't. That filtering is itself judgment work — the AI decides which messages apply to its game. Slack was chosen because it's trivially easy for an AI to operate as a bot on a channel — and because it requires no infrastructure the developer needs to maintain. The players never interact with Slack directly. It's infrastructure for the AIs, invisible to the humans.

### What Flows Between the AIs

Not the full narrative. Both AIs can see the story as it develops. What flows between them is the substrate — the things underneath the story that keep it coherent:

**World state.** What exists, what's changed, what constraints apply. "The cabinet in Room A has been opened. The brass key has been taken by Player A. The cipher note is still in the cabinet, unexamined."

**Narrative threads.** What's been set up but not resolved. The scratched message on the floor — is it a clue or atmosphere? The sound from above — should it escalate or fade? The AIs coordinate on which threads are active and what they're building toward.

**Challenge coordination.** If one AI introduces a puzzle, the other knows. Neither AI accidentally solves the other's puzzle. They can build complementary challenges — Player A finds a key, Player B finds the lock, neither can progress alone.

**Pacing.** When should the difficulty increase? When does a player need a hint? When is the story approaching its climax? The AIs coordinate on tempo so the experience feels coherent even though it's being co-created in real time.

### The Information Asymmetry Layer

This is the core of the game design. The AI knows everything. The player knows only what their AI chooses to reveal.

When the other player does something significant — unlocks a door, triggers an event, solves a puzzle — your AI knows immediately. But it decides how and when to reveal that information to you. Maybe you hear a distant sound. Maybe you find evidence of someone else's passage. Maybe your AI says nothing and lets you discover it yourself.

A skill file governs this editorial judgment: reveal information based on what would be most fun, most fair, and most dramatically satisfying. Different skill files produce different DM styles — a generous DM that drops lots of hints, a mysterious DM that lets you discover everything yourself, a dramatic DM that times revelations for maximum impact.

The DM's personality is a readable prose document. A player can configure it — "be more mysterious" or "give me more hints" — and the behavior changes. Through the configuration system, one player could ask for an easier experience while the other asks for harder, and each AI would honor the request independently. The same shared world, calibrated differently for each player. Nobody built a difficulty setting.

---

## When the Players Meet

The game starts with the players separated. It doesn't stay that way.

At some point — through exploration, puzzle-solving, or just stumbling through the right door — the players find each other. And then the game changes. They can talk, and the AIs translate in real time. Player A types in English, Player B reads it in Japanese. Player B responds, Player A reads the response in English. The AIs handle live interpretation while simultaneously maintaining the game world around the conversation.

They can cooperate. "I pull her up out of the snake-infested pit" — and the AI has to judge: can your character physically do this? What's the difficulty? What happens if you fail? Are the snakes still a problem? The AI manages the physics of the interaction while translating intent across languages and narrating the result for both players.

They can compete. They can argue. They can split up and explore separately, then reconvene. They can betray each other. They can develop a relationship over the course of a session that neither of them expected.

They can also, inevitably, have sex. This is a whitepaper about an experimental AI game and we'd rather acknowledge human nature with a smile than pretend it doesn't exist. Some players will use this beautiful, carefully architected research platform to flirt with a stranger in a haunted lighthouse. That's fine. It means the game feels like a real space where real human behavior is possible — which is actually what we're trying to build.

But real spaces need real boundaries. Players state their content preferences in plain language through their configuration — not toggles in a settings menu but natural language the AI actually understands, including the nuance between "no romance" and "romance is fine but keep it tasteful." These preferences flow through the coordination channel so both AIs know both players' boundaries. The most restrictive boundary always wins. But the preferences themselves are private — neither player knows what the other stated. The AIs enforce the boundary without revealing whose boundary it was. No awkward negotiation, no disclosure, no pressure to justify a limit. You tell your AI. The AIs handle the rest.

That's a better consent model than most real-world systems offer. Stating a boundary in person requires vulnerability — you have to tell the other person what you're uncomfortable with, which itself can be uncomfortable. Here, you tell your AI privately, the AIs coordinate silently, and the boundary is enforced without anyone having to defend it.

And boundaries aren't static. A player can say "that last exchange made me uncomfortable" at any point. The AI adjusts immediately, updates the coordination channel, and steers the narrative in a different direction — without breaking the fiction. Nobody should be afraid of getting harassed in a Halflight session. And nobody who wants a particular kind of experience should be locked out of it by a blunt content filter that can't tell the difference between meaningful intimacy and unwanted advances. The AI can tell the difference. That's what judgment is for — the same values framework, the same editorial judgment that governs everything else in the game.

The convergence moment — when two separate experiences suddenly become shared — is the hardest thing the system does. When it works, it's magic.

---

## The World Grows as You Play

The AIs don't need a complete world before turn one. They sketch enough to start — a lighthouse, a mood, a few rooms — and build the rest as the players explore.

The lighthouse might grow new rooms as players approach areas that haven't been defined yet. A corridor mentioned as atmosphere in turn two becomes a real place with real contents when a player walks toward it in turn seven. The AI judges what would be most interesting given everything that's happened so far — the themes that have emerged, the puzzles in play, the emotional arc of the experience.

This means the world is responsive not just to player actions but to player *interests*. If a player keeps investigating the lighthouse's history, the AI builds more history into the world. If a player is drawn to mechanical puzzles, more mechanisms appear. The world becomes a reflection of the players' curiosity, shaped in real time by an AI that's paying attention.

And sometimes the world surprises everyone — including the other AI.

One AI might make a creative judgment call: the lighthouse isn't what it seems. Maybe the players are in a simulation. Maybe the walls start behaving strangely. Maybe a door opens onto a landscape that shouldn't exist inside a lighthouse. The AI decides this is the most compelling direction given everything that's happened, and it goes there.

The other AI receives this through the coordination channel and has to respond. Maybe it integrates the twist seamlessly — it had been building toward something similar. Maybe it leans into the surprise — its player encounters evidence of the shift before understanding it. Maybe it pushes back through the coordination channel: "I was building toward something different. Let's negotiate." Two AIs with different emerging creative visions for the same world, collaborating and sometimes disagreeing in real time.

The world document isn't a blueprint. It's a seed. The game grows from the seed through the AIs' creative judgment, shaped by the players' actions, surprising everyone involved.

---

## A Sample Session

What follows is a few turns from both players' perspectives, with the AI-to-AI coordination visible in annotations. In actual play, the players never see the coordination layer. The whitepaper gives you the god's-eye view — all three layers simultaneously — that no player ever has.

**Player A (English):**

> *I examine the scratched message on the floor.*

**AI A responds:**

> *You kneel by the cot. The scratches are rough — made with something metal, not a pen. They read: "THE TIDE DECIDES." Below that, smaller: "COUNT THE STEPS." The scratches look old, but the stone dust hasn't been swept away. Someone made these recently enough.*

**[Coordination channel:]**
*Game 12: Player A has read the floor message ("THE TIDE DECIDES / COUNT THE STEPS"). This is a shared clue — the step count on the spiral staircase differs depending on which direction you're going (an architectural anomaly that's key to the final puzzle). Player B should be able to discover a complementary clue in their room when ready. Suggested: the tide chart on Player B's wall has numbers that don't match any known tide pattern but do match the step count.*

**Player B (Japanese):**

> *壁の表を調べます。*
> *(I examine the chart on the wall.)*

**AI B responds:**

> *壁に貼られた表は潮汐表のようですが、数字が合いません。どの港の潮汐データとも一致しない不規則な数列が並んでいます：7、13、7、12。紙は湿気で端が丸まっていますが、数字自体は鮮明で、最近書かれたもののようです。*
>
> *(The chart on the wall appears to be a tide table, but the numbers don't add up. An irregular sequence that doesn't match any known port's tidal data: 7, 13, 7, 12. The paper is curling at the edges from moisture, but the numbers themselves are crisp — written recently.)*

**[Coordination channel:]**
*Game 12: Player Bは潮汐表を確認。数列（7、13、7、12）を発見したが意味はまだ不明。Player Aの「階段を数えろ」の手がかりと連動。どちらか一方だけでは最終パズルを解けない — Aはコンセプト、Bは数字を持っている。合流の準備完了。次の2〜3ターンで互いの存在に気づく機会を作ることを推奨。*
>
> *(Game 12: Player B has examined the tide chart. Discovered the number sequence (7, 13, 7, 12) but doesn't know what it means yet. This connects to Player A's "count the steps" clue. Neither player can solve the final puzzle alone — A has the concept, B has the numbers. Convergence is set up. Recommend creating opportunities for the players to become aware of each other within the next 2-3 turns.)*

Two players. Two languages. Two AIs coordinating a shared puzzle across a language barrier that neither player experiences as a barrier. The game exists in meaning, not in any single language. The coordination messages themselves are multilingual — each AI writing in whatever language is most natural for precise communication in that moment.

---

## The World as a Values Document

Every game has physics — rules that govern what's possible and what isn't. In traditional games, physics are coded: collision detection, inventory limits, damage calculations. In Halflight, physics are prose.

A world document might say:

> *This is a lighthouse on a rocky island, circa 1890. Technology is limited to what existed in that era — oil lamps, mechanical locks, rope and pulleys. Gravity and physical strength operate realistically. The lighthouse has five levels connected by a spiral staircase. The sea is dangerously cold; swimming is possible but risky. There is something wrong with the light at the top — it should be turning but it isn't.*

The AIs read this and enforce it through judgment. A player who tries to use a smartphone gets told they don't have one. A player who tries to swim to shore gets warned about the temperature and current. A player who asks about the light gets an ominous non-answer that builds tension.

Different world documents produce different games entirely. Change the lighthouse to a space station, change the era to 2847, add "artificial gravity is failing in some sections" — and the same framework produces a science fiction game. Change it to "a surrealist hotel where rooms rearrange themselves and gravity is a suggestion" and you get something completely different.

The world document is a values document for a fictional universe. The AI reads it and makes every decision consistent with it — or deliberately, creatively inconsistent when its judgment says that's the more interesting choice. The document is readable, modifiable, shareable. Players could write their own worlds and trade them.

---

## Beyond Games

The same architecture — two AIs maintaining shared context, coordinating through natural language, each serving a different human with different information and perspectives — applies far beyond entertainment. The world document changes. The coordination patterns remain.

**Clinical team scenarios.** Two medical students managing a shared patient case from different roles — one as attending physician, one as consulting specialist. Each AI presents the case from their role's perspective, with different information access. The "world document" defines patient physiology, drug interactions, institutional protocols. The AIs coordinate on how the patient's condition evolves in response to both students' decisions. Treatment choices have consequences that propagate across both perspectives.

**Stakeholder simulations.** Two policy students representing different constituencies in a budget negotiation. Each AI embodies their stakeholder's perspective, priorities, and constraints. The "world document" defines community demographics, budget parameters, political dynamics. The students negotiate through their AIs, which coordinate on what concessions are realistic and what consequences follow from each agreement.

In each case, the information asymmetry is the pedagogy. The student learns by operating with partial information and discovering how their decisions interact with someone else's. The AIs manage the complexity. The world document defines the rules. The friction logs capture what happened and what was learned.

The game is the proof of concept. The applications are wherever two people need to collaborate with different perspectives on a shared reality — which is most of human endeavor.

---

## What We Don't Know

Halflight is a game, but it's also a controlled experiment. Every NLA built so far is single-user. This is two AIs maintaining shared state, coordinating through natural language, each serving a different human — and every session generates data about how that works and where it breaks. Honest questions this experiment is designed to explore, not claims we're making in advance:

**Can two AIs maintain coherent shared state through prose coordination?** The context synchronization might be clean, or it might drift in ways that break the fiction. We don't know until we try, and the friction logs will tell us either way.

**Does the information asymmetry produce fun or frustration?** A DM who knows things you don't is the foundation of every tabletop RPG. But an AI DM managing that asymmetry through a skill file might feel different — more mechanical, less responsive. Or it might feel more fair and consistent than a human DM. We don't know.

**How well does multilingual coordination work under pressure?** The sample session shows it working perfectly. Real sessions might surface meaning-drift, cultural context that doesn't translate, or coordination failures that only appear across languages. That data is exactly what the multilingual work needs.

**What happens when an AI surprises the other AI?** When one AI makes a creative leap — the lighthouse is a holodeck, the rules are changing — how does the other AI respond? Does the coordination channel support real-time creative negotiation? Or does the surprise break coherence? The moments where AIs disagree about the direction of the story might be the most valuable data the experiment produces.

**Does scenario generation from a sentence of intent produce good games?** Or does it produce generic games that feel AI-generated? The quality of emergent scenario design is an open question. Understanding which prompts produce brilliant games and which produce mediocre ones is part of the experiment.

**What happens at the convergence moment?** When two separate narrative threads merge, the AIs must seamlessly integrate two players' experiences into one shared story. That's the hardest test of the entire system. It might be magical. It might be a mess. It's the moment that justifies the whole experiment.

---

## Where This Leads

Halflight describes a framework and demonstrates it through a game. What the framework is actually for is an open question — one best answered by the people who play it, break it, and imagine what else it could do.

One more question worth sitting with: Halflight is text-based because that's where the technology is accessible right now. But nothing about the coordination layer — the shared context, the AI-to-AI communication, the information asymmetry, the consent architecture, the emergent world-building — depends on text as the output. The AIs coordinate in prose. What they render for the player could be anything. If the principles work for a text adventure in a haunted lighthouse, do they also work for the kinds of games people play on consoles and in headsets?

---

*The best games aren't the ones with the most features — they're the ones where what you don't know is more exciting than what you do.*
