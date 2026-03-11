---
name: playtest-protocol-designer
description: >
  Structure playtests to generate actionable data, not just "it was fun" or
  "it wasn't." Use this skill when: (1) planning a playtest session with clear
  objectives, (2) designing observation checklists and post-play questionnaires,
  (3) choosing between playtest types (blind, facilitated, A/B, stress test),
  (4) building data collection plans (quantitative vs. qualitative), (5) creating
  analysis frameworks to interpret results, (6) structuring feedback sessions
  to extract useful information, (7) validating whether the intended experience
  is landing with real players. Medium-agnostic — works for digital playtests,
  tabletop playtests, and hybrid testing.
---

# Playtest Protocol Designer

Playtesting without protocol is just playing. You'll have fun. You'll learn nothing. This skill structures playtests to generate the specific data needed to improve the game.

## Playtest Types

### Blind Playtest
Players receive the game with no explanation from the designer. They read the rules (or tutorial) and play.
- **Tests:** Rulebook clarity, onboarding, independent learnability
- **When:** Rules are drafted, UI/tutorial exists
- **Who:** Players who have never seen the game
- **Designer role:** Silent observer. Do not help. Do not explain. Take notes.

### Facilitated Playtest
Designer teaches the game and observes play, answering questions.
- **Tests:** Core mechanics, balance, engagement, flow
- **When:** Prototype stage, mechanics are functional but rules may be rough
- **Who:** Any players, including familiar ones
- **Designer role:** Teach, then observe. Note every question asked — those are design failures.

### A/B Playtest
Two groups play different versions of the same game element.
- **Tests:** Specific design decisions (version A vs. version B)
- **When:** A specific design question has two viable answers
- **Who:** Comparable skill-level groups
- **Designer role:** Set up both, observe both, compare data.

### Stress Test
Push the game to breaking points deliberately.
- **Tests:** Edge cases, degenerate strategies, scaling limits
- **When:** Core mechanics work but robustness is unknown
- **Who:** Experienced/adversarial players who will try to break things
- **Designer role:** Encourage breaking. "Try to win in the cheapest way possible."

### Focus Test
Players experience a specific element and provide targeted feedback.
- **Tests:** Specific systems, narrative moments, aesthetic impact
- **When:** A particular element needs validation in isolation
- **Who:** Target audience for that element
- **Designer role:** Present the element, ask targeted questions.

## Core Deliverables

### 1. Playtest Objective

Every playtest must have a clear purpose:

```
PLAYTEST ID:     [Identifier — e.g., PT-007]
TYPE:            [Blind / Facilitated / A/B / Stress / Focus]
HYPOTHESIS:      [What we're testing — connected to prototype hypothesis]
QUESTIONS:       [Specific questions this playtest should answer]
NOT TESTING:     [What we're explicitly NOT evaluating this session]
```

**Anti-pattern:** "Let's playtest and see what happens." If you don't know what you're looking for, you won't find it.

### 2. Observation Checklist

What to watch for during play:

**Engagement indicators:**
- [ ] Players are making active decisions (not just going through motions)
- [ ] Players are discussing strategy with each other
- [ ] Players show emotional reactions (excitement, tension, laughter)
- [ ] Players lean forward / show focused body language
- [ ] Players ask "can I do X?" (exploring the possibility space)

**Disengagement indicators:**
- [ ] Players check phones or look away
- [ ] Players ask "whose turn is it?" (lost track of game state)
- [ ] Players make choices without consideration (just picking randomly)
- [ ] Players ask "how much longer?" or "are we almost done?"
- [ ] Silence during what should be exciting moments

**Confusion indicators:**
- [ ] Players ask the same question twice
- [ ] Players make illegal moves without realizing
- [ ] Players misunderstand a rule and play incorrectly
- [ ] Players stare at their options for extended periods
- [ ] Players ask each other for rule clarification instead of the rulebook

**Balance indicators:**
- [ ] One player/strategy pulls ahead early and stays ahead
- [ ] A player feels hopeless before the game ends
- [ ] All players converge on the same strategy
- [ ] A mechanic is used by nobody (dead feature)
- [ ] A mechanic is used by everybody (possibly dominant)

### 3. Post-Play Questionnaire

Targeted questions, not generic. Design these per-playtest.

**Universal questions (use every time):**
1. What was the most fun moment? (identifies peaks)
2. What was the most frustrating moment? (identifies friction)
3. Would you play again? Why or why not? (overall verdict)
4. What confused you? (identifies clarity problems)
5. Did you feel like your decisions mattered? (agency check)

**Hypothesis-specific questions (custom per test):**
- Design 3-5 questions that directly probe the hypothesis being tested
- Use specific language, not vague ("Did you enjoy the random character?" not "Did you like it?")
- Include one question that tests the negative ("What would you change about X?")

**Question design rules:**
- **No leading questions** — "Wasn't the combat exciting?" vs. "How did the combat feel?"
- **No compound questions** — One question, one topic
- **Scale + open-ended** — "Rate combat satisfaction 1-5" THEN "Why that rating?"
- **Behavioral over opinion** — "What did you do when X happened?" vs. "Did you like X?"

### 4. Data Collection Plan

What data to capture and how:

**Quantitative data:**
```
METRIC              HOW CAPTURED       WHAT IT TELLS US
──────────────────  ──────────────── ──────────────────────────
Game duration       Timer              Pacing health
Turns to completion Counter            Loop efficiency
Resource at end     Snapshot           Economy balance
Win margin          Score diff         Competitiveness
Choice distribution Tally marks        Option viability
```

**Qualitative data:**
```
DATA TYPE           HOW CAPTURED       WHAT IT TELLS US
──────────────────  ──────────────── ──────────────────────────
Player reactions    Observer notes     Emotional experience
Questions asked     Written log        Clarity problems
Strategies used     Observer notes     Design space utilization
Table talk          Audio/notes        Social dynamics
Post-game comments  Questionnaire      Reflective assessment
```

### 5. Analysis Framework

How to interpret results after the playtest:

**Pattern identification:**
- Did multiple players encounter the same problem? (Systematic issue)
- Did one player have a unique problem? (Edge case or skill gap)
- Did observed behavior match self-reported experience? (If not, dig deeper)

**Severity classification:**
```
FINDING             SEVERITY          ACTION
──────────────────  ──────────────── ──────────────────────
[Description]       [Critical/Major/  [Immediate fix / Next
                     Minor/Cosmetic]   iteration / Backlog /
                                       Monitor]
```

**Critical:** Prevents play. Game breaks or stops making sense.
**Major:** Significantly harms experience. Players notice and complain.
**Minor:** Small friction. Players notice but continue.
**Cosmetic:** Polish issue. Doesn't affect gameplay.

**Signal vs. noise:** Not every player complaint requires a design change. Look for patterns across multiple playtests, not individual reactions. One player hating a mechanic is data. Five players hating it is a signal.

## Facilitator Guidelines

**Before the test:**
- Set up the game completely before players arrive
- Prepare note-taking materials (paper, forms, or digital)
- Brief observers on what to watch for
- Decide: will you intervene if players are stuck? At what threshold?

**During the test:**
- Resist the urge to explain or defend design choices
- Note the TIME when interesting things happen (for cross-referencing)
- Watch faces as much as the game board/screen
- If you must intervene, note what triggered it — that's a design problem

**After the test:**
- Run the questionnaire immediately (memory fades fast)
- Ask open-ended questions before specific ones
- Don't argue with feedback ("but that's intentional" is not useful)
- Thank players genuinely — their time is valuable

## Workflow

### Planning a playtest

1. **Define the objective** — What question must this test answer?
2. **Choose playtest type** — What type matches the objective?
3. **Build observation checklist** — What to watch for, connected to the objective
4. **Design questionnaire** — Universal + hypothesis-specific questions
5. **Set up data collection** — What metrics, how captured
6. **Recruit players** — Match player profile to test needs
7. **Prepare the prototype** (Skill 15) — Ensure it's ready
8. **Brief observers** — Everyone knows what to watch for
9. **Run the test**
10. **Analyze results** — Pattern identification, severity classification
11. **Report findings** — Actionable items, not just observations
12. **Flag to iteration** (Skill 17) — Log what was found and what changes

### Interpreting ambiguous results

1. Is the sample size sufficient? (1 playtest is anecdotal; 5+ is a pattern)
2. Are players representative of the target audience?
3. Did the prototype fidelity affect results? (Testing the wrong thing)
4. Is this a design problem or a communication problem?
5. Would watching one more test clarify, or is it time to iterate?

## Outputs

This skill produces:
1. **Playtest protocol** — objective, type, checklist, questionnaire, data plan
2. **Observation checklist** — engagement, disengagement, confusion, balance
3. **Post-play questionnaire** — universal + custom questions
4. **Data collection plan** — metrics and capture methods
5. **Analysis framework** — pattern identification and severity classification

These outputs feed into:
- **Skill 11 (Balance)** — Balance hypotheses get tested
- **Skill 17 (Iteration)** — Playtest results drive design changes
- **Skill 4 (Experience)** — Did the intended experience land?
- **Skill 0 (Coherence)** — Results may trigger re-evaluation cascades
