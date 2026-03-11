# Game Design Skill Suite — Topology Reference

## Connection Map

Each skill lists what it receives from (inputs) and what it feeds into (outputs).

### Tier 1: Foundation

**1. Game Vision Architect**
- Receives from: Designer's idea/inspiration
- Feeds into: 2 (Pillars), 3 (Aesthetic), 4 (Experience), 5 (Pitch)

### Tier 2: Identity (co-equal, bidirectional)

**2. Design Pillars Architect**
- Receives from: 1 (Vision)
- Feeds into: ALL downstream skills, 3 (Aesthetic — bidirectional)
- Bidirectional with: 3 (Aesthetic Direction)

**3. Aesthetic Direction Framework**
- Receives from: 1 (Vision), 2 (Pillars — bidirectional)
- Feeds into: 4 (Experience), 5 (Pitch), 7 (Loop — game feel), 12 (Narrative), 13 (Levels), 14 (World Logic), 15 (Prototype), 21 (Tech Bridge), 18 (UI/UX)
- Bidirectional with: 2 (Pillars)

### Tier 3: Intent

**4. Player Experience Modeler**
- Receives from: 1 (Vision), 2 (Pillars), 3 (Aesthetic)
- Feeds into: 7 (Loop), 10 (Economy), 12 (Narrative), 13 (Levels), 15 (Prototype), 16 (Playtest)

**5. High Concept & Elevator Pitch Writer**
- Receives from: 1 (Vision), 2 (Pillars), 3 (Aesthetic), 6 (Market — evidence strengthens pitch)
- Feeds into: 19 (GDD)

**6. Game Market Analyst**
- Receives from: 1 (Vision — core fantasy, personas, attention niche), 2 (Pillars), 3 (Aesthetic)
- Feeds into: 5 (Pitch — market evidence), 4 (Experience — audience expectations), 1 (Vision — market validation feedback), 20 (Scope — viability informs priorities), 10 (Economy — monetization shapes in-game economy), 19 (GDD — market positioning section)

### Tier 4: Structure

**7. Core Loop Designer**
- Receives from: 2 (Pillars), 4 (Experience), 3 (Aesthetic — game feel)
- Feeds into: 8 (Rules), 9 (Systems), 10 (Economy), 11 (Balance), 15 (Prototype), 18 (UI/UX)

**8. Rules Formalizer**
- Receives from: 7 (Loop), 9 (Systems)
- Feeds into: 11 (Balance), 14 (World Logic), 16 (Playtest), 21 (Tech Bridge), 18 (UI/UX)

**9. Systems Interaction Mapper**
- Receives from: 7 (Loop), 8 (Rules), 10 (Economy)
- Feeds into: 11 (Balance), 21 (Tech Bridge)

**10. Economy & Progression Designer**
- Receives from: 2 (Pillars), 4 (Experience), 7 (Loop)
- Feeds into: 9 (Systems), 11 (Balance), 21 (Tech Bridge)

### Tier 5: Calibration

**11. Game Balance Analyst**
- Receives from: 7 (Loop), 8 (Rules), 9 (Systems), 10 (Economy)
- Feeds into: 8 (Rules — balance changes become rule changes), 13 (Levels), 16 (Playtest), 17 (Iteration), 18 (UI/UX)

### Tier 6: Substance

**12. Narrative Systems Designer**
- Receives from: 2 (Pillars), 4 (Experience), 3 (Aesthetic)
- Feeds into: 13 (Levels), 14 (World Logic)

**13. Level/Encounter Blueprint Planner**
- Receives from: 2 (Pillars), 4 (Experience), 7 (Loop), 11 (Balance), 12 (Narrative), 3 (Aesthetic)
- Feeds into: 15 (Prototype)

**14. World Logic & Lore Consistency Checker**
- Receives from: 1 (Vision — core fantasy), 8 (Rules), 12 (Narrative), 3 (Aesthetic)
- Feeds into: 12 (Narrative — lore constrains narrative), 17 (Iteration)

### Tier 7: Proof

**15. Prototype Scope Definer**
- Receives from: 2 (Pillars), 7 (Loop), 13 (Levels), 3 (Aesthetic)
- Feeds into: 16 (Playtest), 21 (Tech Bridge)

**16. Playtest Protocol Designer**
- Receives from: 4 (Experience), 11 (Balance), 15 (Prototype)
- Feeds into: 0 (Coherence Engine — may trigger cascades), 17 (Iteration)

**17. Design Iteration Tracker**
- Receives from: ALL skills (any change is logged)
- Feeds into: 0 (Coherence Engine — pattern detection), 19 (GDD)

**18. UI/UX Systems Designer**
- Receives from: 4 (Experience), 7 (Loop), 8 (Rules), 11 (Balance), 3 (Aesthetic)
- Feeds into: 15 (Prototype), 21 (Tech Bridge)

### Tier 8: Delivery

**19. GDD Author**
- Receives from: ALL active skills
- Feeds into: 20 (Scope), 21 (Tech Bridge)

**20. Scope & Feature Prioritizer**
- Receives from: 2 (Pillars), 15 (Prototype), 19 (GDD), 21 (Tech Bridge)
- Feeds into: 15 (Prototype — what to test first)

**21. Technical Design Bridge**
- Receives from: 8 (Rules), 9 (Systems), 10 (Economy), 19 (GDD), 3 (Aesthetic), 18 (UI/UX)
- Feeds into: 20 (Scope — feasibility informs priority)

## Impact Severity Guide

When assessing how a change in one skill affects others:

### Foundational changes (re-evaluate everything downstream)
- Vision (1): Core fantasy, player persona, or market fit changes
- Pillars (2): A pillar is added, removed, or redefined
- Aesthetic (3): Sensory identity shifts fundamentally (e.g., realistic → stylized)
- Core Loop (7): Primary loop is redesigned

### Structural changes (re-evaluate direct connections)
- Experience (4): Emotional arc targets shift
- Market (6): Competitive landscape shifts, audience viability changes
- Rules (8): Rule additions/modifications
- Economy (10): Progression curve adjustments
- Balance (11): Balance lever changes
- Narrative (12): Delivery method changes

### Cosmetic changes (update but don't re-evaluate)
- Naming changes (factions, resources, abilities)
- Minor pacing adjustments
- Documentation formatting
- Asset swaps that maintain the same aesthetic intent

## Minimum Viable Skill Sets

| Project Type | Active Skills | Notes |
|---|---|---|
| Game jam (48h) | 1, 2, 7, 15 | Vision, Pillars, Loop, Prototype. Skip everything else. |
| Game jam (week) | 1, 2, 7, 8, 11, 15, 16 | Add Rules, Balance, Playtest. |
| Indie prototype | 1, 2, 3, 4, 7, 8, 10, 11, 15, 16, 17 | Full concept + structure + proof. Defer content & delivery. |
| Indie with publisher pitch | 1, 2, 3, 4, 5, 6, 7, 8, 10, 11, 15, 16, 17 | Add Pitch and Market for publisher conversations. |
| Tabletop prototype | 1, 2, 3, 4, 7, 8, 10, 11, 15, 16, 17, 18 | UI/UX critical early for tabletop (component layout). |
| Kickstarter tabletop | 1, 2, 3, 4, 5, 6, 7, 8, 10, 11, 15, 16, 17, 18 | Market + Pitch essential for campaign planning. |
| Full indie | All except possibly 14 (World Logic) | Scale 14 based on lore complexity. |
| AAA / large team | All 22 at full depth | All skills active, all tiers engaged. |
