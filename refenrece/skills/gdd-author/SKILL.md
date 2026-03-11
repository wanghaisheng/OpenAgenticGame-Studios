---
name: gdd-author
description: >
  Structure and maintain a living Game Design Document — the single source of
  truth for the game's design. Use this skill when: (1) creating a GDD from
  existing design outputs, (2) structuring a modular, navigable document that
  scales with the project, (3) determining appropriate detail level for
  different audiences (team, publisher, investor), (4) integrating change
  tracking from iteration history, (5) generating section templates per domain,
  (6) ensuring cross-references between sections are maintained.
  Medium-agnostic — works for digital, tabletop, and hybrid games.
---

# GDD Author

The Game Design Document is not a sacred text — it's a living tool. It must be current, navigable, and useful to everyone who reads it. If nobody reads the GDD, the problem is the GDD, not the team.

## GDD Philosophy

**Living document, not monument.** The GDD changes as the design changes. A GDD that's "finished" means the game has shipped or been cancelled.

**Modular, not monolithic.** Nobody reads a 200-page document. The GDD is a collection of sections that can be read independently.

**Audience-aware.** Different readers need different things. A programmer needs systems specs. A publisher needs vision and market. An artist needs aesthetic direction. Write for your readers.

**Source of truth, not source of everything.** The GDD links to detailed documents — it doesn't contain every balance spreadsheet and level blueprint. It provides the definitive overview and points to depth.

## GDD Structure

### Master Template

```
1. OVERVIEW
   1.1 Vision Statement (from Skill 1)
   1.2 Elevator Pitch (from Skill 5)
   1.3 Core Fantasy
   1.4 Target Audience
   1.5 Platform / Medium
   1.6 Current Status / Version

2. IDENTITY
   2.1 Design Pillars (from Skill 2)
   2.2 Aesthetic Direction Summary (from Skill 3)
   2.3 Comparison Frame & References

3. PLAYER EXPERIENCE
   3.1 Emotional Arc (from Skill 4)
   3.2 Engagement Model
   3.3 Flow Targets
   3.4 Player Motivation Profile

4. CORE GAMEPLAY
   4.1 Core Loop Diagram (from Skill 7)
   4.2 Loop Hierarchy (micro, core, session, meta)
   4.3 Key Mechanics Summary
   4.4 Rules Overview (from Skill 8, summary — full rules linked)

5. SYSTEMS
   5.1 Systems Interaction Map (from Skill 9)
   5.2 Economy & Progression Overview (from Skill 10)
   5.3 Balance Framework (from Skill 11)

6. CONTENT
   6.1 Narrative Systems (from Skill 12)
   6.2 Level/Encounter Overview (from Skill 13)
   6.3 World Logic Summary (from Skill 14)

7. INTERFACE
   7.1 UI/UX Design (from Skill 18)
   7.2 Information Hierarchy
   7.3 Onboarding Plan

8. PRODUCTION
   8.1 Scope & Priority (from Skill 20)
   8.2 Technical Requirements (from Skill 21)
   8.3 Prototype Status (from Skill 15)
   8.4 Playtest History (from Skill 16)
   8.5 Iteration Log (from Skill 17)

9. APPENDICES
   9.1 Full Rules Document (linked)
   9.2 Balance Spreadsheets (linked)
   9.3 Level Blueprints (linked)
   9.4 Art/Audio Reference Board (linked)
   9.5 Glossary
```

### Section Templates

Each section follows a consistent format:

```
## [Section Title]

### Summary
[2-3 sentences — the essential takeaway]

### Current State
[What's decided, what's in progress, what's open]

### Details
[The substance — varies by section type]

### Open Questions
[What hasn't been decided yet?]

### Change History
[Recent changes to this section, linked to iteration log]

### Cross-References
[Which other sections this connects to]
```

## GDD Variants

Not every project needs the full template. Scale to fit.

### Game Jam GDD (1-2 pages)
- Vision statement
- Core loop diagram
- 3-5 pillars
- Key mechanics list
- Scope definition (what's in, what's out)

### Indie GDD (5-15 pages)
- Full Overview and Identity sections
- Core Gameplay section
- Abbreviated Systems and Content
- Scope and priorities
- No formal appendices (working docs serve as reference)

### Publisher Pitch GDD (10-20 pages)
- Heavy on Overview, Identity, and Player Experience
- Market positioning and competitive analysis
- Visual/audio references and concept art
- Production timeline and budget overview
- Light on technical details

### Full Production GDD (20-50+ pages, modular)
- All sections fully developed
- Linked appendices with full detail documents
- Change tracking integrated
- Multiple audience views (design view, engineering view, art view)

## Writing Quality Guidelines

**Be specific, not aspirational.** "The combat system uses a 2d6 + modifier resolution with opposed rolls" not "The combat system is deep and engaging."

**Use examples liberally.** Every abstract concept should have a concrete instance. "Resources are scarce" becomes "At session start, players have 5 gold. A basic weapon costs 3. A health potion costs 2. They must choose."

**Define before using.** Every game term should be defined the first time it appears and listed in the glossary.

**Write for scan-reading.** Use headers, bullet points, bold key terms, and summaries. Nobody reads a GDD linearly — they search for what they need.

**Date everything.** Every section should show when it was last updated. Stale sections should be flagged.

**Kill filler text.** If a section says nothing specific ("the economy will be robust and balanced"), delete it until there's real content to fill it with.

## Workflow

### Creating a GDD from existing design outputs

1. **Gather all skill outputs** — Vision, pillars, aesthetic, experience, loop, rules, systems, economy, balance, narrative, levels, world, UI, scope, tech
2. **Choose the GDD variant** — Match project scale and audience
3. **Write summaries first** — Every section starts with a 2-3 sentence summary
4. **Fill in details** — Expand from skill outputs
5. **Add cross-references** — Link related sections
6. **Flag open questions** — What hasn't been decided?
7. **Link appendices** — Point to detailed documents for depth
8. **Review for audience** — Can each reader find what they need?

### Maintaining the GDD

1. When any skill output changes, update the corresponding GDD section
2. Mark change date and link to iteration log (Skill 17)
3. Flag stale sections (not updated in 30+ days for active projects)
4. Periodically review for consistency across sections
5. The GDD is the responsibility of the design lead, not a committee

### Using the GDD in practice

- **Team alignment meetings** — Reference specific sections
- **Onboarding** — New members read Overview and Identity first, then their domain
- **Decision making** — "Does this serve our pillars?" (section 2.1)
- **Publisher communication** — Extract the Pitch GDD variant
- **Scope discussions** — Reference section 8.1 (Scope & Priority)

## Anti-Patterns

**The Museum Piece** — A GDD written once and never updated. Becomes fiction within weeks.

**The Novel** — So long that nobody reads it. The GDD should be scannable, not a reading assignment.

**The Wish List** — Full of aspirational features without constraints, priorities, or trade-offs.

**The Committee Draft** — Written by consensus with no voice, full of hedged language and non-commitments.

**The Secret Document** — A GDD that exists but nobody can find, access, or navigate.

## Outputs

This skill produces:
1. **GDD structure** — modular, navigable, audience-appropriate
2. **Section templates** — consistent format per domain
3. **GDD variant selection** — scaled to project needs
4. **Cross-reference system** — sections linked to related sections
5. **Maintenance protocol** — how and when to update

These outputs integrate:
- **All skills** — The GDD synthesizes outputs from every active skill
- **Skill 17 (Iteration)** — Change tracking feeds GDD updates
- **Skill 0 (Coherence)** — GDD is the readable expression of design coherence
