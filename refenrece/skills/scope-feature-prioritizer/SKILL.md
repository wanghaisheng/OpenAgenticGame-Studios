---
name: scope-feature-prioritizer
description: >
  Decide what to build and in what order. The skill of cutting the right things.
  Use this skill when: (1) applying MoSCoW prioritization mapped to design
  pillars, (2) defining the Minimum Viable Game, (3) building feature dependency
  graphs (what must exist before what), (4) making risk-weighted priority
  decisions (high risk = prototype early), (5) managing scope creep by evaluating
  features against pillars, (6) creating and maintaining a cut list with
  reasoning. Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Scope & Feature Prioritizer

Every game has more ideas than time. The skill isn't having ideas — it's choosing which ones earn their place. Everything that makes it into the game takes time from something else. This skill makes those trade-offs explicit.

## Prioritization Philosophy

**Cut early, cut often, cut with data.** Features cut in concept cost nothing. Features cut after implementation cost everything.

**Pillars are the filter.** If a feature doesn't serve a pillar, it doesn't belong — no matter how cool it is. (Skill 2)

**Risk-weighted, not feature-weighted.** The riskiest assumptions should be tested first, regardless of how "important" the feature is to the final product.

## Core Deliverables

### 1. MoSCoW Categorization

Every feature evaluated against pillars:

```
FEATURE              MUST   SHOULD  COULD  WON'T   PILLARS SERVED   RATIONALE
──────────────────── ────── ─────── ────── ─────── ──────────────── ──────────────
[Feature name]       [X]                            [Which pillars?]  [Why here?]
```

**Definitions:**
- **Must** — The game literally cannot function or fulfill its core fantasy without this. If you cut it, you don't have a game.
- **Should** — Significantly enhances the experience and serves pillars. Game works without it but is notably weaker.
- **Could** — Nice to have. Adds polish or depth. Cut this first when time is short.
- **Won't** — Explicitly out of scope for this version. Not "never" but "not now."

**Quality checks:**
- If more than 40% of features are "Must" → you haven't prioritized, you've listed features
- If nothing is "Won't" → scope isn't managed, it's fantasized
- Every "Must" should directly serve at least one pillar
- Every "Won't" should have a clear reason (not just "ran out of time")

### 2. Feature Dependency Graph

What must exist before what:

```
[Core Loop] ──must precede──→ [Economy System]
[Economy System] ──must precede──→ [Crafting]
[Core Loop] ──must precede──→ [Combat System]
[Combat System] ──independent──→ [Crafting]
```

**Dependency types:**
- **Hard dependency** — B literally cannot function without A
- **Soft dependency** — B works without A but is significantly better with it
- **Independent** — A and B have no meaningful dependency

**Critical path:** The longest chain of hard dependencies defines the minimum time to a playable build. This is your critical path.

### 3. Risk-Weighted Priority List

Features prioritized by risk, not importance:

```
FEATURE              RISK LEVEL    RISK TYPE          PRIORITY    RATIONALE
──────────────────── ──────────── ──────────────────── ──────────  ──────────────
[Feature]            [High/Med/Low] [Design/Tech/      [Build     [Why this
                                     Market/Audience]   order #]   order?]
```

**Risk types:**
- **Design risk** — "We don't know if this is fun." → Prototype early.
- **Technical risk** — "We don't know if we can build this." → Spike early.
- **Market risk** — "We don't know if players want this." → Test early.
- **Audience risk** — "We don't know if our target audience engages with this." → Focus test early.

**Priority rule:** High-risk features go first, not high-importance features. A "Must" feature that's low-risk can wait. A "Should" feature that's high-risk should be tested immediately.

### 4. Minimum Viable Game (MVG)

The smallest version of the game that delivers the core fantasy:

```
THE MVG INCLUDES:
  - [Feature] — because [rationale]
  - [Feature] — because [rationale]
  - [Feature] — because [rationale]

THE MVG EXCLUDES:
  - [Feature] — deferred because [rationale]
  - [Feature] — deferred because [rationale]

THE MVG TEST:
  A player who plays the MVG should feel: [core emotional target]
  A player who plays the MVG should understand: [what this game is about]
  A player who plays the MVG should want: [to play more / see what's next]
```

**MVG quality check:**
- [ ] The core loop is complete and functional
- [ ] At least one pillar is fully expressed
- [ ] A new player can understand what the game IS from the MVG alone
- [ ] The core fantasy is achievable, not just promised
- [ ] The MVG is playable and testable, not just theoretically functional

### 5. Cut List

Everything removed from scope, with reasoning preserved:

```
FEATURE              CUT DATE    REASON                  REVISIT?    CONDITIONS
──────────────────── ──────────  ──────────────────────  ──────────  ──────────────
[Feature]            [Date]      [Why it was cut]        [Yes/No]    [When to
                                                                      reconsider]
```

**Why maintain a cut list:**
- Prevents re-proposing cut features without new information
- Documents trade-offs for future reference
- Identifies patterns (if the same feature keeps coming back, maybe it belongs)
- Provides honest communication to stakeholders about what was sacrificed

## Scope Management Techniques

### The Pillar Test
For every proposed feature: "Which pillar does this serve?" If the answer is "none" or requires a stretch, cut it.

### The 10-Second Pitch Test
Can you explain why this feature matters in 10 seconds? If not, it may be a nice idea without a clear purpose.

### The Opportunity Cost Frame
"Adding this feature means NOT doing [specific alternative]." Make the trade-off explicit.

### The Complexity Budget
Every feature adds complexity to learn, maintain, balance, and test. Set a complexity budget and track it:
```
FEATURE              COMPLEXITY COST    CUMULATIVE    BUDGET REMAINING
──────────────────── ──────────────── ──────────────  ──────────────────
Core combat          High               High           75% remaining
Crafting system      Medium             High+Medium    50% remaining
Pet companions       Medium             ...            25% remaining
Weather effects      Low                ...            20% remaining
```

### Scope Creep Detection
Warning signs that scope is expanding:
- "What if we also..." in every design meeting
- Feature list growing between milestones
- No features being cut or deferred
- "We'll figure that out later" as rationale for including something
- Prototype scope expanding beyond the hypothesis being tested

## Workflow

### Initial prioritization

1. **List all proposed features** — Everything the game could include
2. **Run the pillar test** — Does each feature serve a pillar?
3. **Apply MoSCoW** — Categorize ruthlessly
4. **Build dependency graph** — What depends on what?
5. **Assess risk** — Design, technical, market, and audience risk per feature
6. **Define the MVG** — What's the minimum that delivers the fantasy?
7. **Create the cut list** — Everything not in MVG goes here (for now)
8. **Cross-check with budget/timeline** — Does the scope fit reality?
9. **Cross-check with tech bridge** (Skill 21) — Are technical constraints accounted for?
10. **Cross-check with pillars** (Skill 2) — Is every pillar adequately served?

### Ongoing scope management

1. Every new feature proposal runs through the pillar test
2. Every accepted feature gets MoSCoW classification and risk assessment
3. Dependency graph updated when features are added or cut
4. Cut list maintained with reasoning
5. MVG definition reviewed after every major playtest
6. Scope reviewed at every milestone against timeline and budget

### Responding to "can we add this?"

1. Which pillar does it serve?
2. What MoSCoW category would it be?
3. What does it depend on?
4. What's the risk level?
5. What gets cut or deferred to make room?
6. Does this change the MVG?

## Anti-Patterns

**The Kitchen Sink** — "We'll include everything and cut later." You won't cut later. Decide now.

**The Sacred Feature** — A feature that's immune to cutting despite serving no pillar and failing every test. Usually someone's pet idea.

**The False Deadline** — "We don't have time to prioritize, just build everything faster." Prioritization IS how you go faster.

**The Invisible Cut** — Features quietly dropped without documentation. Nobody knows why it was cut, so it keeps coming back.

**The Feature Auction** — Prioritizing features by who argues loudest rather than by pillar alignment and risk.

## Outputs

This skill produces:
1. **MoSCoW categorization** — every feature prioritized against pillars
2. **Feature dependency graph** — build order constraints
3. **Risk-weighted priority list** — what to build/test first
4. **Minimum Viable Game definition** — smallest version that delivers the fantasy
5. **Cut list** — everything removed with reasoning and revisit conditions

These outputs feed into:
- **Skill 2 (Pillars)** — Pillars are the primary filter
- **Skill 15 (Prototype)** — What to prototype first
- **Skill 21 (Tech Bridge)** — Feasibility informs priority
- **Skill 19 (GDD)** — Scope is a core GDD section
- **Skill 0 (Coherence)** — Scope changes may trigger re-evaluation
