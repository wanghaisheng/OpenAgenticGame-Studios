---
name: economy-progression-designer
description: >
  Design the mathematical backbone of a game — resource flows, power curves,
  unlock pacing, and reward schedules. Use this skill when: (1) designing
  resource systems (currencies, materials, energy, cards, tokens), (2) defining
  progression curves (XP, power, unlock cadence), (3) choosing reward schedules
  (fixed, variable, interval-based), (4) diagnosing inflation, deflation, or
  resource starvation, (5) designing monetization without pay-to-win (if
  applicable), (6) pacing unlock cadence across a campaign or live service,
  (7) balancing resource sinks against sources to maintain a healthy economy
  over time. Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Economy & Progression Designer

The economy is the circulatory system of the game. Resources flow, convert, accumulate, and deplete. Progression is the patient's growth over time. Design both wrong and the game either hemorrhages or clots.

## Economy Fundamentals

### The Four Pillars of Game Economy

Every game economy, no matter how simple, has four elements:

**Sources** — Where resources enter the game.
- Killing enemies drops gold
- Passing GO collects $200
- Beginning of turn produces resources based on territory
- Drawing cards from the deck

**Sinks** — Where resources leave the game.
- Buying items from shops
- Paying upkeep/maintenance costs
- Card discard/exhaustion
- Death penalties (lose gold, lose items)

**Converters** — Where one resource type transforms into another.
- Crafting (materials → equipment)
- Training (gold + time → skill levels)
- Trading posts (resource A → resource B)
- Card upgrade (base card + currency → improved card)

**Traders** — Where resources move between players or between player and game.
- Player-to-player trading
- Auction houses
- Drafting (select from shared pool)
- Markets with dynamic pricing

**The health equation:**
If Sources > Sinks over time → **Inflation** (resources become meaningless)
If Sinks > Sources over time → **Deflation** (players feel starved)
If Sources ≈ Sinks with variance → **Healthy** (resources feel valuable but attainable)

### Resource Types

**Hard currencies** — Limited supply, primary value driver.
- Premium currency, rare materials, unique items
- Should always feel slightly scarce
- Primary sink should be meaningful choices

**Soft currencies** — Abundant supply, lubricant for gameplay.
- Gold, common materials, basic ammo
- Should never fully block progress
- Primary role is creating micro-decisions, not gates

**Time currencies** — Gated by real or game time.
- Energy systems, cooldowns, turn limits
- Creates pacing and prevents binging (or monetizes impatience)
- Must feel fair, not manipulative

**Attention currencies** — Gated by player cognitive/action bandwidth.
- Action points, hand size, inventory slots
- Creates prioritization decisions
- The most elegant economy constraint — it's invisible

**Social currencies** — Value derived from other players.
- Reputation, alliances, traded goods, shared resources
- Multiplayer only; creates interdependence
- Hardest to balance because humans are unpredictable

## Core Deliverables

### 1. Resource Flow Diagram

Map every resource's lifecycle:

```
[SOURCE] ──amount/rate──→ [POOL] ──cost──→ [SINK]
                            │
                            ├──conversion──→ [CONVERTER] ──→ [DIFFERENT POOL]
                            │
                            └──trade──→ [OTHER PLAYER/SYSTEM]
```

For each resource, document:
```
RESOURCE:      [Name]
TYPE:          [Hard / Soft / Time / Attention / Social]
SOURCES:       [Where it comes from, with rates]
SINKS:         [Where it goes, with costs]
CONVERTERS:    [What it transforms into]
CAP:           [Maximum amount a player can hold? Or unlimited?]
STARTING:      [How much does a player begin with?]
VISIBILITY:    [Is the exact amount visible to the player? To other players?]
FEEL TARGET:   [Should this feel scarce? Abundant? Variable?]
```

### 2. Progression Curves

Progression is the long-arc economy — how the player's capability, content access, and experience evolve over time.

**Power curve** — How strong does the player get, and how fast?

```
TIME          POWER LEVEL    UNLOCK MILESTONE        FEEL
────────────  ─────────────  ────────────────────── ──────────────────
0-30 min      Baseline       Tutorial complete       "I can do things"
30-120 min    +20-40%        Core systems unlocked   "I'm getting good"
2-5 hours     +60-100%       Build identity emerges  "This is MY build"
5-20 hours    +150-250%      Advanced options open    "I'm mastering this"
20+ hours     +300-500%      Endgame/prestige         "I'm expressing myself"
```

**Curve shapes:**
- **Linear** — Steady, predictable growth. Safe but can feel grindy. Good for: casual games, tabletop campaigns.
- **Logarithmic** — Fast early, slowing later. Feels rewarding early but "plateaus." Good for: games with a defined endpoint.
- **Exponential** — Slow early, accelerating later. Frustrating start but explosive endgame. Good for: incremental/idle games.
- **S-curve** — Slow start, fast middle, slow end. The most natural feeling for most games. Good for: RPGs, campaign games.
- **Stepped** — Flat periods punctuated by jumps. Creates moments of transformation. Good for: tier-based progression, prestige systems.

### 3. Reward Schedule Model

When and how the player receives rewards determines engagement more than *what* the reward is.

**Fixed ratio** — Reward after N actions.
- "Every 5 kills, earn a bonus"
- Predictable, steady. Can feel grindy.
- Best for: routine tasks the player should always do

**Variable ratio** — Reward after random N actions (average known, exact unknown).
- "Each enemy has a 20% chance to drop rare loot"
- Highly engaging, the "slot machine" effect. Can be addictive/exploitative.
- Best for: optional rewards, excitement moments

**Fixed interval** — Reward after N time units.
- "Daily login bonus" / "End of round scoring"
- Creates rhythm and habit. Can feel like a chore.
- Best for: session bookends, campaign milestones

**Variable interval** — Reward at random time intervals.
- "Random events" / "Wandering merchants"
- Creates anticipation and surprise. Can feel unfair.
- Best for: discovery moments, world-building events

**Compound schedules** — Layer multiple schedules:
```
LAYER 1 (micro):   Variable ratio — each combat has random loot drops
LAYER 2 (session):  Fixed ratio — complete 3 missions for a guaranteed reward
LAYER 3 (campaign): Fixed interval — story beats every ~2 hours
LAYER 4 (meta):     Variable interval — seasonal events and surprise content
```

**Reward type variety** — Alternate between:
- **Power rewards** — Make the player stronger (gear, levels, abilities)
- **Content rewards** — Give the player new things to do (areas, modes, characters)
- **Cosmetic rewards** — Let the player express identity (skins, titles, decorations)
- **Knowledge rewards** — Reveal information (lore, map, strategy options)
- **Social rewards** — Recognition from others (leaderboards, achievements, titles)

### 4. Inflation/Deflation Analysis

Project the economy's health at key time horizons:

```
TIMEPOINT       TOTAL SOURCES    TOTAL SINKS    NET FLOW    HEALTH
──────────────  ──────────────── ──────────────  ──────────  ──────────
Session 1       [amount/session] [amount/session] [+/-]      [Assessment]
Session 10      [amount/session] [amount/session] [+/-]      [Assessment]
Session 50      [amount/session] [amount/session] [+/-]      [Assessment]
Session 100+    [amount/session] [amount/session] [+/-]      [Assessment]
```

**Inflation warning signs:**
- Players accumulate resources with nothing meaningful to spend on
- Prices in player-to-player trades escalate over time
- Late-game resources feel trivial
- "I have 50,000 gold and nothing to buy"

**Deflation warning signs:**
- Players feel constantly starved
- Progress stalls because resource gates are too tight
- Players hoard instead of spending (fear of waste)
- "I've been saving for 10 hours and still can't afford the upgrade"

**Control mechanisms:**
- **Progressive sinks** — More expensive options unlock as the player progresses
- **Maintenance costs** — Ongoing costs that scale with player power
- **Diminishing returns** — Each additional unit of a resource is worth less
- **Dynamic pricing** — Costs adjust based on player wealth or game state
- **Prestige/reset mechanics** — Voluntary reset for permanent bonuses

### 5. Pacing Benchmarks

Define concrete snapshots of the player's economic state at key moments:

```
BENCHMARK: "Session 1 Player"
─────────────────────────────
Resources:    [What they have]
Unlocks:      [What they've opened]
Power level:  [Relative strength]
Decisions:    [What meaningful choices they face]
Emotional target: [How should they feel about their economic state?]

BENCHMARK: "Session 10 Player"
─────────────────────────────
[Same format]

BENCHMARK: "Session 50 Player"
─────────────────────────────
[Same format]
```

These benchmarks become balance targets (Skill 11) and playtest validation criteria (Skill 16).

## Progression Systems

### Unlock Pacing

The cadence at which new content/abilities become available:

**Principles:**
- **Front-load variety** — Give new players options quickly to sustain engagement
- **Space out transformative unlocks** — Major game-changers should be paced, not dumped
- **End-game unlocks should be lateral, not vertical** — Late unlocks add options, not just power
- **Every unlock should change how the player plays** — An unlock that's just "+5% damage" isn't a meaningful unlock

**Unlock cadence planning:**
```
HOUR 0-1:    [Rapid unlocks — new option every 5-10 min]
HOUR 1-5:    [Steady unlocks — new option every 15-30 min]
HOUR 5-20:   [Spaced unlocks — new option every 1-2 hours]
HOUR 20+:    [Rare unlocks — mastery rewards, prestige, cosmetic]
```

### Progression Archetypes

**Vertical progression** — Player gets objectively stronger.
- Level 10 character beats level 5 character
- Risk: power gap makes content trivial or multiplayer unfair
- Mitigation: level scaling, level-gated content, PvP normalization

**Horizontal progression** — Player gets more options, not more power.
- New character classes, new weapon types, new strategies
- Risk: option overload, balance nightmare
- Mitigation: clear trade-offs between options, build archetypes

**Prestige progression** — Player resets for permanent bonuses.
- New Game+, seasonal resets, prestige ranks
- Risk: reset feels punishing, not rewarding
- Mitigation: meaningful permanent carries, visible prestige markers

**Social progression** — Player advances through community standing.
- Guilds, reputation, ranked ladders
- Risk: toxic competition, exclusion
- Mitigation: multiple paths, cooperation incentives

## Workflow

### Designing an economy from scratch

1. **List all resources** — Everything the player earns, spends, or trades
2. **Classify each resource** — Hard, soft, time, attention, social
3. **Map sources and sinks** — Where does each resource come from and go?
4. **Add converters and traders** — How do resources transform and move?
5. **Draw the resource flow diagram** — Visual map of the full economy
6. **Define the progression curve** — Shape, pace, milestones
7. **Design reward schedules** — What schedule for what reward at what layer?
8. **Set pacing benchmarks** — Concrete snapshots at session 1, 10, 50
9. **Project inflation/deflation** — Will the economy stay healthy over time?
10. **Cross-check with core loop** (Skill 7) — Does the economy power the reward phase?
11. **Cross-check with experience model** (Skill 4) — Does progression deliver the intended emotional arc?
12. **Cross-check with pillars** (Skill 2) — Does the economy serve the pillars?
13. **Flag to balance** (Skill 11) — All quantitative values need testing

### Diagnosing an unhealthy economy

1. Identify the symptom: Inflation? Deflation? Grind wall? Meaningless rewards?
2. Trace the resource flow — where is the blockage or flood?
3. Check source/sink balance — is net flow positive or negative?
4. Check reward schedules — are rewards too predictable or too stingy?
5. Check progression curve — has the player hit a plateau with no new unlocks?
6. Check sinks — are there enough meaningful things to spend on?
7. Propose fix and run through systems interaction map (Skill 9) for cascading effects

### Economy and monetization (if applicable)

If the game has real-money transactions:
1. Separate "earnable" and "purchasable" — clarity for the player
2. Never sell power advantage in competitive contexts
3. Respect the player's time investment — purchased items shouldn't trivialize earned items
4. Test the free path independently — is the game fun without spending?
5. Document the monetization philosophy as part of the economy design

## Anti-Patterns

**The Faucet Without a Drain** — Resources pour in but have nowhere to go. Players drown in gold with nothing to buy.

**The Paywall Masquerading as Progression** — Progress is gated not by gameplay but by artificial time/resource walls designed to sell shortcuts.

**The Meaningless Number** — "Level 500!" that feels no different from Level 499. Big numbers aren't progression if they don't change gameplay.

**The Single Funnel** — One resource does everything. No trade-offs, no interesting economic decisions. "Just get more gold."

**The Invisible Economy** — Resources and costs are so opaque the player can't make informed decisions. Economy requires spreadsheets to understand.

## Outputs

This skill produces:
1. **Resource flow diagram** — sources, sinks, converters, traders for every resource
2. **Progression curves** — power, unlock cadence, and curve shape per timeframe
3. **Reward schedule model** — schedule type per reward layer with compound structure
4. **Inflation/deflation analysis** — projected economy health at key time horizons
5. **Pacing benchmarks** — concrete player state snapshots at session 1, 10, 50, 100

These outputs feed into:
- **Skill 7 (Core Loop)** — Economy powers the reward phase of the loop
- **Skill 9 (Systems)** — Economy interacts with every other system
- **Skill 11 (Balance)** — All economic values need balancing
- **Skill 13 (Levels)** — Resource pacing per encounter/level
- **Skill 16 (Playtest)** — Economic health needs testing at benchmarks
- **Skill 20 (Scope)** — Economy complexity affects scope
