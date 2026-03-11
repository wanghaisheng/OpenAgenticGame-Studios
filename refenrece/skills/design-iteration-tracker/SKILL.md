---
name: design-iteration-tracker
description: >
  Track what changed, why it changed, and what the result was. Prevent circular
  design and build institutional memory. Use this skill when: (1) logging design
  decisions with rationale and supporting data, (2) detecting when a proposed
  change moves back toward a previously rejected state, (3) tracking the impact
  chain of changes across systems, (4) maintaining version history of key design
  parameters, (5) building a searchable history of design evolution,
  (6) onboarding new team members who need to understand why things are the way
  they are. Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Design Iteration Tracker

Games are built through iteration. Every playtest changes something. Every insight reshapes the design. Without tracking, teams make the same mistakes twice, undo good changes, and lose the reasoning behind critical decisions. This skill is the project's design memory.

## Why Track Iterations?

**Prevent circular design** — "Let's try making combat faster." "We tried that in v3. Players felt rushed and couldn't read the board state. We slowed it back down in v4 for that reason."

**Preserve reasoning** — Six months from now, why is this value set to 7? Because it was 5 and players felt starved, then 10 and players felt flooded, then 7 which tested well.

**Enable informed decisions** — When proposing a change, know what's already been tried.

**Onboard new contributors** — New team members understand not just what the design IS but how it got there.

## Core Deliverables

### 1. Decision Log

The primary record. Every meaningful design change gets an entry:

```
DECISION ID:     [Unique identifier — e.g., DEC-042]
DATE:            [When]
CHANGE:          [What was changed, specifically]
FROM:            [Previous state/value]
TO:              [New state/value]
RATIONALE:       [Why this change was made]
DATA SOURCE:     [What evidence supported this? Playtest, intuition, data?]
AFFECTED SKILLS: [Which design areas are impacted?]
DECIDED BY:      [Who made the call?]
STATUS:          [Implemented / Pending / Reverted / Superseded]
```

**Quality rules for decision entries:**
- State the change precisely ("Increased starting health from 100 to 150" not "tweaked health")
- Always record the rationale, even if it's "designer intuition" — that's valid but should be explicit
- Link to playtest data when it exists (PT-007 found that players felt too fragile)
- Record who decided — for accountability and future consultation

### 2. Revert Warnings

The most valuable feature. Detects when a proposed change would move toward a previously rejected state:

```
WARNING: Proposed change [X] resembles reverted decision DEC-023.

DEC-023 attempted: [What was tried]
DEC-023 result:    [What happened — why it was reverted]
DEC-023 data:      [What evidence drove the revert]

PROCEED IF:  [Conditions that make this time different]
ABORT IF:    [Conditions that make this the same mistake]
```

**The "this time is different" check:**
1. Has the context changed? (New systems, different player base, different platform)
2. Is the proposed implementation different? (Same direction but different execution)
3. Was the original revert data-driven or intuition-driven?
4. Can we test this cheaply before committing?

### 3. Impact Chain Tracking

When a change cascades through the design:

```
CHANGE: [The initial change — e.g., DEC-042: Increased starting health to 150]

DIRECT IMPACTS:
  → Balance: All damage values may need rescaling
  → Economy: Health potion value changed relative to health pool
  → Encounters: Early encounter difficulty shifts

INDIRECT IMPACTS:
  → Progression: Health upgrades less impactful (smaller % gain)
  → Build diversity: Tanky builds less differentiated from baseline

MONITORED BUT NO ACTION YET:
  → Player experience: Does this change the emotional arc of early game?
```

### 4. Parameter Version History

For key design values, maintain a history:

```
PARAMETER: Starting Player Health
────────────────────────────────────────
v1 (initial):     100    [Designer estimate]
v2 (PT-003):      80     [Players felt too safe, reduced to add tension]
v3 (PT-005):      120    [80 was too punishing, overcorrected]
v4 (PT-007):      100    [Returned to baseline, problem was damage not health]
v5 (PT-009):      150    [Damage rebalanced, health increased for build diversity]
CURRENT:          150
```

This is invaluable for avoiding the "tuning treadmill" — adjusting the same value back and forth without progress.

### 5. Iteration Summary Reports

Periodic summaries of design evolution:

```
ITERATION PERIOD: [Date range or playtest range]
TOTAL CHANGES:    [Count]
MAJOR CHANGES:    [List the significant ones]
REVERTS:          [Any changes that were undone]
OPEN QUESTIONS:   [What remains unresolved?]
DESIGN DIRECTION: [How has the game's direction shifted?]
NEXT PRIORITIES:  [What should the next iteration focus on?]
```

## Tracking Methodology

### What to Track

**Always track:**
- Changes to core mechanics (rules, values, systems)
- Changes to pillars or vision (highest-impact changes)
- Playtest-driven changes (with linked playtest data)
- Reversions (why something was undone)

**Track when significant:**
- Content changes (new levels, encounters, characters)
- Balance adjustments (value tweaks with rationale)
- Aesthetic changes (art direction shifts, audio changes)

**Don't track:**
- Typo fixes and formatting
- Work-in-progress states (only track when a decision is made)
- Individual developer experiments that don't reach the shared design

### How to Categorize

**Change types:**
- **Addition** — New element added to the design
- **Removal** — Element cut from the design
- **Modification** — Existing element changed
- **Revert** — Previous change undone
- **Rebalance** — Quantitative adjustment to existing values
- **Restructure** — Organizational change (systems reorganized, not modified)

**Change drivers:**
- **Playtest data** — Observable evidence from testing
- **Player feedback** — Reported experience from testers
- **Designer insight** — Professional judgment
- **Technical constraint** — Implementation forced a change
- **Scope pressure** — Time/budget forced a cut
- **Market shift** — External factors changed priorities

## Anti-Patterns

**The Undocumented Change** — "Oh, I changed that last week." Nobody knows why. Nobody can evaluate the impact.

**The Amnesia Loop** — Trying the same failed approach every few months because nobody remembers why it was rejected.

**The Tracking Tax** — Documentation so onerous that designers stop updating it. Keep entries concise.

**The Justification Theater** — Writing rationale AFTER the change to justify it, not BEFORE to evaluate it.

**The Frozen Design** — Using the change log as a reason not to change things. "We already tried that" shouldn't end discussion if context has changed.

## Workflow

### Logging a design change

1. **Document current state** — What is it now?
2. **Document proposed change** — What will it become?
3. **State rationale** — Why this change?
4. **Check revert warnings** — Have we tried this before?
5. **Map impact chain** — What else is affected?
6. **Implement the change**
7. **Update parameter history** (if applicable)
8. **Flag affected skills to Coherence Engine** (Skill 0)

### Running an iteration review

1. Gather all changes since last review
2. Categorize by type and driver
3. Identify patterns (are we constantly adjusting the same thing?)
4. Check for circular changes (A→B→A patterns)
5. Assess overall design direction — is the game converging or diverging?
6. Set priorities for next iteration

## Outputs

This skill produces:
1. **Decision log** — every change with rationale, data, and impact
2. **Revert warnings** — detection of circular design patterns
3. **Impact chain tracking** — cascade effects of changes
4. **Parameter version history** — evolution of key design values
5. **Iteration summary reports** — periodic design evolution overview

These outputs feed into:
- **All skills** — Any design element can change
- **Skill 11 (Balance)** — Balance is the most iterated element
- **Skill 19 (GDD)** — GDD must reflect current state
- **Skill 0 (Coherence)** — Feeds the engine's change awareness
