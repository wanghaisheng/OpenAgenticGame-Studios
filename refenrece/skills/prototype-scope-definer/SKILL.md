---
name: prototype-scope-definer
description: >
  Define the minimum buildable artifact that tests the core design hypothesis.
  Prevent over-building before validation. Use this skill when: (1) defining
  what a prototype must include to test the core hypothesis, (2) making
  build-vs-fake decisions (what must be real, what can be placeholder),
  (3) setting aesthetic fidelity targets for a prototype, (4) defining success
  criteria for prototype validation, (5) scoping a paper prototype, vertical
  slice, or greybox, (6) preventing scope creep during prototyping.
  Medium-agnostic — works for digital prototypes, tabletop paper prototypes,
  and hybrid builds.
---

# Prototype Scope Definer

The prototype exists to answer one question: "Does this work?" Everything in the prototype must serve that question. Everything that doesn't is scope creep.

## Prototype Philosophy

**Build the minimum artifact that tests your riskiest assumption.** Not the whole game. Not even a representative slice. Just enough to validate or invalidate the hypothesis that matters most right now.

### What a Prototype IS
- A test of a specific hypothesis
- Disposable — it can and often should be thrown away
- Focused on the core experience, not edge cases
- Good enough to generate real feedback

### What a Prototype IS NOT
- A demo (prototypes aren't for impressing people)
- The foundation of the final product (unless you're lucky)
- Complete (completeness is the enemy of speed)
- Polished (polish hides problems)

## Core Deliverables

### 1. Core Hypothesis Statement

Every prototype tests a hypothesis. State it clearly:

```
WE BELIEVE:         [The design assumption being tested]
WE WILL KNOW:       [What evidence would validate or invalidate this?]
WE WILL TEST BY:    [How the prototype creates conditions for this evidence]
SUCCESS LOOKS LIKE: [Specific, observable criteria]
FAILURE LOOKS LIKE: [Specific, observable criteria]
```

**Multiple hypotheses:** Rank risky assumptions. Test the riskiest first. Don't try to test everything at once.

### 2. Vertical Slice Definition

What's in and what's not:

```
ELEMENT              IN PROTOTYPE    FIDELITY       RATIONALE
──────────────────── ──────────────  ────────────── ──────────────────
[Game element]       [Yes/No/Fake]   [Placeholder/  [Why this decision?]
                                      Functional/
                                      Polished]
```

**Fidelity levels:**
- **Placeholder** — Grey boxes, index cards, borrowed art
- **Functional** — Works correctly but rough. Programmer art.
- **Polished** — Near-final quality. Only where fidelity affects the hypothesis.

**Decision framework:**
1. Directly affects the hypothesis? Must be functional.
2. Needs to exist for test to make sense? Can be placeholder.
3. Fidelity affects player behavior during test? Match threshold where behavior changes.
4. Everything else? Not in the prototype.

### 3. Build-vs-Fake Decisions

For each system in the game:

```
SYSTEM          BUILD?    FAKE HOW?                WHY?
──────────────  ──────── ──────────────────────── ──────────────────
Core loop       Real      N/A                      This IS the test
Combat          Real      Simplified rules          Core to hypothesis
Economy         Fake      Fixed handouts            Not testing this
Progression     Fake      Manual level-up           Not testing this
Narrative       Fake      Text cards/verbal         Not testing story
UI              Fake      Paper/whiteboard          Not testing usability
AI              Fake      Human-controlled          Quality not in scope
```

**Tabletop-specific fakes:** Index cards for printed cards, borrowed tokens, handwritten rules, verbal narration for flavor text.

**Digital-specific fakes:** Greybox environments, programmer art, hard-coded values, debug UI, no save system.

### 4. Aesthetic Fidelity Targets

How polished based on what you're testing:

```
TESTING FOR:              FIDELITY NEEDED:
──────────────────────── ──────────────────────────────
Core mechanic feel        Functional — must work correctly
Emotional response        Medium — enough atmosphere to evoke
Visual identity           High — testing art direction itself
Game feel (juice/weight)  High — feel IS fidelity
Social dynamics           Low — people create their own energy
Strategic depth           Low — ugly games reveal deep strategy
```

### 5. Success Criteria

Define before building, not after.

**Quantitative** (measurable): Completion rate, time-on-task, choice distribution, retry rate.

**Qualitative** (observable): Emotional reactions, unprompted comments, body language, social dynamics.

**Kill criteria** (hypothesis is dead if): 2-3 observations that conclusively invalidate the core assumption. Not "needs polish" but "the idea doesn't work."

## Prototype Types

**Paper Prototype** — Hours to build. Tests mechanics, decisions, turn structure. Works for any game, even digital.

**Digital Greybox** — Days to build. Tests spatial design, movement, timing. For games with spatial or real-time elements.

**Vertical Slice** — Weeks to build. Tests complete core experience near-final quality. For publisher/investor validation.

**Wizard of Oz** — Hours to build. Human simulates AI/procedural systems. Tests complex systems cheaply.

## Workflow

### Defining prototype scope

1. **List all risky assumptions** — What could be wrong about the design?
2. **Rank by risk** — Which assumption, if wrong, kills the project?
3. **Write the hypothesis** — Clear, testable, falsifiable
4. **Define the vertical slice** — In, out, faked
5. **Make build-vs-fake decisions** — For every system
6. **Set aesthetic fidelity targets** — Based on what's being tested
7. **Define success/failure criteria** — Before building, not after
8. **Estimate build time** — More than 2 weeks for first prototype? Scope down.
9. **Cross-check with core loop** (Skill 7) — Prototype must express the loop
10. **Cross-check with playtest protocol** (Skill 16) — How will this be tested?

### When the prototype fails

1. What specifically failed — hypothesis, execution, or test?
2. **Hypothesis failed:** Core assumption wrong. Revisit vision and pillars.
3. **Execution failed:** Prototype didn't test what it should. Rebuild.
4. **Test failed:** Conditions didn't generate useful data. Re-test.
5. Flag to Coherence Engine (Skill 0) for cascade analysis

## Outputs

This skill produces:
1. **Core hypothesis statement** — what the prototype tests
2. **Vertical slice definition** — what's included at what fidelity
3. **Build-vs-fake decision log** — every system categorized
4. **Aesthetic fidelity targets** — polish level per element
5. **Success/failure criteria** — observable metrics

These outputs feed into:
- **Skill 16 (Playtest)** — The prototype is what gets tested
- **Skill 7 (Core Loop)** — Prototype must express the loop
- **Skill 17 (Iteration)** — Results drive iteration
- **Skill 21 (Tech Bridge)** — Prototype has build requirements
- **Skill 3 (Aesthetic)** — Fidelity targets may need aesthetic decisions
