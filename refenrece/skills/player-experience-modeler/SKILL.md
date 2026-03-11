---
name: player-experience-modeler
description: >
  Map the intended emotional journey and psychological engagement model for a game.
  Defines what the player should feel at each stage of play and what motivates
  continued engagement. Use this skill when: (1) translating a vision and pillars into
  concrete emotional targets, (2) designing the pacing of a play session or campaign,
  (3) evaluating whether a game delivers the intended experience, (4) diagnosing why a
  game "feels off" despite sound mechanics, (5) choosing between design options based
  on which better serves the intended experience, (6) mapping flow state targets and
  challenge curves. Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# Player Experience Modeler

Define what the player should *feel*, not just what they should *do*. Mechanics are the vehicle. Experience is the destination.

## Experience Frameworks

Use these frameworks as lenses, not checklists. Apply whichever combination reveals the most about your specific game.

### MDA (Mechanics-Dynamics-Aesthetics)

Work backward from desired aesthetics (emotional responses) to dynamics (runtime behavior) to mechanics (rules):

**8 Aesthetic Categories** (Hunicke, LeBlanc, Zubek):
1. **Sensation** — Game as sense-pleasure
2. **Fantasy** — Game as make-believe
3. **Narrative** — Game as drama
4. **Challenge** — Game as obstacle course
5. **Fellowship** — Game as social framework
6. **Discovery** — Game as uncharted territory
7. **Expression** — Game as self-discovery
8. **Submission** — Game as pastime

Identify your game's primary aesthetics (2-3 max). These must align with your pillars and core fantasy.

### Bartle Player Types (first-pass lens, multiplayer)

A useful starting filter — 4 broad types from Richard Bartle's 1996 MUD research:

- **Achievers** — Want to accumulate, complete, master
- **Explorers** — Want to discover, understand, map
- **Socializers** — Want to connect, communicate, belong
- **Killers** — Want to compete, dominate, impose

Which types does your game primarily serve? Which are explicitly NOT served? Bartle is a quick first-pass. For deeper motivational modeling, use Quantic Foundry below.

**Bartle's limitations:** Only 4 types, derived from text MUDs, treats motivations as exclusive categories rather than spectra, and lacks empirical personality grounding. Use it for fast alignment — then refine with Quantic Foundry.

### Quantic Foundry Gamer Motivation Model (primary motivation lens)

Nick Yee's empirically-derived model based on data from 1,250,000+ gamers. Identifies 12 motivation factors in 6 paired clusters across 3 high-level groups. Each motivation is a spectrum (0-100%), not a binary type — players have a unique profile across all 12.

**3 Groups → 6 Clusters → 12 Motivations:**

```
ACTION-SOCIAL (correlates with Extraversion in OCEAN)
├── Action
│   ├── Destruction — Chaos, explosions, mayhem, causing havoc
│   └── Excitement — Fast-paced, thrilling, action-packed, surprising
└── Social
    ├── Competition — Duels, matches, PvP, leaderboards, being the best
    └── Community — Teamwork, chatting, groups, guilds, being on a team

MASTERY-ACHIEVEMENT (correlates with Conscientiousness in OCEAN)
├── Mastery
│   ├── Challenge — Difficulty, practice, skill mastery, hard-won victory
│   └── Strategy — Thinking ahead, planning, decision-making, second-order effects
└── Achievement
    ├── Completion — Collecting everything, finishing all missions, 100% completion
    └── Power — Powerful characters, rare gear, leveling up, becoming dominant

IMMERSION-CREATIVITY (correlates with Openness to Experience in OCEAN)
├── Immersion
│   ├── Fantasy — Being someone else, somewhere else, role-playing, escapism
│   └── Story — Elaborate plots, interesting characters, narrative depth
└── Creativity
    ├── Design — Expression, customization, building, decorating, personal style
    └── Discovery — Exploring, experimenting, tinkering, finding hidden things
```

**OCEAN / Big Five Personality Correlation:**

| OCEAN Trait | Gaming Motivation Group | Correlation |
|---|---|---|
| **Openness** (curious, imaginative) | Immersion-Creativity (Fantasy, Story, Design, Discovery) | Strong positive |
| **Conscientiousness** (organized, disciplined) | Mastery-Achievement (Challenge, Strategy, Completion, Power) | Moderate positive |
| **Extraversion** (outgoing, energetic) | Action-Social (Destruction, Excitement, Competition, Community) | Strong positive |
| **Agreeableness** (sympathetic, cooperative) | No clean cluster — correlates with Community, inversely with Competition | Partial |
| **Neuroticism** (anxious, sensitive) | No clean cluster mapping — research ongoing | Weak/none |

**How to use this model:**

For your game, score each of the 12 motivations as a target:
```
MOTIVATION       TARGET     NOTES
──────────────── ────────── ──────────────────────────────────
Destruction       [0-100%]   [How much does your game deliver this?]
Excitement        [0-100%]   [...]
Competition       [0-100%]   [...]
Community         [0-100%]   [...]
Challenge         [0-100%]   [...]
Strategy          [0-100%]   [...]
Completion        [0-100%]   [...]
Power             [0-100%]   [...]
Fantasy           [0-100%]   [...]
Story             [0-100%]   [...]
Design            [0-100%]   [...]
Discovery         [0-100%]   [...]
```

This creates a motivation fingerprint for your game. Compare it to:
- Your target player personas (do their motivation profiles match what you're building?)
- Comp titles (what's the motivation profile of Deep Rock Galactic vs. your game?)
- Market gaps (is there a motivation combination nobody's serving?)

**Key advantage over Bartle:** A player can score 90% on both Community AND Competition — they love cooperative teams AND being the best. Bartle forces a choice. Quantic Foundry recognizes that motivations coexist on spectra.

### Self-Determination Theory (SDT)

Three innate psychological needs that drive intrinsic motivation:
- **Autonomy** — Feeling of choice and agency
- **Competence** — Feeling of mastery and effectiveness
- **Relatedness** — Feeling of connection and belonging

Map how your game satisfies each. Which is the primary driver? Where are the gaps?

### Flow Model (Csikszentmihalyi)

The balance between challenge and skill that produces optimal engagement:

```
            HIGH
  ANXIETY   │          FLOW
            │        ╱
 Challenge  │      ╱
            │    ╱
            │  ╱
  BOREDOM   │╱         RELAXATION
            └──────────────────
            LOW    Skill    HIGH
```

Define your flow targets:
- **Entry flow** — Where should a new player sit on the challenge/skill curve?
- **Session flow** — How should challenge ramp within a single session?
- **Mastery flow** — How does the curve evolve over hours 1, 10, 100?
- **Flow disruptors** — What intentionally breaks flow? (Narrative beats, social moments, discovery pauses)

### Lenses of Game Design (Schell)

Selected lenses particularly useful for experience modeling:
- **Lens of Essential Experience** — What experience do I want the player to have? What is essential to that experience?
- **Lens of Surprise** — What surprises the player? Does the game have enough of them?
- **Lens of Curiosity** — What questions does the game put in the player's mind? What can I do to make them even more curious?
- **Lens of Endogenous Value** — How can I make items in my game more valuable to players?
- **Lens of the Hero's Journey** — Does the player's emotional arc mirror a hero's journey?

## Core Deliverables

### 1. Emotional Arc Map

Chart the intended emotional journey across two scales:

**Per-session arc** (what a single play session should feel like):
```
MOMENT          EMOTION              INTENSITY
─────────────── ──────────────────── ─────────
Session start   Anticipation/Curiosity   ██░░░
Early play      Discovery/Orientation    ███░░
Mid session     Engagement/Flow          ████░
Tension peak    Excitement/Anxiety       █████
Climax          Triumph/Devastation      █████
Resolution      Satisfaction/Reflection  ███░░
Session end     Desire to return         ██░░░
```

**Campaign/progression arc** (how the experience evolves over many sessions):
Map emotional evolution at session 1, session 5, session 20, session 50+. What changes? What stays constant? Where does the game's emotional center of gravity shift?

### 2. Engagement Model

What motivates continued play? Define the primary and secondary engagement drivers:

**Short-term drivers** (why keep playing this session):
- Immediate feedback loop satisfaction
- "One more try" pull
- Social momentum (friends are still playing)
- Unresolved curiosity (what's around the next corner?)

**Medium-term drivers** (why come back tomorrow):
- Progression toward a goal
- Unfinished business
- Social commitment (our group plays Thursdays)
- New content/discovery promise

**Long-term drivers** (why still playing in 6 months):
- Mastery depth
- Social identity (this is "our game")
- Evolving meta/challenge
- Creative expression possibilities
- Community belonging

### 3. Flow State Targets

For each phase of play, define the challenge-skill balance target:

```
PHASE           CHALLENGE    SKILL REQUIRED    FLOW TARGET
────────────── ──────────── ──────────────── ──────────────
Onboarding      Low          Low               Guided flow
Early game      Medium-Low   Low-Medium        Learning flow
Core gameplay   Medium       Medium            Engaged flow
Advanced play   High         High              Mastery flow
Endgame/Meta    Variable     High              Creative flow
```

Define what pushes the player OUT of flow and whether that's intentional:
- Difficulty spikes (intentional tension builder or bad balance?)
- Information overload (designed overwhelm or UI failure?)
- Downtime (narrative breathing room or pacing problem?)

### 4. Player Motivation Profile

Using the frameworks above, create a profile:

```
PRIMARY AESTHETICS (MDA):      [2-3 from the 8 categories]
BARTLE QUICK-PASS:             [1-2 types served, 1-2 explicitly NOT served]
QUANTIC FOUNDRY FINGERPRINT:   [Score all 12 motivations — see template below]
SDT EMPHASIS:                  [Which need is primary?]
FLOW PHILOSOPHY:               [Steady state? Oscillating? Escalating?]
KEY LENSES:                    [Which Schell lenses are most relevant?]
OCEAN IMPLICATION:             [What personality traits does this game attract?]
```

**Quantic Foundry motivation fingerprint for your game:**
```
ACTION-SOCIAL                    MASTERY-ACHIEVEMENT              IMMERSION-CREATIVITY
Destruction  [__]%               Challenge   [__]%                Fantasy     [__]%
Excitement   [__]%               Strategy    [__]%                Story       [__]%
Competition  [__]%               Completion  [__]%                Design      [__]%
Community    [__]%               Power       [__]%                Discovery   [__]%
```

**Reading the fingerprint:**
- High scores (70%+) = your game is designed to deliver this strongly
- Medium scores (30-70%) = present but not a focus
- Low scores (<30%) = intentionally absent or irrelevant
- The SHAPE of the profile matters more than individual scores — a game high on Community + Discovery + Strategy but low on Competition + Power + Destruction is a very different product than the reverse
- Compare your game's fingerprint to your target persona's fingerprint — mismatches reveal design-audience misalignment

## Workflow

### Building an experience model from scratch

1. **Start with the core fantasy** (from Vision, Skill 1) — What emotion does the fantasy promise?
2. **Reference the pillars** (from Skill 2) — Which pillars have direct emotional implications?
3. **Reference the aesthetic direction** (from Skill 3) — How does sensory identity shape emotional delivery?
4. **Select applicable frameworks** — Not all frameworks apply to all games. Pick 2-3 that reveal the most.
5. **Draft the emotional arc** — Session level first, then campaign/progression level
6. **Define engagement drivers** — Short, medium, and long-term
7. **Set flow targets** — Per phase of play
8. **Build motivation profile** — Synthesize across frameworks
9. **Cross-check** — Does every element serve the core fantasy? Do engagement drivers match player personas?

### Diagnosing a "feels wrong" problem

1. Identify the moment that feels wrong
2. What emotion was intended at this moment?
3. What emotion is actually being produced?
4. Check each layer: Is the mechanic right but the pacing wrong? The aesthetic misaligned? The challenge/skill balance off?
5. Trace the misalignment to a specific deliverable (arc, engagement, flow, or motivation)
6. Propose fix and flag to Coherence Engine (Skill 0) for impact analysis

## Outputs

This skill produces:
1. **Emotional arc map** — per-session and per-campaign
2. **Engagement model** — short/medium/long-term drivers
3. **Flow state targets** — per phase with intentional disruptors
4. **Player motivation profile** — synthesis across frameworks

These outputs feed into:
- **Skill 7 (Core Loop)** — Loop must deliver the modeled experience
- **Skill 10 (Economy)** — Reward schedules serve engagement drivers
- **Skill 12 (Narrative)** — Narrative serves emotional arc beats
- **Skill 13 (Levels)** — Pacing curves implement the emotional arc
- **Skill 16 (Playtest)** — Playtests verify whether intended emotions land
