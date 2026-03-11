---
name: ui-ux-systems-designer
description: >
  Design the information architecture and interaction model — how the player
  reads game state and provides input. The interface between the player's brain
  and the game's systems. Use this skill when: (1) designing information
  hierarchy (what the player needs to know, in what order), (2) defining input
  models (how players express intent), (3) designing feedback language (how the
  game communicates outcomes), (4) managing cognitive load, (5) planning
  accessibility features, (6) designing onboarding and tutorial flows,
  (7) creating player aids for tabletop games. Distinct from aesthetic direction
  — this is about communication and usability, not sensory identity.
  Medium-agnostic — works for digital UI, tabletop graphic design, and hybrid.
---

# UI/UX Systems Designer

UI is the conversation between the player and the game. The game speaks through visual, audio, and tactile feedback. The player speaks through inputs. If the conversation is unclear, the game fails regardless of how good the design underneath is.

## UI vs. UX vs. Aesthetic

**UI (User Interface)** — The elements the player interacts with. Buttons, menus, cards, boards, dice, HUD.

**UX (User Experience)** — How it *feels* to interact. Clarity, flow, satisfaction, frustration.

**Aesthetic Direction** (Skill 3) — How it *looks and sounds*. Style, mood, identity.

UI/UX serves clarity and function. Aesthetic serves identity and emotion. They must work together but are designed with different priorities. A beautiful interface that's confusing fails. A clear interface that's ugly succeeds functionally but misses emotionally.

## Core Deliverables

### 1. Information Hierarchy

What does the player need to know, in what order of priority?

```
PRIORITY    INFORMATION              ALWAYS VISIBLE?   HOW COMMUNICATED
──────────  ──────────────────────── ──────────────── ────────────────────
Critical    [Must know NOW]          Yes               [Method]
Important   [Need to know soon]      Yes/On demand     [Method]
Useful      [Helpful to know]        On demand          [Method]
Reference   [Occasionally needed]    Hidden until asked [Method]
```

**Communication methods:**
- **Persistent display** — Always on screen/board (HP bar, score, resource counters)
- **Contextual display** — Appears when relevant (damage numbers, range indicators)
- **On-demand display** — Player requests it (inventory, map, detailed stats)
- **Ambient display** — Communicated through game world, not UI (low health = red screen tint, resource scarcity = visual change in environment)

**Information hierarchy principles:**
- **Less is more** — Every element on screen competes for attention
- **Progressive disclosure** — Show basics first, details on demand
- **Spatial consistency** — Same info always in the same place
- **Hierarchy through size/color/position** — Most important = largest, most prominent

### 2. Input Model

How does the player express intent?

**Digital inputs:**
```
ACTION              INPUT               FEEDBACK          FEEL TARGET
──────────────────  ──────────────────  ──────────────── ──────────────
[Player action]     [Button/gesture/    [What confirms    [How should this
                     mouse/voice]        the input?]       feel?]
```

**Tabletop inputs:**
```
ACTION              PHYSICAL ACTION     GAME STATE CHANGE SOCIAL SIGNAL
──────────────────  ──────────────────  ──────────────── ──────────────
[Player action]     [What they do       [What changes     [What other
                     physically]          on the table?]    players see]
```

**Input quality checklist:**
- [ ] Every action has exactly one input (no ambiguity about how to do something)
- [ ] Frequent actions require less effort than rare ones
- [ ] Destructive actions require confirmation (or are reversible)
- [ ] Input and feedback are temporally connected (no mystery delays)
- [ ] The input method matches the action's importance (big actions deserve deliberate inputs)

### 3. Feedback Language

How does the game communicate outcomes to the player?

**Feedback types:**
- **Confirmation** — "Your action was received" (button press visual, card placement sound)
- **Result** — "Here's what happened" (damage number, resource change, board state update)
- **Consequence** — "Here's what this means" (health bar change, victory point update)
- **Anticipation** — "Here's what's coming" (enemy telegraph, timer, warning indicator)

**Feedback channels:**
- **Visual** — Color, animation, particle effects, UI changes, card state
- **Audio** — Sound effects, music changes, silence
- **Haptic** — Controller vibration, card weight, dice feel
- **Spatial** — Camera movement, board state change, token positioning

**Feedback design rules:**
- Every player action must produce visible/audible feedback within 100ms (digital) or immediately (tabletop)
- Positive outcomes feel different from negative outcomes
- The magnitude of feedback matches the magnitude of the event
- Repeated feedback doesn't become annoying (satisfying on repetition 100, not just repetition 1)

### 4. Cognitive Load Management

How much information is the player processing at once?

**Cognitive load types:**
- **Intrinsic** — Complexity inherent to the game (many systems, complex rules)
- **Extraneous** — Complexity added by poor UI (confusing layout, unclear icons)
- **Germane** — Productive mental effort (strategic thinking, planning)

**The goal:** Minimize extraneous load. Manage intrinsic load. Maximize germane load. The player should be thinking about strategy, not about how to read the interface.

**Load management techniques:**
- **Chunking** — Group related info visually (all combat stats together, all economy stats together)
- **Progressive disclosure** — Don't show everything at once
- **Consistent patterns** — Same type of info always looks the same
- **Visual encoding** — Color = type, size = importance, position = category
- **Defaults and presets** — Reduce choices when possible
- **Undo support** — Reduce decision anxiety by allowing reversal

**Cognitive load audit:**
```
SCREEN/STATE        ELEMENTS VISIBLE    DECISIONS REQUIRED    LOAD LEVEL
──────────────────  ──────────────────  ──────────────────── ──────────
[Game state]        [Count of elements] [Count of decisions]  [Low/Med/High]
```

Any state with High load should be scrutinized — can elements be hidden, grouped, or deferred?

### 5. Accessibility Design

Design for the widest possible audience:

**Visual accessibility:**
- Colorblind-safe palettes (don't rely on color alone — use shape, pattern, or label)
- Scalable text / component size
- High contrast mode
- Screen reader support (digital)
- Clear iconography that doesn't require color vision

**Motor accessibility:**
- Remappable controls (digital)
- Adjustable timing (digital)
- One-handed play options
- Large touch targets
- Component handling alternatives (tabletop — card holders, dice rollers)

**Cognitive accessibility:**
- Tutorial/help always available
- Game state summaries on demand
- Undo/replay support
- Difficulty options
- Player aids and reference cards (tabletop)

### 6. Onboarding/Tutorial Design

How does a new player learn the interface and game?

**Onboarding principles:**
- **Teach through play, not text** — The best tutorial is a simplified version of the real game
- **One concept at a time** — Introduce mechanic, let player practice, then add next
- **Fail safely** — Early mistakes should be recoverable
- **Show, don't tell** — Visual demonstration over written explanation
- **Let players skip** — Experienced players should never be trapped in a tutorial

**Onboarding structure:**
```
STEP    CONCEPT INTRODUCED     HOW TAUGHT           SUCCESS CHECK
──────  ────────────────────── ──────────────────── ──────────────────
1       [Core input]           [Guided action]       [Player does it]
2       [Core feedback]        [Result shown]        [Player reads it]
3       [First decision]       [Simple choice]       [Player chooses]
4       [Core loop complete]   [Full cycle played]   [Player understands]
...
```

**Tabletop onboarding:**
- First game setup guide (simplified rules for game 1)
- Player aid cards (quick reference during play)
- Glossary on back of rulebook
- "Your first game" walkthrough in rules

## Medium-Specific Considerations

### Digital
- HUD design (what's persistent, what's contextual)
- Menu architecture (navigation depth, back-button behavior)
- Control mapping (button assignment, gesture library)
- Camera as UI (what the camera shows IS information)
- Loading screen utility (tips, lore, progress)

### Tabletop
- Board layout (information zones, player areas, shared areas)
- Card design (information hierarchy top-to-bottom, readability at arm's length)
- Iconography system (consistent symbols across all components)
- Player aid design (what goes on the reference card?)
- Rulebook as UI (structure, indexing, examples, FAQ)
- Component as information carrier (color, shape, size encode game state)

## Workflow

### Designing UI/UX for a new game

1. **Define information hierarchy** — What matters most?
2. **Design input model** — How does the player act?
3. **Design feedback language** — How does the game respond?
4. **Audit cognitive load** — Is there too much at once?
5. **Plan accessibility** — Who might be excluded?
6. **Design onboarding** — How does a new player learn?
7. **Cross-check with aesthetic direction** (Skill 3) — UI must fit the visual identity
8. **Cross-check with core loop** (Skill 7) — UI surfaces the loop moment-to-moment
9. **Cross-check with rules** (Skill 8) — UI must communicate rules clearly
10. **Prototype and test** (Skills 13, 14) — UI/UX problems only surface in use

## Outputs

This skill produces:
1. **Information hierarchy** — priority-ordered display plan
2. **Input model** — how players express intent per action
3. **Feedback language** — how the game communicates per channel
4. **Cognitive load audit** — per-state complexity assessment
5. **Accessibility plan** — visual, motor, cognitive accommodations
6. **Onboarding design** — step-by-step tutorial structure

These outputs feed into:
- **Skill 7 (Core Loop)** — UI surfaces the loop
- **Skill 8 (Rules)** — UI communicates rules
- **Skill 3 (Aesthetic)** — UI must fit sensory identity
- **Skill 15 (Prototype)** — Prototype needs enough UI to test
- **Skill 21 (Tech Bridge)** — UI has implementation requirements
- **Skill 19 (GDD)** — UI/UX is a core GDD section
