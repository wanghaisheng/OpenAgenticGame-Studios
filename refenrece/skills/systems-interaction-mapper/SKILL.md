---
name: systems-interaction-mapper
description: >
  Map how all game systems affect each other. Identify feedback loops, emergent
  behaviors, and potential degenerate strategies before they ship. Use this skill
  when: (1) designing a game with multiple interacting systems, (2) diagnosing
  unexpected emergent behavior or exploit paths, (3) evaluating whether adding a
  new system creates healthy or degenerate interactions, (4) identifying which
  systems are too tightly or loosely coupled, (5) mapping feedback loops
  (reinforcing, balancing, broken), (6) predicting where player-discovered
  strategies will emerge, (7) understanding why a balance change in one system
  cascades unexpectedly. Medium-agnostic — works for digital, tabletop, and
  hybrid games.
---

# Systems Interaction Mapper

Every game is a web of interconnected systems. Combat affects economy. Economy affects progression. Progression affects combat. This skill maps those connections, finds the feedback loops, and predicts where the web will produce genius or disaster.

## Systems Thinking for Games

A "system" in game design is any set of rules that manages a domain of game state. Combat is a system. Inventory is a system. Movement is a system. Weather is a system. The interesting design isn't in the systems themselves — it's in the spaces *between* them.

### What Makes a System

A game system has:
- **State** — Variables it tracks (HP, gold, position, reputation)
- **Inputs** — What other systems or players feed into it
- **Rules** — How inputs transform state (formalized in Skill 8)
- **Outputs** — What it produces for other systems or the player
- **Boundaries** — Where this system ends and another begins

### System Interaction Types

**Direct interaction** — System A explicitly modifies System B's state.
- "Killing an enemy (Combat) drops gold (Economy)"
- "Spending resources (Economy) unlocks abilities (Progression)"

**Indirect interaction** — System A changes conditions that affect System B's behavior.
- "Weather (Environment) reduces visibility, which changes Combat outcomes"
- "Player reputation (Social) affects shop prices (Economy)"

**Emergent interaction** — Systems A and B interact in ways the designer didn't explicitly create.
- Players discover that combining poison (Combat) with life steal (Progression) creates an invincibility loop
- Resource trading between players (Economy) becomes a kingmaking tool (Social)

## Core Deliverables

### 1. Systems Interaction Diagram

Map all systems as nodes and all interactions as edges:

```
SYSTEM A ──[interaction type]──→ SYSTEM B

Interaction types:
  ──→  Direct influence (A changes B's state)
  ···→  Indirect influence (A changes conditions B operates in)
  ←──→  Bidirectional (A and B affect each other)
  ──X→  Gated (A affects B only when condition is met)
```

**Example diagram (text representation):**
```
                    ┌──────────┐
                    │ COMBAT   │
                    └──┬───┬───┘
            drops loot │   │ costs ammo
                       v   v
┌──────────┐     ┌──────────┐     ┌──────────────┐
│ CRAFTING │←────│ ECONOMY  │────→│ PROGRESSION  │
└──────────┘     └──────────┘     └──────┬───────┘
  produces gear       │           unlocks abilities
       │              │                  │
       └──────────────┼──────────────────┘
                      │
              feeds back to COMBAT
```

For each edge, document:
```
FROM:        [Source system]
TO:          [Target system]
INTERACTION: [What specifically happens]
DIRECTION:   [One-way / Bidirectional / Conditional]
STRENGTH:    [How much does this interaction matter? Critical / Significant / Minor]
FREQUENCY:   [How often does this interaction fire? Every turn / Situational / Rare]
```

### 2. Feedback Loop Inventory

Feedback loops are the engine of emergent gameplay — and the source of most balance disasters.

**Reinforcing loops** (positive feedback) — Success breeds more success.
```
Win fight → Get better gear → Win harder fights → Get even better gear
```
- **Healthy when:** They accelerate toward a satisfying conclusion
- **Dangerous when:** They create runaway leaders or "rich get richer" spirals
- **Control mechanisms:** Catch-up mechanics, diminishing returns, risk escalation

**Balancing loops** (negative feedback) — Success creates new challenges.
```
Expand territory → More borders to defend → Harder to hold → Contraction pressure
```
- **Healthy when:** They create natural oscillation and tension
- **Dangerous when:** They prevent any progress (treadmill feeling)
- **Control mechanisms:** Threshold-based triggers, player agency in loop engagement

**Broken loops** — Feedback that should exist but doesn't.
```
Player accumulates power → Nothing challenges that power → Boredom
```
- **Symptom:** A system's output has no consequences
- **Fix:** Connect the output to a balancing system

**Loop documentation format:**
```
LOOP NAME:    [Descriptive name]
TYPE:         [Reinforcing / Balancing / Broken]
SYSTEMS:      [Which systems participate]
CYCLE:        [Step-by-step: A → B → C → A]
SPEED:        [How quickly does the loop complete one cycle?]
STRENGTH:     [How powerful is the effect per cycle?]
INTENDED?:    [Was this designed or discovered?]
HEALTH:       [Healthy / Needs monitoring / Dangerous]
CONTROL:      [What mechanism prevents this loop from dominating?]
```

### 3. Emergence Potential Map

Emergence is the holy grail of systems design — when the *combination* of systems produces experiences the designer didn't explicitly create.

**Positive emergence** (desired):
- Players discover creative strategies by combining systems
- Unexpected but fair interactions create memorable moments
- "Speedrunning" techniques that use systems in novel ways
- Emergent narrative from system interactions

**Negative emergence** (exploits):
- Dominant strategies that bypass intended gameplay
- Infinite resource loops
- Griefing vectors in multiplayer
- Sequence breaks that skip intended content

**For each system pair, assess:**
```
SYSTEMS:           [System A] x [System B]
INTERACTION SPACE: [What happens when these systems interact?]
POSITIVE EMERGENCE:[What cool things could players discover?]
NEGATIVE EMERGENCE:[What exploits or degenerate strategies could exist?]
RISK LEVEL:        [Low / Medium / High]
MONITORING PLAN:   [How will we detect if this goes wrong?]
```

### 4. Degenerate Strategy Warnings

A degenerate strategy is any approach that:
- Bypasses the intended core loop
- Is clearly optimal, eliminating meaningful choice
- Is unfun to execute but necessary to compete
- Exploits a system interaction the designer didn't intend

**Detection method — the "if I were trying to break this game" exercise:**
1. For each system output, ask: "What if I maximize this to the exclusion of everything else?"
2. For each system pair, ask: "What if I exploit this interaction as aggressively as possible?"
3. For each resource, ask: "What if I hoard this? What if I dump this immediately?"
4. For multiplayer: "What if I cooperate/defect when the game expects the opposite?"

**Warning format:**
```
STRATEGY:     [Description of the degenerate approach]
SYSTEMS:      [Which systems does it exploit?]
WHY IT WORKS: [What rule or interaction makes this viable?]
IMPACT:       [How does this affect the experience? Who suffers?]
FIX OPTIONS:  [Possible design responses, with trade-offs]
```

### 5. Coupling Analysis

Systems can be too tightly or too loosely coupled.

**Too tight** — Changing one system requires changing several others. Symptoms:
- Balance changes cascade unpredictably
- Can't tune one system without breaking another
- New content requires updates across many systems
- Bug in one system corrupts others

**Too loose** — Systems don't interact enough. Symptoms:
- Game feels like several mini-games stapled together
- Player can ignore entire systems without consequence
- No emergent behaviors
- No interesting trade-offs between systems

**Coupling assessment format:**
```
SYSTEM PAIR     COUPLING    ASSESSMENT
──────────────  ──────────  ──────────────────────────────────
Combat-Economy  Tight       Intentional — loot drives engagement
Combat-Crafting Loose       Problem — crafting feels disconnected
Economy-Social  Medium      Healthy — trading creates optional depth
```

**Ideal coupling:** Most systems should be loosely coupled with 2-3 tight coupling relationships that create the game's core tension. A system tightly coupled to everything is a maintenance nightmare. A system coupled to nothing is scope creep.

## Interaction Mapping Techniques

### Influence Matrix

For quick analysis, build an N x N matrix of all systems:

```
             Combat  Economy  Craft  Progress  Social
Combat         --    Strong   Weak   Medium    Weak
Economy      Medium    --     Strong  Strong   Medium
Crafting     Strong  Medium    --     Weak     None
Progression  Strong  Medium   Medium   --      Weak
Social       Weak    Strong   None    None      --
```

Read rows as "how much does this system AFFECT others."
Read columns as "how much is this system AFFECTED BY others."

**Flags:**
- A row of all "None/Weak" = isolated system (why does it exist?)
- A column of all "Strong" = bottleneck system (fragile, high-impact)
- Asymmetric pairs = potential for runaway feedback

### Event Flow Tracing

For complex interactions, trace a single player action through all affected systems:

```
EVENT: Player kills a boss enemy
  → Combat: Boss defeated state, XP awarded
    → Progression: Level check, ability unlock triggered
      → Combat: New ability available in combat
  → Economy: Rare loot dropped
    → Inventory: Loot stored, capacity check
      → Economy: If full, auto-sell triggers, gold awarded
        → Crafting: Gold available for crafting
  → Narrative: Boss death triggers story beat
    → World: Area state changes (zone cleared)
      → Social: Achievement shared with party
```

This reveals the actual cascade of a single action and helps identify unexpected chains.

## Workflow

### Mapping systems for a new game

1. **List all systems** — Every distinct domain of game state
2. **Define boundaries** — Where does each system start and end?
3. **Map direct interactions** — What does each system explicitly send to and receive from others?
4. **Identify indirect interactions** — What conditions does each system create that affect others?
5. **Build the influence matrix** — Quick assessment of interaction strength
6. **Draw the interaction diagram** — Visual map of all connections
7. **Inventory feedback loops** — Classify each as reinforcing, balancing, or broken
8. **Assess emergence potential** — For high-interaction pairs, brainstorm positive and negative emergence
9. **Hunt degenerate strategies** — "If I were trying to break this, how would I?"
10. **Analyze coupling** — Are systems appropriately connected?
11. **Cross-reference with core loop** (Skill 7) — Does the interaction map support the intended gameplay cycle?
12. **Flag risks to balance** (Skill 11) — Which interactions need balance testing?

### Adding a new system

1. Define the new system's state, inputs, rules, outputs, boundaries
2. Map all interactions with existing systems
3. Check for new feedback loops created
4. Assess emergence potential with each existing system
5. Check coupling — does the new system tighten or loosen the overall web?
6. Run degenerate strategy check specifically for the new system
7. Flag to Coherence Engine (Skill 0) for impact analysis

### Diagnosing unexpected behavior

1. Identify the unexpected behavior precisely
2. Trace the event flow — what chain of system interactions produces this?
3. Identify the specific interaction that's producing the unexpected result
4. Classify: Is this positive emergence (keep it) or a degenerate strategy (fix it)?
5. If fixing: Identify the minimum change that corrects the behavior without breaking healthy interactions
6. Run the fix through the influence matrix — what else does it affect?

## Outputs

This skill produces:
1. **Systems interaction diagram** — visual map of all systems and their connections
2. **Feedback loop inventory** — all reinforcing, balancing, and broken loops classified
3. **Emergence potential map** — positive and negative emergence for high-interaction pairs
4. **Degenerate strategy warnings** — exploit paths with fix options
5. **Coupling analysis** — assessment of system interdependence with health ratings
6. **Influence matrix** — quick-reference strength map of all system pairs

These outputs feed into:
- **Skill 8 (Rules)** — Interactions must be formalized as rules
- **Skill 10 (Economy)** — Economy is a key system in the web
- **Skill 11 (Balance)** — Feedback loops and interactions define balance targets
- **Skill 16 (Playtest)** — Emergence predictions need testing
- **Skill 17 (Iteration)** — System interaction changes need tracking
- **Skill 21 (Tech Bridge)** — System boundaries inform architecture
