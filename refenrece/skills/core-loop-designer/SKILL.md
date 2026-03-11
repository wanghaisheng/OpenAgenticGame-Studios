---
name: core-loop-designer
description: >
  Define the fundamental action cycle — what the player does repeatedly and why
  it stays engaging. The heartbeat of the game. Use this skill when:
  (1) translating pillars and experience targets into a concrete gameplay cycle,
  (2) diagnosing why a game feels repetitive or disengaging, (3) designing nested
  loop structures (moment-to-moment, session, meta/campaign), (4) identifying
  attrition risk points where players disengage, (5) evaluating whether a
  proposed mechanic serves the core loop or fragments it, (6) designing how the
  loop evolves over time to sustain long-term engagement. Medium-agnostic —
  works for digital, tabletop, and hybrid games.
---

# Core Loop Designer

The core loop is the heartbeat of the game — the fundamental cycle the player repeats. If the heartbeat is wrong, no amount of content, narrative, or polish saves the game. Get this right first.

## What Is a Core Loop?

A core loop is the minimum cycle of player action that produces engagement. It has four phases:

```
ACTION → FEEDBACK → REWARD → DECISION → (back to ACTION)
```

- **Action** — What the player does (move, shoot, play a card, place a worker)
- **Feedback** — What the game tells the player happened (hit markers, dice results, board state change)
- **Reward** — What the player gains (resources, knowledge, position, power, narrative progression)
- **Decision** — What the player must decide next (where to go, what to spend, what to prioritize)

The decision phase is what makes it a *game loop* and not just a *task loop*. Without meaningful decision, the loop degenerates into button-pressing or procedure-following.

**Quality test:** Remove the reward. Is the action itself satisfying? If yes, the loop has intrinsic engagement. If no, the loop is reward-dependent and fragile.

## Loop Hierarchy

Games have nested loops at different time scales. Each loop wraps the one below it.

### Micro Loop (Moment-to-Moment)
The tightest cycle — measured in seconds.
- Digital: Aim → Shoot → Hit/Miss → Adjust aim
- Tabletop: Draw card → Evaluate hand → Play card → Resolve effect
- Duration: 2-30 seconds

### Core Loop (Per-Turn/Per-Encounter)
The primary gameplay cycle — measured in minutes.
- Digital: Enter area → Navigate threats → Collect loot → Choose next area
- Tabletop: Worker placement round → Resource conversion → Scoring check → Next round
- Duration: 1-10 minutes

### Session Loop (Per-Play-Session)
What a single sitting of play feels like — measured in the full session.
- Digital: Select mission → Play through encounters → Receive rewards → Upgrade/unlock → Select next mission
- Tabletop: Setup → Play through rounds → Final scoring → Post-game discussion
- Duration: 20 minutes to 4+ hours

### Meta Loop (Cross-Session/Campaign)
What keeps players coming back across multiple sessions.
- Digital: Complete chapter → Unlock new abilities/areas → Face escalating challenges → Complete campaign
- Tabletop: Play campaign scenario → Unlock new content → Character progression → Next scenario
- Duration: Days to months

### Loop Nesting Diagram

```
META LOOP (across sessions)
├── SESSION LOOP (one sitting)
│   ├── CORE LOOP (one turn/encounter)
│   │   ├── MICRO LOOP (one action)
│   │   ├── MICRO LOOP
│   │   └── MICRO LOOP
│   ├── CORE LOOP
│   └── CORE LOOP
├── SESSION LOOP
└── SESSION LOOP
```

**Rule of thumb:** Each loop level should contain 3-10 iterations of the level below it. Fewer than 3 and the outer loop feels empty. More than 10 and it feels grinding.

## Core Deliverables

### 1. Primary Loop Diagram

Map the core loop with specific actions, not abstractions:

```
PHASE       PLAYER ACTION              GAME RESPONSE           PLAYER DECISION
─────────── ────────────────────────── ──────────────────────── ─────────────────────
Action      [What exactly do they do?]
Feedback                               [What happens visually,
                                        aurally, mechanically?]
Reward                                 [What do they gain?
                                        Is it immediate or
                                        deferred?]
Decision                                                        [What must they
                                                                 decide before the
                                                                 next action?]
```

**Anti-patterns:**
- **No decision point** — "Kill enemies → Get XP → Kill more enemies" has no meaningful choice
- **Deferred reward only** — If all rewards are long-term, the loop has no short-term pull
- **Feedback vacuum** — Actions without clear, immediate feedback feel disconnected
- **Decision paralysis** — Too many options at the decision point stalls the loop

### 2. Loop Evolution Model

The loop must change over time or it becomes monotonous. Define how:

```
PHASE           WHAT CHANGES              WHY IT STAYS ENGAGING
─────────────── ───────────────────────── ────────────────────────────
First hour      [Simplified loop]          Learning the rhythm
Hours 2-5       [Full loop introduced]     Mastering the basics
Hours 5-20      [Loop deepens]             New layers of decision
Hours 20+       [Loop transcends]          Creative/expressive play
```

**Evolution mechanisms:**
- **Additive** — New systems layer onto the existing loop (Slay the Spire adding relics)
- **Transformative** — The loop itself changes shape (Outer Wilds shifting from exploration to puzzle-solving)
- **Expansive** — Same loop, bigger stakes (Civilization's early game vs. late game)
- **Player-driven** — The player chooses how the loop changes (skill trees, build choices)

### 3. Engagement Hook Inventory

For each phase of the loop, identify what creates the pull to continue:

**Micro-level hooks** (why complete this action):
- Satisfying feedback (game feel, juice, tactile pleasure)
- Immediate curiosity ("what's behind this door?")
- Competitive pressure ("they're about to score")

**Core-level hooks** (why complete this turn/encounter):
- Sunk cost momentum ("I'm halfway through this dungeon")
- Escalating stakes ("one more hit and the boss is dead")
- Resource accumulation ("I need 3 more gold for that upgrade")

**Session-level hooks** (why keep playing this sitting):
- Goal proximity ("one more mission to unlock the new area")
- Social momentum ("our group is having fun")
- Flow state maintenance ("I'm in the zone")

**Meta-level hooks** (why come back tomorrow):
- Unfinished progression ("I was so close to that unlock")
- Social commitment ("our group plays Thursdays")
- Anticipation of novelty ("the new content drops tomorrow")

### 4. Attrition Risk Map

Identify where players are most likely to disengage and why:

```
RISK POINT           SYMPTOM                    CAUSE                    MITIGATION
──────────────────── ────────────────────────── ──────────────────────── ─────────────────
[When in the loop?]  [What does quitting        [Why does it happen?]   [How do we
                      look like?]                                        prevent it?]
```

**Common attrition points:**
- **Tutorial exit** — Loop isn't engaging yet because training wheels remove all decision
- **First plateau** — Initial learning curve mastered, nothing new introduced
- **Mid-game sag** — Content between early excitement and endgame payoff
- **Grind wall** — Reward rate drops below engagement threshold
- **Social decay** — Multiplayer groups fragment, social hooks disappear

### 5. Loop-Pillar Alignment Check

Every phase of the loop must serve at least one pillar:

```
LOOP PHASE    PILLAR 1     PILLAR 2     PILLAR 3     PILLAR 4
────────────  ──────────── ──────────── ──────────── ────────────
Action        [Serves/Conflicts/Neutral]
Feedback      [Serves/Conflicts/Neutral]
Reward        [Serves/Conflicts/Neutral]
Decision      [Serves/Conflicts/Neutral]
```

Any row with all Neutral is a dead phase — it exists mechanically but doesn't serve the game's identity.
Any Conflict requires immediate attention — a loop phase that contradicts a pillar is an active problem.

## Loop Patterns

Common loop structures to consider:

### Linear Loop
```
A → B → C → D → (repeat)
```
Simple, readable, easy to learn. Risk: monotony.
*Examples:* Most turn-based games, roguelite run structure

### Branching Loop
```
A → B → {C1 or C2 or C3} → D → (repeat)
```
Decision creates variety. Risk: analysis paralysis.
*Examples:* Open-world mission selection, deck-building card choices

### Parallel Loop
```
A1 → B1 → C1 ─┐
A2 → B2 → C2 ─┤→ D → (repeat)
A3 → B3 → C3 ─┘
```
Multiple simultaneous systems converge. Risk: cognitive overload.
*Examples:* Real-time strategy (economy + army + tech simultaneously)

### Hub-and-Spoke Loop
```
    ┌→ B1 → C1 ─┐
A ──┼→ B2 → C2 ─┼→ A (hub) → (repeat)
    └→ B3 → C3 ─┘
```
Central hub with radiating activities. Risk: hub becomes boring.
*Examples:* Monster Hunter (hub town → hunt → return), Hades (hub → run → return)

### Escalating Loop
```
A1 → B1 → C1 → A2(harder) → B2(richer) → C2(better) → ...
```
Same structure with increasing stakes. Risk: difficulty spike or reward fatigue.
*Examples:* Roguelites with escalating floors, campaign progression

## Workflow

### Designing a core loop from scratch

1. **Start with the core fantasy** (Skill 1) — What does the player do in the fantasy? That's the seed of the action phase.
2. **Reference the experience model** (Skill 4) — What emotion should the loop produce? Flow? Tension? Discovery?
3. **Define the micro loop first** — What's the smallest satisfying cycle?
4. **Build outward** — Wrap the micro loop in the core loop, then session, then meta
5. **Map the four phases** — For each loop level: action, feedback, reward, decision
6. **Check for decision** — Does every loop level have a meaningful choice? No decision = no game.
7. **Define evolution** — How does each loop change over time?
8. **Identify engagement hooks** — What creates pull at each level?
9. **Map attrition risks** — Where will players quit? How do you prevent it?
10. **Run pillar alignment** — Does the loop serve the pillars?
11. **Cross-check with aesthetic direction** (Skill 3) — Game feel targets directly affect how the loop *feels*

### Diagnosing a broken loop

1. Identify the symptom: Is the game boring? Confusing? Repetitive? Frustrating?
2. Locate which loop level is failing (micro, core, session, or meta)
3. Check each phase at that level:
   - **Action phase problem?** — Is the action itself unsatisfying? (Game feel issue → Skill 3)
   - **Feedback problem?** — Is the player getting clear response? (Communication issue → Skill 18)
   - **Reward problem?** — Is the reward motivating? (Economy issue → Skill 10)
   - **Decision problem?** — Is there meaningful choice? (Design issue → Skill 2/6)
4. Check loop evolution — Has the loop stopped evolving? Is the player stuck in a mastered pattern?
5. Check nesting — Are the outer loops wrapping the inner loops properly, or are there gaps?
6. Propose fix and flag to Coherence Engine (Skill 0) for impact analysis

### Evaluating a proposed feature against the loop

1. Does this feature live inside an existing loop phase, or does it create a new one?
2. If inside: Does it strengthen or fragment the phase it lives in?
3. If new: Does it nest properly into the loop hierarchy?
4. Does it create a new decision point? If not, it might be content but not gameplay.
5. Does it serve the loop's evolution model, or is it a one-time distraction?

## Outputs

This skill produces:
1. **Primary loop diagram** — all four phases mapped with specific actions
2. **Loop hierarchy** — micro, core, session, and meta loops with nesting
3. **Loop evolution model** — how the loop changes over hours 1, 5, 20, and 100
4. **Engagement hook inventory** — what creates pull at each level
5. **Attrition risk map** — where players disengage and how to prevent it
6. **Loop-pillar alignment check** — verified that every loop phase serves a pillar

These outputs feed into:
- **Skill 8 (Rules)** — The loop must be formalized into rules
- **Skill 9 (Systems)** — Systems must support the loop's interactions
- **Skill 10 (Economy)** — Economy powers the reward phase
- **Skill 11 (Balance)** — The loop must stay balanced across its evolution
- **Skill 13 (Levels)** — Encounters are instances of the loop
- **Skill 15 (Prototype)** — The prototype must express the core loop
- **Skill 18 (UI/UX)** — UI surfaces the loop moment-to-moment
