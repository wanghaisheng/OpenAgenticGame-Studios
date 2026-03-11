---
name: design-coherence-engine
description: >
  Meta-skill that wraps the Game Design Skill Suite (21 skills, 8 tiers). Manages
  change propagation, coherence checking, priority arbitration, and adaptive flow
  between game design skills. Use this skill when: (1) starting a new game design
  project and determining which skills to activate, (2) a design change in one area
  may affect other areas, (3) checking whether all design elements are still aligned
  with vision and pillars, (4) resolving conflicts between competing design demands,
  (5) re-entering the design process after a playtest or discovery invalidates
  assumptions, (6) the designer wants to start from a non-standard entry point
  (e.g., starting from a mechanic idea rather than vision).
---

# Design Coherence Engine

The connective tissue of the Game Design Skill Suite. This skill does not produce game design artifacts directly — it manages the *process* of design across all other skills, ensuring coherence as things change.

## The Motorhead Principle

*"Everything louder than everything else."*

Every element of a game fights for primacy. Vision, aesthetics, mechanics, narrative, balance — all pull in different directions. This engine does not impose a fixed hierarchy. It helps the designer maintain a coherent center of gravity while everything shifts.

## Suite Topology

The suite uses a **gravity model, not a waterfall.** Tiers suggest natural starting points, but any skill can activate at any time.

```
Tier 0: META        → 0. Design Coherence Engine (this skill)
Tier 1: FOUNDATION  → 1. Game Vision Architect
Tier 2: IDENTITY    → 2. Design Pillars ←→ 19. Aesthetic Direction
Tier 3: INTENT      → 3. Player Experience, 4. Pitch
Tier 4: STRUCTURE   → 5. Core Loop, 6. Rules, 7. Systems, 8. Economy
Tier 5: CALIBRATION → 9. Balance
Tier 6: SUBSTANCE   → 10. Narrative, 11. Levels, 12. World Logic
Tier 7: PROOF       → 13. Prototype, 14. Playtest, 15. Iteration, 20. UI/UX
Tier 8: DELIVERY    → 16. GDD, 17. Scope, 18. Tech Bridge
```

For full skill definitions, inputs, outputs, and connections see [references/suite-topology.md](references/suite-topology.md).

## Core Operations

### 1. Determine Active Skill Set

Not every project needs all 21 skills. Determine which are relevant:

1. Assess project scale and medium (jam game, indie, AAA, tabletop, hybrid)
2. Identify which tiers are already addressed (designer may have existing vision)
3. Recommend the minimum active skill set for the current phase
4. Flag skills that are dormant but may activate later

**Example:**
- Game jam: Vision (1), Pillars (2), Loop (5), Prototype (13) — 4 skills
- Indie digital: All tiers active, Scope (17) and Tech Bridge (18) lightweight
- Tabletop: All tiers, Tech Bridge (18) focuses on component manufacturing
- AAA: All 21 skills at full depth

### 2. Check Coherence

Verify alignment across all active skills. Run when:
- A skill's outputs have changed
- The designer suspects drift
- Before major milestones (prototype, vertical slice, alpha, release)
- After any playtest round

Coherence check process:

1. **Anchor check** — Do all active skills still trace back to Vision (1)? Are Pillars (2) and Aesthetic (19) still mutually reinforcing?
2. **Vertical alignment** — For each active skill, do its outputs still serve the tier above it?
3. **Cross-tier alignment** — Do skills at the same tier agree with each other?
4. **Aesthetic-mechanic coherence** — Does the sensory identity (19) still match what the mechanics (5-9) produce? A mismatch here is the most common source of "the game feels wrong."
5. **Output coherence report** — For each misalignment: which skills are in tension, what specifically conflicts, and what the likely resolution paths are.

### 3. Propagate Change

When a design change occurs in any skill, determine what else is affected:

1. **Identify the changed skill and what specifically changed**
2. **Trace connections** — Using suite topology, identify every skill that takes the changed skill's outputs as inputs
3. **Assess impact severity:**
   - **Cosmetic** — Downstream skills need minor updates (e.g., renaming a resource)
   - **Structural** — Downstream skills need re-evaluation but core assumptions hold (e.g., adjusting a progression curve)
   - **Foundational** — Downstream assumptions are invalidated (e.g., changing the core fantasy)
4. **Generate re-evaluation queue** — Ordered list of skills to revisit, prioritized by impact severity and tier distance from the change
5. **Flag cascade risks** — Changes that could ripple beyond direct connections

**Example: Playtest reveals core loop isn't fun**

```
Change: Core Loop (5) — primary loop needs redesign
Impact: FOUNDATIONAL
Re-evaluation queue:
  1. Rules Formalizer (6) — rules express the loop, must change
  2. Economy (8) — reward structure tied to loop stages
  3. Systems Mapper (7) — system interactions may shift
  4. Balance (9) — new loop means new balance targets
  5. Levels (11) — encounters built around old loop pacing
  6. Prototype (13) — prototype must be rebuilt
  7. UI/UX (20) — interface surfaced the old loop
Cascade risk: If radical, check Experience (3) and Pillars (2)
```

**Example: Art style discovery changes aesthetic direction**

```
Change: Aesthetic Direction (19) — shifting from realistic to stylized
Impact: STRUCTURAL
Re-evaluation queue:
  1. Pillars (2) — does this aesthetic still reinforce pillars? (bidirectional check)
  2. Experience (3) — emotional targets may shift with new aesthetic
  3. Pitch (4) — communication artifacts need new mood/tone
  4. Levels (11) — visual pacing changes
  5. Prototype (13) — aesthetic fidelity targets shift
  6. UI/UX (20) — interface must fit new sensory identity
  7. Tech Bridge (18) — technical requirements change (shader complexity, etc.)
Cascade risk: If pillars change, everything downstream re-evaluates
```

### 4. Arbitrate Conflicts

When skills produce contradictory demands:

1. **Name the conflict precisely** — e.g., "Aesthetic wants minimalist UI, but Rules complexity requires dense information display"
2. **Check both sides against Pillars (2)** — Which pillar does each serve?
3. **Check against Vision (1)** — Which resolution better serves the core fantasy?
4. **If pillars conflict** — Refer to pillar priority ranking (from Skill 2)
5. **If still unresolved** — Surface the tension to the designer with clear trade-offs. Not every conflict has a clean resolution. Sometimes the answer is "change a pillar."
6. **Log the resolution** — Feed to Design Iteration Tracker (15)

### 5. Support Non-Standard Entry

The designer may not start at Vision. Support entry from any point:

**Starting from a mechanic idea:**
1. Document the mechanic
2. What experience does this create? (→ Skill 4)
3. What fantasy does that experience serve? (→ Skill 1)
4. What pillars does this imply? (→ Skill 2)
5. What aesthetic identity fits? (→ Skill 3)
6. Proceed forward through remaining tiers

**Starting from an aesthetic vision:**
1. Document the aesthetic
2. What fantasy does this evoke? (→ Skill 1)
3. What pillars support this? (→ Skill 2)
4. What experience should match? (→ Skill 4)
5. Proceed forward

**Starting from a playtest result:**
1. Document the finding
2. Identify which skill's assumptions are invalidated
3. Run change propagation (Operation 3)
4. Execute re-evaluation queue

**Starting from a market opportunity:**
1. Document the market gap
2. What player persona fills this gap? (→ Skill 1)
3. What core fantasy appeals to that persona? (→ Skill 1)
4. Proceed forward

## Operation Triggers

| Trigger | Operation |
|---------|-----------|
| New project started | 1. Determine Active Skill Set |
| Any skill output changed | 3. Propagate Change |
| Before milestone/review | 2. Check Coherence |
| Two skills disagree | 4. Arbitrate Conflicts |
| Designer starts mid-process | 5. Non-Standard Entry |
| Project scope changes | 1. Determine Active Skill Set (re-run) |
| After playtest round | 3. Propagate Change → 2. Check Coherence |
| "Something feels off" | 2. Check Coherence |

## Relationship to Skill 17 (Design Iteration Tracker)

| | Coherence Engine (0) | Iteration Tracker (15) |
|---|---|---|
| **Nature** | Active process | Passive record |
| **Question** | "What needs to change?" | "What already changed?" |
| **Timing** | Forward-looking | Backward-looking |
| **Output** | Re-evaluation queue, conflicts | Decision log, version history |
| **Analogy** | Air traffic controller | Flight recorder |

The Coherence Engine uses the Tracker's logs as input for pattern detection (e.g., "you've changed this pillar three times — is it the right pillar?").
