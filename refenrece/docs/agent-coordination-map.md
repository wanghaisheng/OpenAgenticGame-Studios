# Agent Coordination and Delegation Map

## 🏗️ Team-Based Organizational Hierarchy

```
                           [Human Developer]
                                 |
                 +---------------+---------------+---------------+
                 |               |               |               |
         creative-director  technical-director  producer  game-vision-architect
                 |               |               |               |
        +--------+--------+     |        +--------+--------+     |
        |        |        |     |        |        |        |     |
  game-designer art-dir  narr-dir  audio-dir  lead-programmer  qa-lead  localization-lead
        |        |        |     |        |        |        |     |
     +--+--+     |     +--+--+  +--+--+  +--+--+--+--+--+   |        |
     |  |  |     |     |     |  |  |  |  |  |  |  |   |        |
    sys lvl eco  ta   wrt  wrld gp ep  ai net tl ui qa-t    snd    release-manager
        |        |        |     |        |        |        |        |
     +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
     |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
    perf-a  devops  analytics  comm  security  prototyper  access  live-ops  enhanced
```

## 🎯 Team Structure Overview

### **Leadership Team** (7 agents)
- **creative-director** - Creative vision and artistic direction
- **technical-director** - Technical strategy and architecture
- **producer** - Project management and delivery
- **art-director** - Visual direction and art standards
- **audio-director** - Audio direction and sound design
- **narrative-director** - Story & narrative vision
- **game-vision-architect** - Long-term vision and strategy

### **Programming Team** (28 agents)
- **lead-programmer** - Technical leadership and code standards
- **Core Programmers**: gameplay-programmer, engine-programmer, ai-programmer, network-programmer, ui-programmer, tools-programmer
- **Unity Specialists**: unity-specialist, unity-dots-specialist, unity-addressables-specialist, unity-shader-specialist, unity-ui-specialist, unity-development-specialist, unity-skills-automation, unity-asset-guidelines-specialist
- **Godot Specialists**: godot-specialist, godot-gdscript-specialist, godot-gdextension-specialist, godot-shader-specialist, godot-full-stack-specialist
- **Unreal Specialists**: unreal-specialist, ue-blueprint-specialist, ue-gas-specialist, ue-replication-specialist, ue-umg-specialist
- **Cocos Specialists**: cocos-creator-specialist, cocos-skills-automation
- **Skill Specialists**: skill-creation-specialist

### **Design Team** (12 agents)
- **game-designer** - Core mechanics design
- **systems-designer** - Game systems design
- **level-designer** - Level creation and layout
- **economy-designer** - Economy systems and balance
- **world-builder** - World creation and lore
- **writer** - Narrative content and dialogue
- **live-ops-designer** - Live events and retention
- **Design Framework**: narrative-game-generator, aesthetic-direction-framework, core-loop-designer, design-coherence-engine, competitive-analysis-specialist

### **Art Team** (10 agents)
- **technical-artist** - Technical art pipeline and shaders
- **ux-designer** - User experience design
- **accessibility-specialist** - Accessibility and inclusive design
- **sound-designer** - Audio effects and music
- **Enhanced Art**: enhanced-technical-artist, enhanced-sound-designer, enhanced-ui-specialist, enhanced-ux-designer, enhanced-art-director, enhanced-composer

### **Quality Assurance Team** (6 agents)
- **qa-lead** - QA coordination and strategy
- **qa-tester** - Testing execution and bug reporting
- **performance-analyst** - Performance monitoring and optimization
- **game-quality-gates-specialist** - Quality standards and gates
- **Enhanced QA**: enhanced-qa-tester, enhanced-performance-analyst

### **Production Team** (12 agents)
- **release-manager** - Release pipeline and deployment
- **localization-lead** - Internationalization and translation
- **community-manager** - Community engagement and support
- **analytics-engineer** - Player analytics and data analysis
- **devops-engineer** - CI/CD and infrastructure
- **security-engineer** - Security and anti-cheat
- **prototyper** - Rapid prototyping and validation
- **Enhanced Production**: enhanced-release-manager, enhanced-community-manager, enhanced-devops-engineer, enhanced-security-engineer, enhanced-prototyper

### **Support Team** (2 agents)
- **enhanced-analytics-engineer** - Advanced analytics and insights
- **enhanced-network-engineer** - Network architecture and optimization

### **Enhanced Team** (4 agents)
- **enhanced-game-designer** - Advanced game design capabilities
- **enhanced-tool-developer** - Advanced tool development
- **enhanced-art-director** - Advanced art direction
- **enhanced-network-engineer** - Advanced network engineering

  Additional Leads (report to producer/directors):
    release-manager         -- Release pipeline, versioning, deployment
    localization-lead       -- i18n, string tables, translation pipeline
    prototyper              -- Rapid throwaway prototypes, concept validation
    security-engineer       -- Anti-cheat, exploits, data privacy, network security
    accessibility-specialist -- WCAG, colorblind, remapping, text scaling
    live-ops-designer       -- Seasons, events, battle passes, retention, live economy
    community-manager       -- Patch notes, player feedback, crisis comms

  Engine Specialists (use the SET matching your engine):
    unreal-specialist  -- UE5 lead: Blueprint/C++, GAS overview, UE subsystems
      ue-gas-specialist         -- GAS: abilities, effects, attributes, tags, prediction
      ue-blueprint-specialist   -- Blueprint: BP/C++ boundary, graph standards, optimization
      ue-replication-specialist -- Networking: replication, RPCs, prediction, bandwidth
      ue-umg-specialist         -- UI: UMG, CommonUI, widget hierarchy, data binding

    unity-specialist   -- Unity lead: MonoBehaviour/DOTS, Addressables, URP/HDRP
      unity-dots-specialist         -- DOTS/ECS: Jobs, Burst, hybrid renderer
      unity-shader-specialist       -- Shaders: Shader Graph, VFX Graph, SRP customization
      unity-addressables-specialist -- Assets: async loading, bundles, memory, CDN
      unity-ui-specialist           -- UI: UI Toolkit, UGUI, UXML/USS, data binding

    godot-specialist   -- Godot 4 lead: GDScript, node/scene, signals, resources
      godot-gdscript-specialist    -- GDScript: static typing, patterns, signals, performance
      godot-shader-specialist      -- Shaders: Godot shading language, visual shaders, VFX
      godot-gdextension-specialist -- Native: C++/Rust bindings, GDExtension, build systems
```

### Legend
```
sys  = systems-designer       gp  = gameplay-programmer
lvl  = level-designer         ep  = engine-programmer
eco  = economy-designer       ai  = ai-programmer
ta   = technical-artist       net = network-programmer
wrt  = writer                 tl  = tools-programmer
wrld = world-builder          ui  = ui-programmer
snd  = sound-designer         qa-t = qa-tester
narr-dir = narrative-director perf-a = performance-analyst
art-dir = art-director        comm = community-manager
access = accessibility-specialist prototyper = prototyper
enhanced = enhanced-* agents
```

## 🔄 Team-Based Delegation Rules

### **Leadership Team Delegation**

| From | Can Delegate To | Scope |
|------|----------------|-------|
| **creative-director** | game-designer, art-director, audio-director, narrative-director, game-vision-architect | Creative vision and artistic decisions |
| **technical-director** | lead-programmer, devops-engineer, performance-analyst, technical-artist, all programming teams | Technical architecture and standards |
| **producer** | All team leads and specialists | Task assignment and project coordination |
| **game-vision-architect** | creative-director, technical-director, game-designer | Long-term vision alignment |

### **Team Lead Delegation**

| From | Can Delegate To | Scope |
|------|----------------|-------|
| **lead-programmer** | All programming team members | Code architecture, implementation, code review |
| **game-designer** | systems-designer, level-designer, economy-designer, world-builder, writer | Design implementation and content creation |
| **art-director** | technical-artist, ux-designer, accessibility-specialist | Visual direction and art standards |
| **qa-lead** | qa-tester, performance-analyst, game-quality-gates-specialist | Testing strategy and quality assurance |
| **release-manager** | devops-engineer, localization-lead, community-manager | Release pipeline and deployment |
| **localization-lead** | writer, ui-programmer, technical-artist | Translation and text fitting |

### **Specialist Delegation**

| From | Can Delegate To | Scope |
|------|----------------|-------|
| **unity-specialist** | All Unity sub-specialists | Unity-specific implementation |
| **godot-specialist** | All Godot sub-specialists | Godot-specific implementation |
| **unreal-specialist** | All Unreal sub-specialists | Unreal-specific implementation |
| **live-ops-designer** | economy-designer, community-manager, analytics-engineer | Live events and retention |
| **enhanced-* agents** | Standard agents | Advanced capabilities and complex tasks |

### **Team-Based Escalation Paths**

| Situation | Escalate To | Team |
|-----------|------------|------|
| Two designers disagree on a mechanic | game-designer | Design Team |
| Game design vs narrative conflict | creative-director | Leadership Team |
| Game design vs technical feasibility | producer (facilitates), then creative-director + technical-director | Leadership Team |
| Art vs audio tonal conflict | creative-director | Leadership Team |
| Code architecture disagreement | technical-director | Leadership Team |
| Cross-system code conflict | lead-programmer, then technical-director | Programming Team |
| Schedule conflict between departments | producer | Production Team |
| Scope exceeds capacity | producer, then creative-director for cuts | Leadership Team |
| Quality gate disagreement | qa-lead, then technical-director | QA + Leadership Teams |
| Performance budget violation | performance-analyst flags, technical-director decides | QA + Programming Teams |
| Engine-specific technical issue | [engine]-specialist, then technical-director | Programming Team |
| Cross-team coordination issue | producer | Production Team |

## 🚀 Team-Based Workflow Patterns

### **Pattern 1: New Feature (Full Pipeline)**
```
1. creative-director      -- Approves feature concept aligns with vision
2. game-designer         -- Creates design document with full spec
3. producer              -- Schedules work, identifies dependencies
4. technical-director    -- Reviews technical feasibility
5. lead-programmer        -- Designs code architecture, creates interface sketch
6. [specialist-programmer] -- Implements the feature
7. technical-artist      -- Implements visual effects (if needed)
8. writer                -- Creates text content (if needed)
9. sound-designer        -- Creates audio event list (if needed)
10. qa-lead               -- Reviews and approves test coverage
11. lead-programmer        -- Code review
12. qa-tester             -- Executes tests
13. producer              -- Marks task complete
```

### **Pattern 2: Bug Fix**
```
1. qa-tester              -- Files bug report with @refenrece/agents/qa/bug-report.md
2. qa-lead                -- Triages severity and priority
3. producer               -- Assigns to sprint (if not S1)
4. lead-programmer         -- Identifies root cause, assigns to programmer
5. [specialist-programmer] -- Fixes the bug
6. lead-programmer         -- Code review
7. qa-tester              -- Verifies fix and runs regression
8. qa-lead                -- Closes bug
```

### **Pattern 3: Balance Adjustment**
```
1. analytics-engineer     -- Identifies imbalance from data (or player reports)
2. game-designer          -- Evaluates the issue against design intent
3. economy-designer       -- Models the adjustment
4. game-designer          -- Approves the new values
5. [data file update]    -- Change configuration values
6. qa-tester              -- Regression test affected systems
7. analytics-engineer     -- Monitor post-change metrics
```

### **Pattern 4: New Area/Level**
```
1. narrative-director      -- Defines narrative purpose and beats for the area
2. world-builder           -- Creates lore and environmental context
3. level-designer         -- Designs layout, encounters, pacing
4. game-designer          -- Reviews mechanical design of encounters
5. art-director           -- Defines visual direction for the area
6. audio-director         -- Defines audio direction for the area
7. [implementation by relevant programmers and artists]
8. writer                 -- Creates area-specific text content
9. qa-tester              -- Tests the complete area
```

### **Pattern 5: Sprint Cycle**
```
1. producer               -- Plans sprint with @refenrece/agents/production/sprint-plan.md
2. [All agents]         -- Execute assigned tasks
3. producer               -- Daily status with @refenrece/agents/production/sprint-plan.md status
4. qa-lead                -- Continuous testing during sprint
5. lead-programmer         -- Continuous code review during sprint
6. producer               -- Sprint retrospective with post-sprint hook
7. producer               -- Plans next sprint incorporating learnings
```

### **Pattern 6: Milestone Checkpoint**
```
1. producer               -- Runs @refenrece/agents/production/milestone-review.md
2. creative-director      -- Reviews creative progress
3. technical-director     -- Reviews technical health
4. qa-lead                -- Reviews quality metrics
5. producer               -- Facilitates go/no-go discussion
6. [All directors]       -- Agree on scope adjustments if needed
7. producer               -- Documents decisions and updates plans
```

### **Pattern 7: Release Pipeline**
```text
1. producer                 -- Declares release candidate, confirms milestone criteria met
2. release-manager          -- Cuts release branch, generates @refenrece/agents/production/release-checklist.md
3. qa-lead                 -- Runs full regression, signs off on quality
4. localization-lead       -- Verifies all strings translated, text fitting passes
5. performance-analyst     -- Confirms performance benchmarks within targets
6. devops-engineer         -- Builds release artifacts, runs deployment pipeline
7. release-manager          -- Generates @refenrece/agents/production/changelog.md, tags release, creates release notes
8. technical-director      -- Final sign-off on major releases
9. release-manager          -- Deploys and monitors for 48 hours
10. producer                -- Marks release complete
```

### **Pattern 8: Rapid Prototype**
```text
1. game-designer           -- Defines the hypothesis and success criteria
2. prototyper              -- Scaffolds prototype with @refenrece/agents/production/prototype.md
3. prototyper              -- Builds minimal implementation (hours, not days)
4. game-designer           -- Evaluates prototype against criteria
5. prototyper              -- Documents findings report
6. creative-director       -- Go/no-go decision on proceeding to production
7. producer                -- Schedules production work if approved
```

### **Pattern 9: Live Event / Season Launch**
```text
1. live-ops-designer        -- Designs event/season content, rewards, schedule
2. game-designer            -- Validates gameplay mechanics for event
3. economy-designer         -- Balances event economy and reward values
4. narrative-director       -- Provides seasonal narrative theme
5. writer                  -- Creates event descriptions and lore
6. producer                -- Schedules implementation work
7. [implementation by relevant programmers]
8. qa-lead                  -- Test event flow end-to-end
9. community-manager        -- Drafts event announcement and patch notes
10. release-manager         -- Deploys event content
11. analytics-engineer      -- Monitors event participation and metrics
12. live-ops-designer       -- Post-event analysis and learnings
```

### **Pattern 10: Engine-Specific Implementation**
```
1. [engine]-specialist    -- Reviews implementation requirements
2. [engine] sub-specialist -- Implements engine-specific features
3. lead-programmer         -- Reviews integration with core systems
4. qa-lead                  -- Tests engine-specific functionality
5. technical-director      -- Validates engine best practices
```

## 📋 Cross-Domain Communication Protocols

### **Design Change Notification**

When a design document changes, the game-designer must notify:
- lead-programmer (implementation impact)
- qa-lead (test plan update needed)
- producer (schedule impact assessment)
- Relevant specialist agents depending on the change

### **Architecture Change Notification**

When an ADR is created or modified, the technical-director must notify:
- lead-programmer (code changes needed)
- All affected specialist programmers
- qa-lead (testing strategy may change)
- producer (schedule impact)

### **Asset Standard Change Notification**

When the art bible or asset standards change, the art-director must notify:
- technical-artist (pipeline changes)
- All content creators working with affected assets
- devops-engineer (if build pipeline is affected)

### **Team-Based Communication**

#### **Leadership Team Coordination**
- **Weekly sync**: All directors meet to align on project direction
- **Decision documentation**: All major decisions documented in shared space
- **Cross-team issues**: Producer facilitates cross-team conflict resolution

#### **Programming Team Coordination**
- **Daily standups**: Lead programmer coordinates daily with all programmers
- **Code reviews**: Mandatory code reviews for all code changes
- **Engine sync**: Regular sync between engine specialists

#### **Design Team Coordination**
- **Design reviews**: Regular design reviews with game-designer as lead
- **Content planning**: Coordinated planning between design specialists
- **Narrative alignment**: Narrative director ensures narrative consistency

#### **Art Team Coordination**
- **Art reviews**: Art director leads regular art reviews
- **Pipeline coordination**: Technical artist coordinates with programming team
- **Asset standards**: Regular updates to art bible and standards

#### **Quality Coordination**
- **Quality meetings**: QA lead coordinates with all teams on quality metrics
- **Bug triage**: Daily bug triage meetings with development teams
- **Performance monitoring**: Performance analyst monitors and reports to all teams

## ⚠️ Team-Based Anti-Patterns to Avoid

1. **Bypassing the hierarchy**: A specialist agent should never make decisions
   that belong to their team lead without consultation.

2. **Cross-domain implementation**: An agent should never modify files outside
   their designated team area without explicit delegation from the relevant team lead.

3. **Shadow decisions**: All decisions must be documented. Verbal agreements
   without written records lead to contradictions.

4. **Monolithic tasks**: Every task assigned to an agent should be completable
   in 1-3 days. If it is larger, it must be broken down first.

5. **Assumption-based implementation**: If a spec is ambiguous, the implementer
   must ask the specifier rather than guessing. Wrong guesses are more expensive
   than a question.

6. **Team isolation**: Teams should not work in isolation. Regular cross-team
   communication is essential for project success.

7. **Decision paralysis**: Avoid endless meetings. Make decisions with available
   information and document them for later reference.

8. **Resource hoarding**: Teams should not hoard specialists or information.
   Share resources and knowledge across teams as needed.

## 🎯 Team Success Metrics

### **Team Performance Indicators**

| Team | Key Metrics | Success Criteria |
|------|-------------|----------------|
| **Leadership** | Vision clarity, decision speed, team alignment | 95%+ team satisfaction |
| **Programming** | Code quality, feature delivery, bug fix time | 90%+ code quality standards |
| **Design** | Design quality, iteration speed, player feedback | 85%+ positive feedback |
| **Art** | Asset quality, visual consistency, delivery time | 90%+ visual consistency |
| **QA** | Bug detection rate, test coverage, release quality | 95%+ bug detection |
| **Production** | Release frequency, deployment success, uptime | 99%+ deployment success |

### **Cross-Team Collaboration Metrics**

| Metric | Target | Measurement |
|--------|--------|------------|
| **Cross-team meetings** | Weekly | Attendance and participation |
| **Documentation completeness** | 100% | All decisions documented |
| **Knowledge sharing** | 80%+ | Regular cross-team knowledge sharing |
| **Conflict resolution time** | < 24 hours | Quick and effective resolution |

---

## 🎉 **Team-Based Coordination Map Summary**

### **Updated Structure**
- **8 Teams**: Leadership, Programming, Design, Art, QA, Production, Support, Enhanced
- **79 Agents**: All agents organized by team structure
- **Clear Hierarchy**: Defined reporting lines and delegation rules
- **Team Coordination**: Cross-team communication protocols

### **Key Improvements**
- **Team-Based Organization**: Clear team structure and responsibilities
- **Enhanced Delegation**: Team-specific delegation rules and escalation paths
- **Workflow Optimization**: Team-aligned workflow patterns
- **Communication Protocols**: Clear cross-team communication guidelines

### **Benefits**
- **Clear Responsibilities**: Each team has clear ownership and accountability
- **Efficient Delegation**: Optimized delegation rules reduce bottlenecks
- **Better Coordination**: Cross-team communication protocols improve collaboration
- **Quality Assurance**: Team-based quality gates ensure high standards

---

*Agent Coordination Map Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Organization: Team-Based Structure*
*Total Teams: 8*
*Total Agents: 79*
*Hierarchy: Clear and Defined*
