---
name: level-encounter-planner
description: >
  Structure spaces and encounters to deliver on pillars and pacing. The craft of
  "what happens where and in what order." Use this skill when: (1) designing
  level layouts, encounter sequences, or scenario structures, (2) building
  pacing curves (tension/release patterns), (3) defining encounter composition
  (enemy mix, challenge types, resource pressure), (4) choosing spatial flow
  models (linear, hub-and-spoke, open, gated), (5) planning difficulty ramping
  across a game, (6) designing for replayability through encounter variation,
  (7) mapping narrative beats to specific encounters or locations. Medium-agnostic
  — works for digital levels, tabletop scenarios, and hybrid encounters.
---

# Level/Encounter Blueprint Planner

Levels and encounters are where design meets the player. Vision, pillars, loops, and narrative all converge into "what actually happens during play." This skill structures those moments.

## Level vs. Encounter

**Level** — A bounded play space with a beginning, progression, and conclusion. A dungeon. A mission. A board game scenario. A chapter.

**Encounter** — A discrete challenge or interaction within a level. A combat. A puzzle. A social negotiation. A skill check.

Levels contain encounters. Encounters express the core loop. The level's job is to *sequence* encounters to create pacing, variety, and emotional arc.

## Spatial Flow Models

How the player moves through a level:

### Linear
```
A → B → C → D → E
```
Player progresses through a fixed sequence.
- **Strengths:** Easy to pace, clear narrative progression, no disorientation
- **Weaknesses:** Low exploration reward, predictable, no player choice in routing
- **Best for:** Narrative-driven levels, tutorial sequences, competitive maps
- **Examples:** Call of Duty campaigns, Pandemic Legacy scenarios, linear dungeon crawls

### Branching
```
A → B → {C or D} → E → {F or G} → H
```
Player chooses between paths at decision points.
- **Strengths:** Player agency, replay variety, strategic route planning
- **Weaknesses:** Balance across paths, content some players never see
- **Best for:** Roguelikes, heist missions, story-choice games
- **Examples:** Slay the Spire map, Betrayal at House on the Hill exploration

### Hub-and-Spoke
```
    ┌→ B ─┐
A → HUB ─┼→ C ─┼→ HUB → FINALE
    └→ D ─┘
```
Central area with radiating paths the player can tackle in any order.
- **Strengths:** Player freedom, natural pacing (self-directed), clear orientation
- **Weaknesses:** Hub can feel repetitive, difficulty in non-linear areas varies
- **Best for:** Exploration games, RPG towns, Metroidvanias
- **Examples:** Zelda dungeons, Hades hub, Clue mansion

### Open/Sandbox
```
┌─────────────┐
│ A  B  C  D  │
│ E  F  G  H  │
│ I  J  K  L  │
└─────────────┘
```
Player can go anywhere, encounter anything.
- **Strengths:** Maximum freedom, emergent discovery, high replayability
- **Weaknesses:** Hard to pace, disorientation risk, difficulty to balance encounters
- **Best for:** Open worlds, sandbox games, exploration-first designs
- **Examples:** Breath of the Wild, Minecraft, sandbox tabletop RPG sessions

### Gated
```
A → B → [GATE: requires key] → C → D → [GATE: requires boss kill] → E
```
Linear or open with progression gates that require specific conditions.
- **Strengths:** Controlled progression, mastery verification, dramatic pacing
- **Weaknesses:** Can feel artificial, backtracking frustration, key-hunt tedium
- **Best for:** Metroidvanias, campaign games, tiered content
- **Examples:** Metroid, Gloomhaven scenario unlocks, tech-tree-gated content

## Core Deliverables

### 1. Pacing Curve

The tension/release pattern across a level or session:

```
INTENSITY
    5 │                    ╱╲
    4 │              ╱╲   ╱  ╲    ╱╲
    3 │         ╱╲  ╱  ╲ ╱    ╲  ╱  ╲
    2 │    ╱╲  ╱  ╲╱    ╳      ╲╱    ╲
    1 │╱╲ ╱  ╲╱                        ╲
    0 └──────────────────────────────────
      START                          END

      ↑intro  ↑build  ↑peak  ↑climax  ↑resolution
```

**Pacing principles:**
- **Rising baseline** — Each peak should be slightly higher than the last
- **Valleys matter** — Rest moments after peaks let the player process and anticipate
- **The final peak should be the highest** — Don't put the best encounter in the middle
- **Variety in peaks** — Not every peak should be the same type (combat, puzzle, narrative)
- **Opening hook** — Start with a small peak to establish tone, not a slow tutorial

**Pacing template per encounter:**
```
ENCOUNTER #    TYPE          INTENSITY   DURATION    PURPOSE
──────────────  ──────────── ──────────  ──────────  ──────────────────
1              [type]        [1-5]       [minutes]   [Why is this here?]
2              [type]        [1-5]       [minutes]   [Why is this here?]
...
```

### 2. Encounter Composition Templates

Define the building blocks of encounters:

```
ENCOUNTER TYPE:    [Name — e.g., "Ambush", "Puzzle Gate", "Resource Trove"]
CHALLENGE TYPE:    [Combat / Puzzle / Social / Exploration / Survival / Hybrid]
DIFFICULTY:        [1-5 scale relative to player's expected capability]
DURATION:          [Expected time to complete]
RESOURCE PRESSURE: [What resources does this encounter cost the player?]
REWARD:            [What does the player gain?]
PLAYER COUNT:      [Solo / Small group / Full party / Scalable]
FAILURE STATE:     [What happens if the player fails? Retry? Consequence? Bypass?]
PILLAR SERVED:     [Which design pillars does this encounter deliver?]
```

**Encounter variety checklist:**
- [ ] Challenge types vary (not all combat, not all puzzles)
- [ ] Resource pressure varies (some encounters drain, some replenish)
- [ ] Decision density varies (some encounters are action-heavy, some are decision-heavy)
- [ ] Optional encounters exist (for exploration-motivated players)
- [ ] At least one encounter per level showcases a unique or memorable moment

### 3. Difficulty Ramping Plan

How challenge escalates across the full game:

```
SEGMENT          DIFFICULTY    NEW ELEMENTS INTRODUCED    PLAYER CAPABILITY
──────────────── ──────────── ──────────────────────────  ──────────────────
Tutorial         1/5          Core mechanics only          Baseline
Early game       2/5          First system combinations    Learning
Mid game         3/5          Full system depth            Competent
Late game        4/5          Mastery-required encounters  Skilled
Endgame/Bonus    5/5          Creative challenge           Expert
```

**Difficulty sources** (not just "enemies hit harder"):
- **Mechanical complexity** — More systems active simultaneously
- **Time pressure** — Less time to think and react
- **Resource scarcity** — Less margin for error in resource spending
- **Information scarcity** — Less knowledge about what's coming
- **Combination challenge** — Requiring multiple skills/systems at once
- **Opponent intelligence** — Smarter/more aggressive AI or scenario design
- **Stakes escalation** — Higher consequences for failure

### 4. Replayability Design

How encounters stay fresh across multiple playthroughs:

**Procedural variation:**
- Randomized enemy placement / encounter composition
- Modular level segments that recombine
- Random events or modifiers per encounter
- Tabletop: shuffled event decks, random map tiles

**Player-driven variation:**
- Different builds/characters experience encounters differently
- Multiple viable strategies per encounter
- Optional objectives that change approach
- Tabletop: different player count, different character combinations

**Structural variation:**
- Branching paths ensure different encounters per playthrough
- Difficulty modifiers (challenge runs, hard mode, scenario difficulty)
- Meta-progression that changes available options
- Tabletop: scenario variants, legacy changes, expansion content

### 5. Level Blueprint Template

Complete blueprint for a single level/scenario:

```
LEVEL NAME:        [Name]
LEVEL TYPE:        [Main path / Side content / Optional / Bonus]
SPATIAL FLOW:      [Linear / Branching / Hub / Open / Gated]
DURATION TARGET:   [Expected play time]
DIFFICULTY BAND:   [Where in the difficulty curve]
NARRATIVE ROLE:    [What story does this level tell?]
EMOTIONAL ARC:     [What should the player feel at start, middle, end?]

ENCOUNTER SEQUENCE:
  1. [Encounter — type, intensity, duration, purpose]
  2. [Encounter — type, intensity, duration, purpose]
  3. [Encounter — type, intensity, duration, purpose]
  ...

RESOURCE ECONOMY:
  Starting resources: [What the player enters with]
  Resources available: [What can be found/earned in-level]
  Resources consumed: [Expected expenditure]
  Net result: [Player should exit with more/less/same as entry?]

KEY MOMENTS:
  [The 1-3 moments that make this level memorable]

AESTHETIC NOTES:
  Visual: [How should this level look?]
  Audio: [How should this level sound?]
  Feel: [What's the kinesthetic/tactile mood?]
```

## Workflow

### Designing levels/encounters for a new game

1. **Reference the core loop** (Skill 7) — Encounters are instances of the loop
2. **Reference the experience model** (Skill 4) — Levels deliver the emotional arc
3. **Reference the narrative structure** (Skill 12) — Where do story beats land?
4. **Choose spatial flow model** — What movement pattern serves the game?
5. **Build the pacing curve** — Map tension/release across the level
6. **Define encounter types** — What are the building blocks?
7. **Compose encounter sequences** — Arrange encounters to serve the pacing curve
8. **Plan difficulty ramping** — How does challenge escalate?
9. **Design replayability** — How do encounters stay fresh?
10. **Cross-check with aesthetic direction** (Skill 3) — Visual/audio pacing per encounter
11. **Cross-check with balance** (Skill 11) — Are encounters appropriately challenging?
12. **Blueprint specific levels** — Full documentation per level

### Evaluating an existing level

1. Play through and note where engagement rises, falls, or stalls
2. Map the actual pacing curve — does it match the intended curve?
3. Check encounter variety — are there enough different types?
4. Check difficulty curve — does it ramp appropriately?
5. Check resource economy — does the player exit in the intended state?
6. Check narrative delivery — do story beats land at the right moments?
7. Identify the memorable moment — every level needs at least one

## Outputs

This skill produces:
1. **Pacing curves** — tension/release patterns per level and per session
2. **Encounter composition templates** — reusable building blocks
3. **Difficulty ramping plan** — challenge escalation across the full game
4. **Replayability design** — variation mechanisms
5. **Level blueprints** — complete documentation per level/scenario

These outputs feed into:
- **Skill 11 (Balance)** — Encounter difficulty needs balancing
- **Skill 12 (Narrative)** — Encounters deliver story beats
- **Skill 15 (Prototype)** — Which levels to prototype first
- **Skill 16 (Playtest)** — Levels are what's being playtested
- **Skill 3 (Aesthetic)** — Visual/audio pacing per encounter
- **Skill 19 (GDD)** — Level designs are a core GDD section
