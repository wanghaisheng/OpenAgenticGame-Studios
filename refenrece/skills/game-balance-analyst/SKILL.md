---
name: game-balance-analyst
description: >
  Ensure meaningful choice — no dominant strategies, no dead options, no runaway
  leaders or hopeless laggards. Use this skill when: (1) evaluating whether all
  player options are viable, (2) identifying dominant strategies that eliminate
  meaningful choice, (3) designing asymmetric balance (different factions,
  characters, or roles that feel fair despite being different), (4) building
  Monte Carlo or statistical models to test probabilistic systems, (5) creating
  balance levers — the knobs you can turn to adjust without redesigning,
  (6) diagnosing why a game feels unfair even when it technically isn't,
  (7) building matchup matrices for competitive games. Medium-agnostic —
  works for digital, tabletop, and hybrid games.
---

# Game Balance Analyst

Balance is not "everything is equal." Balance is "every choice is interesting." A perfectly balanced game where all options are identical is not balanced — it's boring. The goal is meaningful asymmetry where every option has a reason to exist.

## Balance Philosophy

### What Balance Actually Means

**Balance means:** Every player-facing option is a viable choice in some context. No option is strictly better than all alternatives. The player's decision matters.

**Balance does NOT mean:**
- Everything deals the same damage
- All factions have the same units
- Win rates are exactly 50/50
- Every strategy is equally good in every situation

**The balance target:** Players should lose because they were outplayed, not because they picked the wrong character/faction/build at the select screen.

### Types of Balance

**Symmetric balance** — All players start with identical options.
- Chess, Go, most abstract games
- Balance challenge: First-player advantage, solved strategies
- Easier to balance, harder to make feel diverse

**Asymmetric balance** — Players have different options that are intended to feel equally viable.
- StarCraft factions, fighting game characters, role-based co-op
- Balance challenge: Different capabilities must produce comparable outcomes
- Harder to balance, more interesting to play

**Dynamic balance** — Balance state changes over the course of play.
- Early-game vs. late-game power, meta-game evolution, seasonal patches
- Balance challenge: A strategy dominant at one phase must be vulnerable at another
- Requires balancing across time, not just at a snapshot

**Contextual balance** — Options are balanced within specific contexts.
- Rock-paper-scissors relationship between unit types
- Terrain-dependent strategies
- Balance challenge: No context should be overwhelmingly common
- The ideal — balance through interesting trade-offs

## Core Deliverables

### 1. Balance Framework Definition

Before balancing anything, define *what* balanced means for this specific game:

```
BALANCE TYPE:         [Symmetric / Asymmetric / Dynamic / Contextual / Hybrid]
BALANCE METRIC:       [What are we measuring? Win rate? Option pick rate? Fun?]
BALANCE TOLERANCE:    [How far from "ideal" is acceptable?]
                      (e.g., "All factions should win 45-55% of the time")
INTENTIONAL IMBALANCE:[What is deliberately NOT balanced, and why?]
                      (e.g., "Late-game options are intentionally stronger to
                       reward investment")
```

### 2. Dominant Strategy Analysis

A dominant strategy is an option that is strictly better than alternatives — it eliminates meaningful choice.

**Detection methods:**

**Option comparison matrix:**
```
OPTION        SCENARIO A    SCENARIO B    SCENARIO C    OVERALL
──────────── ──────────── ──────────── ──────────── ────────────
Warrior       Strong        Strong        Medium        Dominant?
Mage          Weak          Strong        Strong        Contextual
Rogue         Medium        Weak          Strong        Contextual
Healer        Weak          Weak          Weak          Dead option
```

If any option is "Strong" in every scenario → likely dominant.
If any option is "Weak" in every scenario → likely dead.

**Efficiency analysis:**
For each option, calculate value per cost:
```
OPTION     EFFECT          COST        EFFICIENCY    RELATIVE
────────── ──────────────  ──────────  ────────────  ────────────
Sword      10 damage       5 gold      2.0 dmg/gold  Baseline
Axe        15 damage       6 gold      2.5 dmg/gold  +25% efficient
Dagger     6 damage        3 gold      2.0 dmg/gold  Equal
Staff      8 damage        8 gold      1.0 dmg/gold  -50% efficient
```

If efficiency varies more than 30-40% without compensating factors → balance problem.

**Counter-play check:**
For every strong strategy, there must be a viable counter:
```
STRATEGY           COUNTER              COUNTER-COUNTER
────────────────── ──────────────────── ────────────────────
Rush (aggressive)  Turtle (defensive)   Tech rush (economy)
Turtle             Tech rush            Rush
Tech rush          Rush                 Turtle
```

Healthy: circular counter relationships. Unhealthy: linear "just be better" hierarchy.

### 3. Option Viability Matrix

Every player-facing choice should be worth considering. Audit all options:

```
OPTION          NICHE                PICK RATE TARGET   ACTUAL    STATUS
──────────────  ──────────────────── ────────────────── ──────── ──────────
[Option name]   [When is this best?] [Expected %]       [Data %] [Healthy/
                                                                  Over/Under]
```

**Viability criteria:**
- [ ] The option has at least one scenario where it's the best choice
- [ ] The option has a distinct identity (not just a worse version of another option)
- [ ] The option requires a different playstyle (not just different numbers)
- [ ] A player who picks this option doesn't feel punished
- [ ] The option has counter-play (it can be beaten)

**Dead option symptoms:**
- Pick rate below 5% in competitive play
- No scenario where it's optimal
- Community consensus that it's "the worst option"
- Only picked by players who don't know better

**Overpowered option symptoms:**
- Pick rate above 40% in competitive play (for games with 4+ options)
- Optimal in most scenarios regardless of context
- Community meta coalesces around this option
- Counter-play exists but is too narrow or too costly

### 4. Statistical Modeling

For games with randomness, intuition isn't enough. Model the probabilities.

**Expected value calculations:**
```
ACTION: Attack with Flameblade
  Hit chance: 70%
  On hit: 2d6+3 damage (average 10)
  On miss: 0 damage
  Expected value: 0.7 * 10 = 7.0 expected damage per attack

vs.

ACTION: Attack with Iceshard
  Hit chance: 90%
  On hit: 1d6+1 damage (average 4.5)
  On miss: half damage = 2.25
  Expected value: (0.9 * 4.5) + (0.1 * 2.25) = 4.275 expected damage per attack
```

Flameblade has higher expected damage but higher variance. Iceshard is consistent. Both are viable if the game rewards different risk profiles.

**Monte Carlo simulation approach:**
For complex systems where analytical solutions aren't feasible:
1. Define the variables and their ranges
2. Run N simulated games/encounters (N = 1000+ for statistical significance)
3. Record outcomes per strategy/option
4. Analyze distribution, not just averages
5. Look for outlier cases — the 1% outcomes that break the experience

**Variance analysis:**
High variance creates exciting moments but frustrating consistency.
Low variance creates reliable gameplay but can feel flat.

```
SYSTEM              CURRENT VARIANCE    TARGET VARIANCE   RATIONALE
──────────────────  ──────────────────  ──────────────── ──────────────────
Combat damage       High (d12 range)    Medium            Too swingy for
                                                          tactical game
Loot drops          Low (fixed tables)  High              Discovery needs
                                                          surprise
Movement range      None (fixed)        None              Predictability
                                                          enables planning
```

### 5. Balance Lever Identification

Balance levers are the knobs you can turn to adjust balance without redesigning systems. Identify them early.

**Quantitative levers** (numbers to adjust):
- Damage/healing values
- Costs (resource, time, opportunity)
- Probabilities (hit chance, drop rate, crit rate)
- Durations (cooldowns, effect timers)
- Ranges (attack range, movement range, detection range)
- Capacities (inventory size, hand limit, unit cap)

**Structural levers** (mechanics to modify):
- Adding/removing counter-play options
- Changing resource conversion rates
- Adjusting prerequisite chains
- Modifying timing windows

**Environmental levers** (context to change):
- Map/level design that favors different strategies
- Encounter composition that requires different approaches
- Meta-game rules (ban lists, draft order, map pools)

**For each lever, document:**
```
LEVER:          [What can be adjusted]
AFFECTS:        [What systems/options does this change?]
DIRECTION:      [Does increasing this buff or nerf?]
SENSITIVITY:    [How much does a small change matter? Low/Medium/High]
SIDE EFFECTS:   [What else changes when this is adjusted?]
CURRENT VALUE:  [What is it set to now?]
VALID RANGE:    [What are the reasonable min/max?]
```

### 6. Matchup Matrices (for competitive/asymmetric games)

For games where different options face each other:

```
ATTACKER →    Warrior   Mage      Rogue     Healer
DEFENDER ↓
Warrior       50/50     40/60     60/40     70/30
Mage          60/40     50/50     45/55     55/45
Rogue         40/60     55/45     50/50     60/40
Healer        30/70     45/55     40/60     50/50
```

**Healthy matchup characteristics:**
- No matchup worse than 30/70 (no hard counters that feel hopeless)
- No matchup better than 70/30 (no auto-wins)
- Every option has at least one favorable matchup
- Circular relationships (A beats B, B beats C, C beats A)
- Mirror matches are close to 50/50

**Unhealthy flags:**
- One row is all >55% → overpowered option
- One row is all <45% → underpowered option
- Linear hierarchy (A > B > C > D) → no interesting counter-play
- Any cell at 20/80 or worse → frustrating matchup

## Workflow

### Building a balance framework from scratch

1. **Define balance type** — Symmetric, asymmetric, dynamic, or contextual?
2. **Define balance metrics** — What are we measuring?
3. **Set tolerance ranges** — How far from ideal is acceptable?
4. **Identify intentional imbalances** — What's deliberately unbalanced?
5. **List all player-facing options** — Everything the player can choose
6. **Run dominant strategy analysis** — Are any options clearly best?
7. **Build option viability matrix** — Does every option have a niche?
8. **Model statistical systems** — Calculate expected values, run simulations
9. **Identify balance levers** — What knobs can we turn?
10. **Build matchup matrices** (if applicable) — How do options fare against each other?
11. **Cross-reference with rules** (Skill 8) — Are the formalized rules producing the intended balance?
12. **Cross-reference with economy** (Skill 10) — Are economic values balanced?
13. **Flag to playtest** (Skill 16) — Balance hypotheses need live testing

### Responding to a balance complaint

1. Clarify the complaint — "too strong," "feels unfair," "this option is useless"
2. Gather data — Is this perception or measurement? Both matter, but differently.
3. Check the option viability matrix — Is this option actually underperforming?
4. Check matchup context — Is it underpowered generally or in a specific matchup?
5. Check the player's skill level — Is this a balance issue or a knowledge issue?
6. If real: identify the appropriate balance lever
7. Model the proposed change — What does adjusting this lever do to all affected systems?
8. Check for cascading effects — Does the fix create a new problem?
9. Propose the minimum change that addresses the issue

### Ongoing balance maintenance (live games)

1. Track pick rates and win rates per option
2. Compare actual data to balance targets
3. Identify emerging dominant strategies
4. Distinguish between meta-game shifts and genuine imbalance
5. Plan balance changes in batches, not one at a time
6. Communicate changes and reasoning to players
7. Log all changes in Design Iteration Tracker (Skill 17)

## Balance Anti-Patterns

**The Nerf Spiral** — Repeatedly nerfing the strongest option instead of buffing weak ones. Eventually everything feels bad.

**The Spreadsheet Trap** — Numbers are perfectly balanced but the *feel* is wrong. A weapon that does 10 DPS on paper but feels terrible to use is not balanced.

**The False Symmetry** — Making asymmetric options "balanced" by making them functionally identical. If the Warrior and Mage play the same, why have both?

**The Complexity Tax** — A hard-to-execute option is balanced on paper but its difficulty makes it unviable for most players. Balance must account for execution difficulty.

**The Meta Ignore** — Balancing individual options without considering the meta-game. Option A is balanced against Option B, but when combined with Option C, it's broken.

**The Patch Treadmill** — Constant balance changes that prevent players from ever learning the game deeply. Stability has value.

## Outputs

This skill produces:
1. **Balance framework** — type, metrics, tolerances, intentional imbalances
2. **Dominant strategy analysis** — identified dominant and dead options with evidence
3. **Option viability matrix** — every option with niche, pick rate target, and status
4. **Statistical models** — expected values, variance analysis, simulation results
5. **Balance lever catalog** — every adjustable parameter with sensitivity and side effects
6. **Matchup matrices** — option-vs-option performance for competitive games

These outputs feed into:
- **Skill 8 (Rules)** — Balance changes become rule changes
- **Skill 9 (Systems)** — Balance interacts with system feedback loops
- **Skill 10 (Economy)** — Economic values are balance parameters
- **Skill 16 (Playtest)** — Balance hypotheses need testing
- **Skill 17 (Iteration)** — Balance is the most iterated element
- **Skill 20 (Scope)** — Balance complexity affects scope
