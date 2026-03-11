---
name: technical-design-bridge
description: >
  Translate game design into implementation requirements without prescribing
  engineering solutions. The bridge between "what the designer wants" and "what
  gets built." Use this skill when: (1) translating formalized rules into
  systems specifications, (2) identifying data structure requirements from game
  state, (3) flagging performance-critical systems, (4) assessing platform
  constraints and their design impact, (5) defining aesthetic implementation
  requirements (shader complexity, audio channels, print specs), (6) creating
  component design specs for tabletop manufacturing. Medium-agnostic — works
  for digital engines, tabletop manufacturing, and hybrid platforms.
---

# Technical Design Bridge

The designer says "what." The engineer says "how." The bridge translates between them without either overstepping. A designer shouldn't prescribe code architecture. An engineer shouldn't override design intent. This skill defines the handoff.

## Bridge Philosophy

**Describe the WHAT, not the HOW.** "The combat system must resolve 4-player simultaneous actions within 100ms" is a design requirement. "Use a thread pool with lock-free queues" is an engineering decision.

**Flag constraints, don't solve them.** "This system requires tracking 10,000+ entities with real-time collision" is a flag. The solution is engineering's domain.

**Respect both directions.** Technical constraints are real and reshape design. If the platform can't handle the designer's vision, the design must adapt — but that's a conversation, not a unilateral cut.

## Core Deliverables

### 1. Systems Specification

For each game system, translate from design to implementation requirements:

```
SYSTEM:           [Name]
PURPOSE:          [What this system does in the game — from design perspective]
STATE:            [All variables this system tracks]
  - [Variable]: [Type, range, persistence, visibility]
INPUTS:           [What feeds into this system — player actions, other systems]
OPERATIONS:       [What transformations the system performs]
OUTPUTS:          [What this system produces — state changes, events, feedback]
PERFORMANCE:      [Real-time? Turn-based? Latency tolerance?]
PERSISTENCE:      [What must be saved? Session? Across sessions? Cloud?]
DEPENDENCIES:     [What other systems must exist for this to function?]
```

**Example:**
```
SYSTEM:           Character Mutation System
PURPOSE:          Manages random power assignment and mutation interactions
STATE:
  - active_mutations: List of MutationID, max 5, persisted per character
  - mutation_energy: Float 0-100, regenerates at 2/sec, session-only
  - catalyst_shard: ItemID reference, persisted
INPUTS:
  - Player activates mutation (player input)
  - Shard equipped/unequipped (inventory system)
  - Damage received (combat system — some mutations trigger on damage)
OPERATIONS:
  - Random mutation assignment on character creation (weighted tables)
  - Mutation activation (check energy, apply effect, start cooldown)
  - Mutation interaction check (when 2+ mutations combine)
OUTPUTS:
  - Visual effect trigger (to rendering)
  - Stat modification events (to combat/movement)
  - Audio trigger (to audio system)
PERFORMANCE:       Real-time, mutation activation must resolve in < 1 frame
PERSISTENCE:       Mutations persist across sessions. Energy resets per session.
DEPENDENCIES:      Combat system, inventory system, character system
```

### 2. Data Structure Requirements

What state the game needs to track:

```
DATA DOMAIN         ENTITIES         VOLUME          UPDATE FREQUENCY
──────────────────  ──────────────── ──────────────  ──────────────────
Player state        Characters       1-4 per session  Real-time
World state         Map tiles        1000-5000        Per event
Economy             Resources        10-20 types      Per transaction
Combat              Active effects   0-50 per entity  Per frame
Progression         Unlock flags     100-500          Per milestone
```

**Data relationship mapping:**
- One-to-one (player ↔ character)
- One-to-many (character ↔ mutations)
- Many-to-many (characters ↔ factions)
- Hierarchical (world → zone → area → tile)

### 3. Performance-Critical Flags

Systems that have hard performance requirements:

```
SYSTEM              REQUIREMENT                          PRIORITY
──────────────────  ──────────────────────────────────── ────────────
[System]            [Specific performance constraint]     [Critical/
                                                          Important/
                                                          Nice-to-have]
```

**Common performance-critical areas:**
- **Input response** — Player action to visual feedback (< 100ms for action games)
- **Physics/collision** — Real-time spatial calculations
- **AI decision-making** — NPC behavior resolution per frame
- **Network synchronization** — Multiplayer state consistency
- **Rendering** — Visual complexity vs. framerate
- **Audio mixing** — Simultaneous sound channels
- **Save/load** — Serialization speed and data size

### 4. Platform Constraints Impact

How target platform shapes design:

**Digital platforms:**
```
CONSTRAINT              DESIGN IMPACT                    ADAPTATION
──────────────────────  ──────────────────────────────── ──────────────────
Input method            [Controller? Touch? M+K?]        [How it affects UI]
Screen size             [Mobile? Monitor? TV?]           [How it affects layout]
Processing power        [Mobile? Console? PC?]           [What's feasible]
Storage                 [Download size limits?]          [Content budget]
Network                 [Online required? Optional?]     [Offline capability]
Session context         [Couch? Commute? Desktop?]       [Session length design]
```

**Tabletop constraints:**
```
CONSTRAINT              DESIGN IMPACT                    ADAPTATION
──────────────────────  ──────────────────────────────── ──────────────────
Component count         [Manufacturing cost per unit]     [Minimize unique pieces]
Card size               [Standard sizes cost less]        [Use standard sizes]
Print process           [Color count, finish options]     [Design within print]
Box size                [Shelf presence vs. shipping]     [Optimize footprint]
Setup time              [Player patience threshold]       [Minimize pieces]
Table footprint         [Available play space]            [Fit standard tables]
```

### 5. Aesthetic Implementation Requirements

Technical requirements driven by aesthetic direction (Skill 3):

**Digital:**
```
AESTHETIC CHOICE        TECHNICAL REQUIREMENT            COST
──────────────────────  ──────────────────────────────── ──────────────
[Visual style]          [Shader complexity, render path]  [GPU budget]
[Animation style]       [Bone count, blend trees]         [Memory/CPU]
[Audio design]          [Channels, reverb, spatialization][Audio budget]
[VFX approach]          [Particle systems, post-process]  [GPU budget]
[Lighting model]        [Dynamic? Baked? Hybrid?]         [Build time + GPU]
```

**Tabletop:**
```
AESTHETIC CHOICE        MANUFACTURING REQUIREMENT        COST
──────────────────────  ──────────────────────────────── ──────────────
[Card art style]        [Print DPI, bleed, color profile] [Per-unit]
[Miniatures]            [Material, detail level, molds]   [Tooling + unit]
[Board material]        [Foldable? Mounted? Neoprene?]    [Per-unit]
[Token material]        [Cardboard? Wood? Acrylic?]       [Per-unit]
[Box design]            [Insert design, shrink wrap]       [Per-unit]
```

### 6. Component Design Spec (Tabletop)

For tabletop games, the technical bridge includes physical component specification:

```
COMPONENT        QUANTITY    SIZE            MATERIAL        NOTES
──────────────── ──────────  ──────────────  ──────────────  ──────────────
Cards            [Count]     [Standard size] [Card stock]    [Finish, sleeve]
Tokens           [Count]     [Dimensions]    [Material]      [Shape, color]
Board            [Count]     [Folded size]   [Material]      [Fold count]
Dice             [Count]     [Size]          [Material]      [Custom faces?]
Rulebook         [Pages]     [Size]          [Paper weight]  [Binding]
Box              [1]         [Dimensions]    [Material]      [Insert type]
```

## Workflow

### Creating a tech bridge document

1. **List all game systems** from rules (Skill 8) and systems map (Skill 9)
2. **Write system specifications** — State, inputs, operations, outputs
3. **Map data requirements** — What state is tracked, how much, how fast
4. **Flag performance-critical systems** — What has hard timing requirements?
5. **Assess platform constraints** — How does target platform shape feasibility?
6. **Document aesthetic requirements** — What does the art/audio direction cost technically?
7. **Create component spec** (tabletop) — Physical manufacturing requirements
8. **Cross-check with scope** (Skill 20) — Does the technical scope match the feature scope?
9. **Review with engineering** — Does this accurately represent the design intent?

### Responding to "we can't build that"

1. Understand the constraint precisely — what specifically is infeasible?
2. Assess design impact — how does this constraint affect the player experience?
3. Propose design alternatives that preserve intent within constraints
4. Evaluate trade-offs with the design team
5. Update affected skills (loop, balance, systems) if the design changes
6. Flag to Coherence Engine (Skill 0) for impact analysis

## Outputs

This skill produces:
1. **Systems specifications** — per-system WHAT documentation for engineering
2. **Data structure requirements** — state tracking needs
3. **Performance-critical flags** — hard requirements per system
4. **Platform constraint analysis** — how platform shapes design
5. **Aesthetic implementation requirements** — technical cost of art/audio direction
6. **Component design spec** — physical manufacturing requirements (tabletop)

These outputs feed into:
- **Skill 8 (Rules)** — Rules become implementation specs
- **Skill 10 (Economy)** — Economy needs data infrastructure
- **Skill 20 (Scope)** — Feasibility informs priority
- **Skill 3 (Aesthetic)** — Aesthetic has technical cost
- **Skill 18 (UI/UX)** — Interface has implementation requirements
- **Skill 19 (GDD)** — Technical requirements are a GDD section
