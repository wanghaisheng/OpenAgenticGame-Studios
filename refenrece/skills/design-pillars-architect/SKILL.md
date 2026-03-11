---
name: design-pillars-architect
description: >
  Distill a game vision into 3-5 actionable design pillars that constrain and guide
  every design decision. Pillars are the filter — if a feature doesn't serve a
  pillar, it gets cut. Use this skill when: (1) a game vision exists but needs
  translating into actionable constraints, (2) the team needs a shared framework for
  evaluating design decisions, (3) feature creep threatens and the project needs
  refocusing, (4) aesthetic direction challenges require pillar re-evaluation
  (bidirectional with Skill 3), (5) a pillar is suspected of no longer serving the
  vision. Co-equal with Aesthetic Direction (Skill 3) at Tier 2. Medium-agnostic.
---

# Design Pillars Architect

Design pillars are the 3-5 non-negotiable commitments that define what this game IS. Everything designed, built, or cut is measured against them. They are not goals ("make it fun") — they are constraints ("every decision point must involve incomplete information").

## What Makes a Good Pillar

A pillar is strong when it:
- **Constrains** — It says "no" to things. A pillar that everything passes is not a pillar.
- **Differentiates** — It distinguishes this game from other games. "High quality" is not a pillar.
- **Is testable** — You can look at a feature and definitively say whether it serves this pillar.
- **Creates tension** — The best pillars are slightly at odds with each other, forcing creative solutions.
- **Is memorable** — A team member can recall all pillars without looking them up.

A pillar is weak when it:
- Applies to all games ("be fun", "engage the player")
- Is a feature masquerading as a pillar ("multiplayer co-op")
- Is too vague to test against ("immersive")
- Never conflicts with anything (too safe)

## Pillar Definition Format

For each pillar, define:

```
PILLAR NAME: [2-4 word name, memorable and evocative]
Statement: [One sentence defining the pillar]
This means: [2-3 concrete implications for design decisions]
This doesn't mean: [2-3 common misinterpretations to prevent drift]
Test: [How to evaluate whether a feature/decision serves this pillar]
Priority: [Rank among other pillars — when this pillar conflicts with another, who wins?]
```

**Example:**

```
PILLAR: Earned Mastery
Statement: Every skill in the game is learnable through practice, never through stats alone.
This means:
  - Player skill, not character level, determines success in challenges
  - Difficulty comes from reading situations, not from number inflation
  - A new player who is skilled can outperform a veteran who is careless
This doesn't mean:
  - No progression systems (progression unlocks options, not power)
  - No difficulty scaling (scaling changes complexity, not stat walls)
  - Players can't fail (failure is the teacher)
Test: Remove all character progression from a challenge. Is it still
  possible to succeed through player skill alone? If yes, pillar served.
Priority: 2 of 4 (yields to "Meaningful Consequence", ties with "Readable Chaos")
```

## Workflow

### Establishing pillars for a new project

1. **Gather vision outputs** — Core fantasy, player persona(s), attention niche from Skill 1
2. **Extract candidate pillars** — From the vision, what are the non-negotiable qualities? What must be true for the core fantasy to work?
3. **Stress-test candidates:**
   - Does this pillar say "no" to something concrete?
   - Could a game exist in this genre without this pillar? (If not, it's genre default, not a pillar)
   - Do any two pillars create productive tension?
4. **Narrow to 3-5** — More than 5 and nothing is prioritized. Fewer than 3 and the design is under-constrained.
5. **Rank by priority** — When two pillars conflict, which wins? This ranking is a design decision, not a quality judgment.
6. **Cross-check with Aesthetic Direction (Skill 3)** — Do the pillars and the aesthetic identity reinforce each other? If Aesthetic says "minimalist and serene" and a pillar says "chaotic emergent behavior," surface the tension.
7. **Define validation tests** — For each pillar, how will you know it's being served during development?

### Revising pillars

Pillars are not sacred. They can change. But changing a pillar has the highest impact of any design change — it cascades to everything.

1. Identify what's driving the revision (playtest data, aesthetic shift, market shift, team insight)
2. Propose the pillar change specifically (add, remove, modify, re-rank)
3. Run impact analysis: What downstream skills are affected?
4. If adding a pillar: Does the total stay at 5 or fewer? What tension does it create with existing pillars?
5. If removing a pillar: What decisions were made on the basis of this pillar? Do they still hold?
6. If re-ranking: What conflicts were previously resolved in this pillar's favor? Do those resolutions flip?
7. Flag to Coherence Engine (Skill 0) for change propagation

### Using pillars to evaluate a feature

1. For each pillar, ask: "Does this feature serve this pillar?"
2. Score: Serves (+), Neutral (0), Conflicts (-)
3. Any feature that conflicts with a pillar needs justification or cutting
4. Features that serve no pillar are scope creep — cut or defer
5. Features that serve multiple pillars are high-priority

## Pillar Anti-Patterns

**The Wishlist** — 8+ pillars that are really a feature list. Narrow to the 3-5 that constrain.

**The Motherhood** — Pillars so universally agreeable they constrain nothing. "Engaging gameplay" passes every game ever made.

**The Straitjacket** — Pillars so narrow that creative solutions are impossible. Pillars constrain the *what*, not the *how*.

**The Ghost Pillar** — A pillar that was established early and never referenced again. If it's not being used to evaluate decisions, it's not a real pillar.

**The Sacred Cow** — A pillar that the team treats as untouchable even when evidence suggests it's wrong. Pillars serve the vision. If the vision evolves, the pillar must be re-evaluated.

## Bidirectional Relationship with Aesthetic Direction (Skill 3)

Pillars and Aesthetic Direction sit at the same tier and inform each other:

- A pillar like "Readable Chaos" demands an aesthetic that makes complex states visually parseable
- An aesthetic commitment to "hand-crafted warmth" might reshape a pillar about procedural generation
- When they conflict, neither automatically wins — surface the tension and resolve against Vision (Skill 1)

Always cross-reference when either skill's outputs change.

## Outputs

This skill produces:
1. **3-5 named, defined pillars** — each with statement, implications, anti-patterns, and test
2. **Pillar priority ranking** — the tiebreaker when pillars conflict
3. **Pillar validation tests** — how to verify each pillar is being served

These outputs feed into every downstream skill. They are the primary filter for Scope & Feature Prioritizer (Skill 20) and the reference point for Coherence Engine (Skill 0) checks.
