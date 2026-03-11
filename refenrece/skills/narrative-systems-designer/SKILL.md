---
name: narrative-systems-designer
description: >
  Design the systems that deliver narrative — not the story itself, but the
  machinery of storytelling in the game. Use this skill when: (1) choosing
  between narrative delivery methods (linear, branching, emergent, environmental,
  systemic), (2) designing how story and mechanics interact and reinforce each
  other, (3) building quest/mission/scenario structures, (4) defining player
  agency within the narrative, (5) integrating faction and character systems
  with gameplay, (6) ensuring narrative serves the emotional arc defined in the
  experience model, (7) designing lore delivery that doesn't interrupt gameplay.
  Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Narrative Systems Designer

This skill designs the *machinery* of storytelling, not the story itself. How does narrative reach the player? Where does gameplay affect story and story affect gameplay? The best game narratives aren't told *to* the player — they happen *through* the player.

## Narrative Delivery Methods

Every game must choose how story reaches the player. These are not mutually exclusive — most games combine several.

### Linear Narrative
Story unfolds in a fixed sequence regardless of player action.
- **Strengths:** Tight authorial control, high emotional precision, efficient production
- **Weaknesses:** Low replay value, player is audience not participant, ludonarrative dissonance risk
- **Best for:** Short experiences, narrative-first games, tabletop scenario campaigns
- **Examples:** The Last of Us, Pandemic Legacy scenarios, most JRPG main plots

### Branching Narrative
Player choices create divergent story paths.
- **Strengths:** Player agency, replay value, consequence-driven engagement
- **Weaknesses:** Exponential content cost, "branch and prune" often feels fake, hard to maintain quality across all paths
- **Best for:** Story-driven RPGs, choice-based adventures, campaigns with lasting consequences
- **Examples:** Disco Elysium, Choose Your Own Adventure books, Gloomhaven retirement paths

**Branching management:**
```
BRANCHING SCOPE:        [How many major branch points?]
BRANCH DEPTH:           [How far do consequences cascade?]
CONVERGENCE:            [Do branches reunite? Where? How naturally?]
CONTENT BUDGET:         [What % of content will any single player see?]
MEANINGFUL VS COSMETIC: [Which choices change plot vs. change flavor?]
```

### Emergent Narrative
Story arises from system interactions, not authored content.
- **Strengths:** Infinite replayability, personal stories, "you won't believe what happened" moments
- **Weaknesses:** No emotional guarantee, stories can be incoherent, requires robust systems
- **Best for:** Sandbox games, simulation games, systemic games with expressive mechanics
- **Examples:** Dwarf Fortress, Rimworld, Betrayal at House on the Hill

### Environmental Narrative
Story embedded in the world itself — discoverable, not delivered.
- **Strengths:** Doesn't interrupt gameplay, rewards curiosity, builds atmosphere
- **Weaknesses:** Easy to miss, hard to tell complex stories, requires strong world-building
- **Best for:** Exploration games, atmospheric games, secondary lore in any genre
- **Examples:** Dark Souls item descriptions, Gone Home, Mysterium's vision cards

### Systemic Narrative
Game systems are designed to create story-like patterns through play.
- **Strengths:** Story and gameplay are one thing, highly replayable, player-authored
- **Weaknesses:** Hard to design, narratives may lack coherence, requires player imagination
- **Best for:** Roguelikes, sandbox, social deduction, tabletop RPGs
- **Examples:** Crusader Kings dynasties, Fiasco's story structure, The Quiet Year

## Core Deliverables

### 1. Narrative Delivery Architecture

Define which methods the game uses and where:

```
NARRATIVE LAYER    METHOD          CONTENT TYPE         FREQUENCY
────────────────── ──────────────  ──────────────────── ─────────────
Main story         [Method]        [What kind of story?] [How often?]
Side content       [Method]        [What kind?]          [How often?]
World-building     [Method]        [What kind?]          [How often?]
Character arcs     [Method]        [What kind?]          [How often?]
Player story       [Method]        [What kind?]          [How often?]
```

### 2. Story-Mechanic Integration Points

The most important deliverable. Where does narrative affect gameplay and vice versa?

**Mechanic to Narrative** (gameplay creates story):
```
MECHANIC:       [What the player does mechanically]
NARRATIVE:      [What story moment this creates]
INTEGRATION:    [How tightly are they connected?]
EXAMPLE:        [Specific instance]
```

**Narrative to Mechanic** (story changes gameplay):
```
STORY BEAT:     [What happens in the narrative]
MECHANICAL:     [How gameplay changes as a result]
INTEGRATION:    [Is this a permanent change or temporary?]
EXAMPLE:        [Specific instance]
```

**Integration quality spectrum:**
- **Dissonant** — Story says one thing, mechanics say another (bad)
- **Parallel** — Story and mechanics coexist but don't interact (missed opportunity)
- **Complementary** — Story and mechanics reinforce the same feeling (good)
- **Unified** — Story and mechanics are indistinguishable (ideal)

### 3. Quest/Mission/Scenario Structure

Define the templates for narrative content:

**Quest anatomy:**
```
QUEST NAME:      [Identifier]
HOOK:            [How does the player discover this quest?]
OBJECTIVE:       [What must the player do? Clear and testable]
MECHANICAL CORE: [What gameplay does this quest use?]
NARRATIVE CORE:  [What story does this quest tell?]
COMPLICATIONS:   [What makes it non-trivial?]
RESOLUTION:      [How does it end? Multiple endings?]
REWARD:          [Mechanical reward + narrative reward]
CONNECTIONS:     [What other quests/systems does this connect to?]
```

**Quest types:**
- **Critical path** — Must complete to progress. Should showcase core mechanics.
- **Side content** — Optional. Should explore secondary themes or systems.
- **Discovery** — Found through exploration. Should reward curiosity.
- **Emergent** — Arises from system interactions. Should feel personal.
- **Recurring** — Repeatable with variation. Should remain engaging.

### 4. Player Agency Model

Define what the player can change in the narrative and what they can't:

```
AGENCY LEVEL     WHAT PLAYER CONTROLS           WHAT'S FIXED
──────────────── ────────────────────────────── ──────────────────────
Full agency      Player determines outcome       Nothing
Guided agency    Player chooses path              Endpoints converge
Expressive       Player chooses how/style         What happens is fixed
Reactive         Player responds to events        Events are scripted
Witness          Player observes                  Everything
```

**For each narrative layer, define the agency level.**

**Agency anti-patterns:**
- **Fake agency** — "Choose A or B" but both lead to the same outcome. Players notice.
- **Consequence-free choice** — Decisions that don't matter mechanically or narratively
- **Invisible agency** — Player's actions affect the story but they can't tell
- **Paralyzing agency** — Too many options with unclear consequences

### 5. Character/Faction System Design

If the game has characters or factions:

```
ENTITY:              [Character/Faction name]
ROLE:                [Narrative function — protagonist, antagonist, ally, wildcard]
MECHANICAL ROLE:     [Gameplay function — quest giver, enemy type, faction benefit]
ARC:                 [How does this entity change over the game?]
PLAYER RELATIONSHIP: [How does the player interact with them?]
AGENCY:              [Can the player affect this entity's fate?]
```

**Faction system design considerations:**
- **Reputation mechanics** — How does player behavior affect standing?
- **Faction interactions** — How do factions relate to each other?
- **Mechanical incentives** — What does faction alignment give the player?
- **Narrative consequences** — What story changes based on faction standing?
- **Faction identity** — What makes each faction feel distinct in aesthetics, values, and gameplay?

## Narrative Anti-Patterns

**The Info Dump** — Walls of text that stop gameplay. If the player can skip it without losing the ability to play, the narrative system has failed.

**The Cutscene Hostage** — Taking control from the player to deliver story. Powerful when rare, exhausting when frequent.

**The Lore Encyclopedia** — Massive codex entries that nobody reads. Environmental or systemic narrative delivers the same lore more effectively.

**The Irrelevant Choice** — "Choose your dialogue option!" but nothing changes. Worse than no choice at all.

**The Narrative Island** — Story segments completely disconnected from gameplay. The story could be removed without affecting the game experience.

## Workflow

### Designing narrative systems for a new game

1. **Start with the core fantasy** (Skill 1) — What role does the player play in the story?
2. **Reference the experience model** (Skill 4) — What emotional beats does narrative need to hit?
3. **Choose delivery methods** — Which methods serve this game's pillars and loop?
4. **Map story-mechanic integration** — Where do story and gameplay touch?
5. **Design quest/scenario templates** — What's the repeatable structure?
6. **Define player agency** — What can players change? What's fixed?
7. **Build character/faction systems** (if applicable)
8. **Cross-check with aesthetic direction** (Skill 3) — How does the sensory layer deliver narrative?
9. **Cross-check with pillars** (Skill 2) — Does the narrative system serve the pillars?
10. **Plan content pipeline** — How much narrative content is needed? What's the production cost?
11. **Flag to world logic** (Skill 14) — Narrative must be consistent with world rules

### Diagnosing narrative problems

1. **"Story is boring"** — Check emotional arc alignment with Skill 4
2. **"Ludonarrative dissonance"** — Check story-mechanic integration map for contradictions
3. **"Choices don't matter"** — Check player agency model for fake agency
4. **"Too much exposition"** — Shift delivery methods from linear to environmental/systemic
5. **"I don't know why I'm doing this"** — Check quest hooks for clear motivation before objectives

## Outputs

This skill produces:
1. **Narrative delivery architecture** — which methods, where, at what frequency
2. **Story-mechanic integration map** — every point where story and gameplay connect
3. **Quest/scenario templates** — repeatable structures for narrative content
4. **Player agency model** — what the player controls vs. what's fixed
5. **Character/faction system design** — how NPCs and factions function mechanically and narratively

These outputs feed into:
- **Skill 13 (Levels)** — Narrative beats map to encounter design
- **Skill 14 (World Logic)** — Narrative must be lore-consistent
- **Skill 4 (Experience)** — Narrative delivers the emotional arc
- **Skill 19 (GDD)** — Narrative systems are a core GDD section
- **Skill 16 (Playtest)** — Narrative impact needs testing
