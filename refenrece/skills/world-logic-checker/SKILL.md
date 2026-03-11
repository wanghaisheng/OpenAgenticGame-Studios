---
name: world-logic-checker
description: >
  Keep the fiction internally consistent as the game scales. The rules of the
  world, not the rules of the game. Use this skill when: (1) establishing the
  foundational rules of a game's fictional world, (2) checking new content for
  lore contradictions, (3) tracking implications of world-building decisions
  ("if X is true, then Y must also be true"), (4) building faction/entity
  relationship maps, (5) defining technology or magic system constraints,
  (6) ensuring narrative content is consistent with established lore,
  (7) maintaining a living world bible that scales with the project.
  Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# World Logic & Lore Consistency Checker

The world has rules. Not game rules — *world* rules. Physics. Magic systems. Social structures. Technology levels. If the world contradicts itself, immersion shatters regardless of how good the mechanics are. This skill maintains the fiction's internal logic.

## World Logic vs. Game Rules

**Game rules** (Skill 8) define what the player can do mechanically: "Roll 2d6 + modifier to attack."

**World logic** defines what's true in the fiction: "Magic requires a physical conduit. No conduit, no magic. This is why mages carry staffs and wizards are powerless in chains."

Game rules can bend world logic for gameplay reasons (a healing potion works instantly because waiting 6 weeks for a broken bone isn't fun), but every bend should be conscious and documented, not accidental.

## Core Deliverables

### 1. World Rules Document

The foundational rules of the fictional world. Not the lore — the *logic*. What's possible, what's impossible, and what's rare.

**Structure:**
```
DOMAIN:          [Physics / Magic / Technology / Biology / Society / Economy / Other]
RULE:            [Statement of what's true in this world]
IMPLICATIONS:    [What else must be true if this rule is true?]
EXCEPTIONS:      [What known exceptions exist, and why?]
GAME IMPACT:     [How does this world rule affect gameplay?]
SOURCE:          [Where was this established? Vision doc, narrative, etc.]
```

**Example:**
```
DOMAIN:       Magic
RULE:         All mutation powers require physical contact with a Catalyst Shard.
IMPLICATIONS: - Powers can be "turned off" by separating the survivor from their shard
              - Shards are a targetable vulnerability
              - New powers require finding new shards
              - A black market for shards would exist
EXCEPTIONS:   - "Fused" characters have absorbed their shard (permanent but visible)
GAME IMPACT:  - Shard as inventory item creates risk/reward decisions
              - Enemy types that steal/destroy shards
              - Crafting system around shard combinations
SOURCE:       Vision doc v2, Core Fantasy statement
```

**World rule categories to address:**
- **Physical laws** — Does gravity work normally? Is there faster-than-light travel? Can the dead return?
- **Power systems** — How does magic/technology/mutation work? What are its limits? What's the cost?
- **Social structures** — How is society organized? What are the power dynamics? Who has authority?
- **Economic reality** — What's scarce? What's abundant? What drives trade?
- **Information rules** — What is known? What is secret? How does information travel?
- **Historical constraints** — What happened before the game begins that shapes the present?

### 2. Faction/Entity Relationship Map

How the major forces in the world relate to each other:

```
ENTITY A          RELATIONSHIP        ENTITY B          STABILITY
──────────────── ──────────────────── ──────────────── ──────────────
[Faction/Power]  [Allied/Hostile/     [Faction/Power]  [Stable/Tense/
                  Neutral/Trading/                      Shifting/
                  Vassal/Rival]                         Volatile]
```

For each entity, define:
```
ENTITY:          [Name]
TYPE:            [Faction / Government / Species / Corporation / Cult / Other]
MOTIVATION:      [What do they want? What drives their actions?]
RESOURCES:       [What do they control? Territory, technology, people, knowledge]
CONSTRAINTS:     [What limits them? Weakness, ideology, geography, numbers]
PLAYER RELATION: [How does the player interact with them? Can this change?]
WORLD ROLE:      [What function do they serve in the world's ecology?]
```

**Relationship health checks:**
- Does every faction have at least one ally and one rival?
- Does every conflict have a logical cause rooted in world rules?
- Are alliances and hostilities consistent with faction motivations?
- Do power dynamics create interesting tensions, not just good vs. evil?

### 3. Technology/Magic System Constraints

Power systems need rules or they become plot holes. Define the boundaries:

```
POWER SYSTEM:    [Name — e.g., "Mutation Powers", "Nanotech", "The Weave"]
SOURCE:          [Where does the power come from?]
COST:            [What does using it cost? Energy, health, sanity, materials?]
LIMITS:          [What can it NOT do? Hard boundaries.]
SCALING:         [How does power grow? Is there an upper limit?]
SIDE EFFECTS:    [What unintended consequences exist?]
SOCIAL IMPACT:   [How does this power affect society? Who fears it? Who wants it?]
INTERACTION:     [How does this system interact with other power systems?]
```

**Constraint quality check:**
- [ ] Every power has a cost (no free magic)
- [ ] Every power has a limit (no omnipotence)
- [ ] The constraints create interesting design space (limits breed creativity)
- [ ] The constraints are consistently applied across all game content
- [ ] NPCs and enemies follow the same constraints as players (or exceptions are explained)

### 4. Contradiction Detection

As the game grows, contradictions creep in. Build a system to catch them.

**Contradiction types:**
- **Direct contradiction** — "Elves are immortal" vs. "The ancient elf graveyard"
- **Implication contradiction** — "Magic requires rare crystals" but "every peasant uses magic daily"
- **Scale contradiction** — "The kingdom has 200 soldiers" but "the army that attacked had 10,000"
- **Timeline contradiction** — "The war ended 50 years ago" but "the veteran who fought in it is 30"
- **Tonal contradiction** — "This is a gritty, realistic world" but "there's a comic relief goblin merchant"

**Contradiction check format:**
```
CONTENT:         [New content being checked]
CLAIMS:          [What does this content assert about the world?]
CONFLICTS WITH:  [What established world rules does it potentially violate?]
SEVERITY:        [Breaking / Significant / Minor / Tonal]
RESOLUTION:      [Retcon? Rewrite content? Add exception to world rule? Intentional?]
```

**Proactive contradiction prevention:**
When adding new content, run each world-claim through existing rules:
1. List all assertions the new content makes about the world
2. For each assertion, check: Does any existing world rule contradict this?
3. For each assertion, check: Does any implication of this assertion contradict something?
4. If contradiction found: Is it a content error or a world rule that needs updating?

### 5. Implication Tracking

The most powerful world-building tool. If X is true, what else must be true?

```
ESTABLISHED FACT:    [Something true in the world]
FIRST-ORDER:         [Direct implications — what must be true because of this?]
SECOND-ORDER:        [Implications of the implications]
DESIGN OPPORTUNITIES:[What gameplay or narrative opportunities do these create?]
UNADDRESSED:         [Implications that exist but the game doesn't explore yet]
```

**Example:**
```
ESTABLISHED FACT:    Mutation powers are random and uncontrollable
FIRST-ORDER:         - Society fears mutants (can't predict what they'll do)
                     - No organized mutant military (can't train standardized units)
                     - Black market for specific mutations (high demand, random supply)
SECOND-ORDER:        - Underground mutant communities (safety in numbers)
                     - Anti-mutant political movements
                     - Religious interpretations (blessing? curse? divine lottery?)
DESIGN OPPORTUNITIES:- Faction quest lines (pro-mutant vs. anti-mutant)
                     - Black market economy system
                     - Social stealth (hiding your mutation)
UNADDRESSED:         - What happens to mutant children? (potentially dark, may skip)
                     - Do mutations breed true? (genetic implications)
```

## Workflow

### Building world logic for a new game

1. **Start with the core fantasy** (Skill 1) — What world makes this fantasy possible?
2. **Define power systems first** — Magic, technology, mutations — whatever the game's central power. Constrain it.
3. **Establish physical laws** — What's normal and what's different?
4. **Build faction/entity map** — Who exists? What do they want? How do they relate?
5. **Run implication chains** — For each major world rule, trace implications 2-3 levels deep
6. **Cross-check with aesthetic direction** (Skill 3) — Does the world's logic support the intended feel?
7. **Cross-check with narrative** (Skill 12) — Does the story respect world rules?
8. **Document everything** — The world bible is a living document

### Checking new content

1. List all world-claims in the new content
2. Run contradiction detection against existing world rules
3. Run implication check — does this content create new implications?
4. Check faction consistency — does this content affect faction relationships logically?
5. Check power system consistency — do abilities/items follow established constraints?
6. If contradictions found: resolve and document the resolution
7. If new implications found: add them to the implication tracking

### Scaling the world bible

As the game grows, the world bible grows. Keep it manageable:
- **Index by domain** — Physical, magical, social, economic, historical
- **Tag by certainty** — Established (in-game), Planned (for future content), Flexible (can change)
- **Version track** — When world rules change, mark the old version and why it changed
- **Link to content** — Every world rule should reference where it's expressed in-game

## Anti-Patterns

**The Soft Magic Excuse** — "It's magic, it doesn't need rules." Soft magic is fine for narrative mystery. But game mechanics need hard rules even if the fiction presents them as soft.

**The Retcon Cascade** — Changing one world rule and not tracing the implications. Every change cascades.

**The Forgotten Implication** — "Teleportation exists" but the game never addresses why armies march instead of teleporting. Players notice.

**The Lore Dump** — A 50-page world bible that nobody references during actual design. World logic should be a living tool, not a document.

**The Rule of Cool Exception** — "This contradicts the world rules but it's awesome so we'll keep it." Fine if rare and conscious. Destructive if habitual.

## Outputs

This skill produces:
1. **World rules document** — foundational logic per domain with implications
2. **Faction/entity relationship map** — all major forces and their interactions
3. **Power system constraints** — source, cost, limits, scaling, side effects
4. **Contradiction flags** — detected inconsistencies with severity and resolution
5. **Implication tracking** — cascading consequences of world-building decisions

These outputs feed into:
- **Skill 12 (Narrative)** — Narrative must respect world rules
- **Skill 8 (Rules)** — World logic can affect game rules
- **Skill 13 (Levels)** — Environments must be world-consistent
- **Skill 17 (Iteration)** — Lore changes need tracking
- **Skill 19 (GDD)** — World bible is a core GDD section
