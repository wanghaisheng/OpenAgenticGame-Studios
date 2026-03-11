---
name: rules-formalizer
description: >
  Write game rules with mathematical precision — unambiguous, complete,
  edge-case-aware. For tabletop, this IS the game. For digital, this is the
  systems specification. Use this skill when: (1) translating a core loop and
  mechanics concepts into precise rule definitions, (2) writing a tabletop
  rulebook or digital systems spec, (3) identifying and resolving edge cases
  and rule conflicts, (4) building a glossary of game terms with precise
  definitions, (5) evaluating whether rules as written match rules as intended,
  (6) creating rule dependency graphs to understand which rules reference which.
  Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Rules Formalizer

Rules are the contract between the game and the player. Ambiguous rules create arguments at the table and bugs in code. This skill turns design intent into precise, testable definitions.

## Rules as State Machines

Every game rule is a state machine, whether the designer thinks of it that way or not. Formalizing rules means making the state machine explicit.

### Rule Anatomy

Every rule has four components:

```
PRECONDITION:  What must be true for this rule to apply?
TRIGGER:       What event activates this rule?
RESOLUTION:    What happens when the rule fires?
POSTCONDITION: What state is the game in after resolution?
```

**Example — Attack Rule:**
```
PRECONDITION:  Active player has a character with Action Points > 0.
               Target is within range of equipped weapon.
               Line of sight exists between attacker and target.
TRIGGER:       Player declares attack action and selects target.
RESOLUTION:    Roll 2d6 + Attack Modifier.
               If result >= target's Defense Value: hit. Apply weapon damage.
               If result < target's Defense Value: miss. No effect.
               Reduce attacker's Action Points by 1.
POSTCONDITION: Target's HP is updated (if hit).
               Attacker's Action Points are reduced.
               Turn continues if Action Points remain.
```

**Weak rule (ambiguous):**
"Players can attack nearby enemies to deal damage."
- What is "nearby"? How much damage? Can they always attack? What resolves the attempt?

### Rule Types

**Constitutional rules** — Define the game itself. Cannot be broken by gameplay.
- "The game ends when one player reaches 10 Victory Points"
- "A player's hand cannot exceed 7 cards at end of turn"

**Operational rules** — Define how play proceeds. The sequence of actions.
- "On your turn, draw a card, then take up to 2 actions, then discard down to hand limit"
- "Movement costs 1 AP per tile traversed"

**Behavioral rules** — Define what entities in the game can do.
- "Rogues may spend 2 AP to become Hidden until they attack"
- "Buildings produce 1 resource per turn of their matching type"

**Conditional rules** — Define exceptions and special cases.
- "If both players reach 10 VP on the same turn, the defender wins ties"
- "Poisoned characters take 1 damage at the start of their turn and cannot heal"

**Meta-rules** — Rules about rules. Resolve ambiguity.
- "When two rules conflict, the more specific rule takes precedence"
- "Card text overrides rulebook text"

## Core Deliverables

### 1. Formal Rule Definitions

For each rule in the game, produce a formal definition:

```
RULE ID:       [Unique identifier, e.g., COMBAT-001]
RULE NAME:     [Human-readable name]
TYPE:          [Constitutional / Operational / Behavioral / Conditional / Meta]
PRECONDITION:  [What must be true]
TRIGGER:       [What activates this rule]
RESOLUTION:    [Step-by-step, no ambiguity]
POSTCONDITION: [What state results]
REFERENCES:    [Other rules this rule depends on or modifies]
EDGE CASES:    [Known edge cases and their resolution]
```

**Precision checklist for each rule:**
- [ ] Every noun is defined in the glossary
- [ ] Every verb has a single interpretation
- [ ] All quantities are explicit (no "some" or "several")
- [ ] Timing is unambiguous (before/after/instead of/during)
- [ ] Simultaneous effects have a resolution order
- [ ] The rule can be implemented in code or enforced at a table without judgment calls

### 2. Edge Case Catalog

Edge cases are where rules break. Identify them proactively.

**Systematic edge case discovery:**
- **Simultaneity** — What if two things happen at the same time?
- **Boundary values** — What if a value hits 0? Goes negative? Overflows?
- **Circular dependencies** — Does rule A trigger rule B which triggers rule A?
- **Resource exhaustion** — What if the deck runs out? The supply is empty?
- **Player elimination** — What if a player is removed? Do their effects persist?
- **Stacking** — Can multiple instances of the same effect apply? How do they combine?
- **Timing windows** — Can a player respond during another player's action?
- **Missing targets** — What if a target becomes invalid mid-resolution?
- **Voluntary vs. mandatory** — Can the player choose not to resolve an effect?

**Edge case format:**
```
EDGE CASE:      [Scenario description]
RULES INVOLVED: [Which rules collide?]
RESOLUTION:     [How is it resolved?]
PRINCIPLE:      [What general principle does this resolution establish?]
```

### 3. Rule Dependency Graph

Map which rules reference, modify, or depend on other rules:

```
RULE                  DEPENDS ON           MODIFIES          OVERRIDDEN BY
────────────────────  ──────────────────── ────────────────── ──────────────────
COMBAT-001 (Attack)   MOVE-003 (Range)     HP-001 (Health)    STEALTH-002 (Hidden)
                      EQUIP-001 (Weapons)  AP-001 (Actions)   SHIELD-001 (Block)
```

**Dependency analysis flags:**
- **Orphan rules** — Rules that nothing references. Are they actually used?
- **Circular dependencies** — A references B references A. Needs resolution order.
- **Deep chains** — Rule A triggers B triggers C triggers D. Too many steps = confusion.
- **Bottleneck rules** — Rules that everything depends on. If this changes, everything changes.

### 4. Glossary of Game Terms

Every game needs a precise glossary. Every term used in rules must appear here.

**Format:**
```
TERM:        [The word or phrase]
DEFINITION:  [Precise, unambiguous meaning in this game's context]
NOT:         [What it doesn't mean, if commonly confused]
FIRST USED:  [Which rule first introduces this term]
```

**Glossary quality rules:**
- No circular definitions ("Attack: when you perform an attack action")
- No undefined terms in definitions (every word in a definition is either a glossary term or a common English word)
- No synonyms without explicit declaration ("damage" and "harm" mean the same thing? State it.)
- Consistent terminology throughout all rules (don't call it "Health" in one rule and "Hit Points" in another unless the glossary declares them equivalent)

### 5. Player-Facing Rule Text

For tabletop: The actual rulebook text. For digital: The in-game help text and tutorial script.

**Rulebook structure (tabletop):**
1. **Overview** — What is this game? (1 paragraph, derived from Skill 5 pitch)
2. **Components** — What's in the box? (with visual references)
3. **Setup** — How to prepare for play (step-by-step with illustrations)
4. **Turn structure** — What happens on a turn (the operational rules)
5. **Actions** — What can a player do? (behavioral rules, usually the longest section)
6. **Special rules** — Conditional rules, exceptions, edge cases
7. **End of game** — How the game ends and who wins (constitutional rules)
8. **Quick reference** — Summary card / player aid content
9. **Glossary** — All game terms defined
10. **FAQ / Edge cases** — Common questions answered

**Systems spec structure (digital):**
1. **System overview** — Purpose and boundaries of this system
2. **State definitions** — All variables and their valid ranges
3. **Operations** — All operations the system performs, with inputs and outputs
4. **Event handling** — What events this system listens for and emits
5. **Edge cases** — Boundary conditions and their handling
6. **Dependencies** — What other systems this interacts with

## Rule Writing Principles

**Precision over elegance.** A rule that's ugly but unambiguous beats a rule that's beautifully written but has three interpretations.

**Atomic rules.** Each rule should do one thing. "On your turn, draw a card and then take an action" is two rules ("draw a card" and "take an action") in one sentence. They should be separable because edge cases will need to address them independently.

**Explicit defaults.** "Unless otherwise stated, all effects are resolved immediately." Don't make the player guess the default.

**Exception hierarchy.** When exceptions exist, define the precedence: Specific beats general. Card text beats rulebook. Later effects beat earlier effects. State these meta-rules clearly.

**Active voice, second person.** "You draw a card" not "A card is drawn by the active player." Rules should feel like instructions, not legal text.

## Workflow

### Formalizing rules for a new game

1. **Start with the core loop** (Skill 7) — The loop defines the primary rule sequence
2. **List all game actions** — Everything a player can choose to do
3. **List all game responses** — Everything the game does in response
4. **Write formal definitions** — Precondition, trigger, resolution, postcondition for each
5. **Build the glossary** — Define every term as you go
6. **Map dependencies** — Which rules reference which?
7. **Systematically hunt edge cases** — Run through the edge case discovery checklist
8. **Resolve edge cases** — Establish principles, not just patches
9. **Write player-facing text** — Translate formal definitions into readable rules
10. **Cross-check with pillars** (Skill 2) — Do the rules create the experience the pillars promise?
11. **Flag to balance** (Skill 11) — Are all quantitative values flagged for balance testing?

### Auditing existing rules

1. Identify the complaint: ambiguity? Inconsistency? Missing edge case?
2. Find the formal definition of the rule in question
3. Check each component: Is the precondition complete? Is the trigger unambiguous? Is the resolution step-by-step?
4. Check the glossary: Are all terms in the rule defined?
5. Check dependencies: Does this rule interact with others in unexpected ways?
6. Run edge case discovery on the specific rule
7. Propose fix and assess impact on dependent rules

### Writing rules for playtesting vs. publishing

**Playtest rules** can be:
- Informal and abbreviated
- Accompanied by verbal explanation
- Incomplete (leave known gaps for the facilitator to resolve)
- Focused on what testers need to play, not on edge cases

**Published rules** must be:
- Complete and self-contained
- Unambiguous to someone with no verbal explanation
- Edge-case-resolved
- Tested by blind playtest (someone who never heard of the game plays from the rules alone)

## Anti-Patterns

**The Novel** — Rules so long and detailed that no one reads them. Brevity serves clarity.

**The FAQ-Dependent Ruleset** — Rules that require a 20-page FAQ to actually play. The FAQ should clarify rare edges, not patch fundamental ambiguity.

**The Gentleman's Agreement** — "Oh, we just handle that with common sense." If it requires judgment, it's not a rule — it's a gap.

**The Power Creep Enabler** — Rules written so loosely that every new card/ability finds an exploit. Tight rules prevent unintended interactions.

**The Retroactive Patch** — Adding rules after problems emerge without checking if the new rule conflicts with existing ones. Every addition must pass the dependency check.

## Outputs

This skill produces:
1. **Formal rule definitions** — every rule with precondition, trigger, resolution, postcondition
2. **Edge case catalog** — known edge cases with resolutions and principles
3. **Rule dependency graph** — which rules reference, modify, and override which
4. **Game term glossary** — precise definitions for every game-specific term
5. **Player-facing rule text** — rulebook (tabletop) or systems spec (digital)

These outputs feed into:
- **Skill 9 (Systems)** — Rules define what systems must implement
- **Skill 11 (Balance)** — Rules with quantitative values need balancing
- **Skill 16 (Playtest)** — Rules are what's being tested
- **Skill 21 (Tech Bridge)** — Rules become implementation specifications
- **Skill 19 (GDD)** — Rules are a core GDD section
