# Game Studio Agent Architecture -- Quick Start Guide

## 🎯 What Is This?

This is a complete Claude Code agent architecture for game development. It
organizes **79 specialized AI agents** into a studio hierarchy that mirrors
real game development teams, with defined responsibilities, delegation
rules, and coordination protocols. It includes engine-specialist agents
for Unity, Godot, Unreal, and Cocos Creator — each with dedicated sub-specialists for
major engine subsystems. All design agents and templates are grounded in
established game design theory (MDA Framework, Self-Determination Theory,
Flow State, Bartle Player Types). Use whichever engine set matches your project.

## 🏗️ Team-Based Organization

### **8 Teams** - Complete Studio Structure

1. **Leadership Team** (7 agents) - Project vision and strategic direction
2. **Programming Team** (28 agents) - Technical implementation and engine expertise
3. **Design Team** (12 agents) - Game design and content creation
4. **Art Team** (10 agents) - Visual art and user experience
5. **Quality Assurance Team** (6 agents) - Testing and quality control
6. **Production Team** (12 agents) - Project management and operations
7. **Support Team** (2 agents) - Advanced technical support
8. **Enhanced Team** (4 agents) - Enhanced capabilities

## 🚀 How to Use

### **1. Understand the Team Structure**

Think in terms of real game development teams:

- **Leadership Team**: Makes high-level strategic decisions
  - `creative-director` -- vision and creative conflict resolution
  - `technical-director` -- architecture and technology decisions
  - `producer` -- scheduling, coordination, and risk management
  - `art-director` -- visual direction and art standards
  - `audio-director` -- audio direction and sound design
  - `narrative-director` -- story and narrative vision
  - `game-vision-architect` -- long-term vision and strategy

- **Team Leads**: Own their domain and coordinate team members
  - Programming: `lead-programmer`
  - Design: `game-designer`
  - Art: `art-director`
  - QA: `qa-lead`
  - Production: `release-manager`, `localization-lead`

- **Specialists**: Execute specific tasks within their domain
  - Programmers, designers, artists, writers, testers, engineers

### **2. Pick the Right Team Agent**

Ask yourself: "What team would handle this in a real studio?"

| I need to... | Use this team/agent |
|-------------|-------------------|
| **Design a new mechanic** | Design Team → `game-designer` |
| **Write combat code** | Programming Team → `gameplay-programmer` |
| **Create a shader** | Art Team → `technical-artist` |
| **Write dialogue** | Design Team → `writer` |
| **Plan the next sprint** | Production Team → `producer` |
| **Review code quality** | Programming Team → `lead-programmer` |
| **Write test cases** | QA Team → `qa-tester` |
| **Design a level** | Design Team → `level-designer` |
| **Fix performance problem** | QA Team → `performance-analyst` |
| **Set up CI/CD** | Production Team → `devops-engineer` |
| **Design a loot table** | Design Team → `economy-designer` |
| **Resolve creative conflict** | Leadership Team → `creative-director` |
| **Make architecture decision** | Leadership Team → `technical-director` |

### **3. Use Engine-Specific Agents**

Choose the right engine specialists for your project:

#### **Unity Projects**
- `unity-specialist` -- Unity best practices and optimization
- `unity-dots-specialist` -- High-performance DOTS/ECS systems
- `unity-shader-specialist` -- Unity shaders and visual effects
- `unity-ui-specialist` -- Unity UI systems and implementation

#### **Godot Projects**
- `godot-specialist` -- Godot best practices and optimization
- `godot-gdscript-specialist` -- GDScript programming and patterns
- `godot-shader-specialist` -- Godot shaders and visual effects

#### **Unreal Projects**
- `unreal-specialist` -- Unreal best practices and optimization
- `ue-blueprint-specialist` -- Blueprint development and optimization
- `ue-gas-specialist` -- Gameplay Ability System implementation

#### **Cocos Creator Projects**
- `cocos-creator-specialist` -- Cocos Creator development and optimization

### **4. Start with the Right Workflow**

#### **New Projects**
```bash
/start                    # First-time onboarding and setup
/setup-engine            # Configure your chosen engine
/project-stage-detect     # Analyze current project state
```

#### **Development Work**
```bash
/design-review            # Review design documents
/code-review              # Review code changes
/prototype                # Create rapid prototypes
/sprint-plan              # Plan development work
```

#### **Quality Assurance**
```bash
/bug-report               # Create structured bug reports
/playtest-report          # Generate playtest reports
/gate-check              # Validate phase transitions
/quality-gates            # Run comprehensive quality checks
```

#### **Production Work**
```bash
/release-checklist        # Prepare for release
/changelog                # Generate changelog
/launch-checklist         # Validate launch readiness
/patch-notes              # Create player-facing patch notes
```

## 🔄 Common Workflows

### **New Feature Development**
1. `creative-director` -- Approve feature concept
2. `game-designer` -- Create design specification
3. `producer` -- Schedule and coordinate work
4. `lead-programmer` -- Design technical architecture
5. `[specialist-programmer]` -- Implement the feature
6. `qa-lead` -- Review and approve test coverage
7. `producer` -- Mark task complete

### **Bug Fix Process**
1. `qa-tester` -- File bug report with `/bug-report`
2. `qa-lead` -- Triage severity and priority
3. `producer` -- Assign to appropriate programmer
4. `[specialist-programmer]` -- Fix the bug
5. `lead-programmer` -- Code review
6. `qa-tester` -- Verify fix and regression test
7. `qa-lead` -- Close bug

### **Release Process**
1. `producer` -- Declare release candidate
2. `release-manager` -- Generate `/release-checklist`
3. `qa-lead` -- Run full regression testing
4. `devops-engineer` -- Build and deploy release
5. `release-manager` -- Generate `/changelog`
6. `technical-director` -- Final sign-off
7. `release-manager` -- Deploy and monitor

## 🎮 Engine Selection Guide

### **Choose Your Engine**
- **Unity**: Best for 2D/3D games, mobile games, cross-platform
- **Godot**: Best for 2D games, indie projects, open-source preference
- **Unreal**: Best for 3D AAA games, high-fidelity graphics
- **Cocos Creator**: Best for web games, mobile games, HTML5

### **Engine Setup**
```bash
/setup-engine unity        # Configure Unity project
/setup-engine godot        # Configure Godot project
/setup-engine unreal       # Configure Unreal project
/setup-engine cocos        # Configure Cocos Creator project
```

## 📊 Team Size Recommendations

### **Small Teams** (1-5 people)
- **Core agents**: `producer`, `game-designer`, `lead-programmer`, `art-director`, `qa-lead`
- **Engine specialist**: Choose one based on your engine
- **Focus**: Core development and essential quality assurance

### **Medium Teams** (6-15 people)
- **All team leads**: Add `audio-director`, `narrative-director`, `release-manager`
- **Specialists**: Add domain specialists based on project needs
- **Engine sub-specialists**: Add 2-3 engine sub-specialists
- **Focus**: Complete development pipeline with specialized expertise

### **Large Teams** (16+ people)
- **All agents**: Use the complete 79-agent architecture
- **Enhanced agents**: Use enhanced agents for complex requirements
- **Full engine support**: All engine specialists and sub-specialists
- **Focus**: Enterprise-scale development with full support

## 🎯 Best Practices

### **Start Small**
1. Begin with `/start` for onboarding
2. Use `/setup-engine` to configure your engine
3. Start with core team agents
4. Add specialists as needed

### **Follow the Hierarchy**
1. Always start with the appropriate team lead
2. Let team leads delegate to specialists
3. Use `producer` for cross-team coordination
4. Escalate to leadership team for major decisions

### **Use Skills Effectively**
1. Choose skills that match your team structure
2. Use team-specific skills for coordinated work
3. Use engine-specific skills for technical work
4. Use workflow skills for process management

### **Maintain Quality**
1. Always use `/gate-check` before phase transitions
2. Use `/quality-gates` for comprehensive validation
3. Follow the escalation paths for conflicts
4. Document decisions with `/architecture-decision`

## 🔧 Advanced Features

### **Team Collaboration Skills**
```bash
/team-combat              # Combat system development
/team-narrative           # Narrative content creation
/team-ui                  # UI/UX development
/team-release             # Release management
/team-polish              # Performance optimization
```

### **Design Framework Skills**
```bash
/competitive-analysis     # Market and competitive analysis
/aesthetic-direction      # Visual philosophy and direction
/core-loop-design         # Core gameplay loop design
/design-coherence         # Design system alignment
```

### **Quality Assurance Skills**
```bash
/playtest-report          # Structured playtest reporting
/bug-report               # Structured bug reporting
/perf-profile             # Performance profiling and optimization
/quality-gates            # Comprehensive quality validation
```

## 📚 Additional Resources

- **[Agent Roster](agent-roster.md)** - Complete list of all agents
- **[Agent Coordination Map](agent-coordination-map.md)** - Delegation rules and workflows
- **[Skills Reference](skills-reference.md)** - All available skills and commands
- **[Technical Preferences](technical-preferences.md)** - Development standards
- **[Directory Structure](directory-structure.md)** - Project organization

## 🎉 Getting Started Checklist

- [ ] Run `/start` for initial onboarding
- [ ] Use `/setup-engine` to configure your engine
- [ ] Identify your core team agents
- [ ] Set up your development workflow
- [ ] Configure quality gates and validation
- [ ] Establish communication protocols
- [ ] Start your first development cycle

---

*Quick Start Guide Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Organization: Team-Based Structure*
*Total Agents: 79*
*Total Teams: 8*
*Engines: Unity, Godot, Unreal, Cocos Creator*
| Manage a release | `release-manager` |
| Prepare strings for translation | `localization-lead` |
| Test a mechanic idea quickly | `prototyper` |
| Review code for security issues | `security-engineer` |
| Check accessibility compliance | `accessibility-specialist` |
| Get Unreal Engine advice | `unreal-specialist` |
| Get Unity advice | `unity-specialist` |
| Get Godot advice | `godot-specialist` |
| Design GAS abilities/effects | `ue-gas-specialist` |
| Define BP/C++ boundaries | `ue-blueprint-specialist` |
| Implement UE replication | `ue-replication-specialist` |
| Build UMG/CommonUI widgets | `ue-umg-specialist` |
| Design DOTS/ECS architecture | `unity-dots-specialist` |
| Write Unity shaders/VFX | `unity-shader-specialist` |
| Manage Addressable assets | `unity-addressables-specialist` |
| Build UI Toolkit/UGUI screens | `unity-ui-specialist` |
| Write idiomatic GDScript | `godot-gdscript-specialist` |
| Create Godot shaders | `godot-shader-specialist` |
| Build GDExtension modules | `godot-gdextension-specialist` |
| Plan live events and seasons | `live-ops-designer` |
| Write patch notes for players | `community-manager` |
| Brainstorm a new game idea | Use `/brainstorm` skill |

### 3. Use Slash Commands for Common Tasks

| Command | What it does |
|---------|-------------|
| `/start` | First-time onboarding — asks where you are, guides you to the right workflow |
| `/design-review` | Reviews a design document |
| `/code-review` | Reviews code for quality and architecture |
| `/playtest-report` | Creates or analyzes playtest feedback |
| `/balance-check` | Analyzes game balance data |
| `/sprint-plan` | Creates or updates sprint plans |
| `/architecture-decision` | Creates an ADR |
| `/asset-audit` | Audits assets for compliance |
| `/milestone-review` | Reviews milestone progress |
| `/onboard` | Generates onboarding docs for a role |
| `/prototype` | Scaffolds a throwaway prototype |
| `/release-checklist` | Validates pre-release checklist |
| `/changelog` | Generates changelog from git history |
| `/retrospective` | Runs sprint/milestone retrospective |
| `/estimate` | Produces structured effort estimates |
| `/hotfix` | Emergency fix with audit trail |
| `/tech-debt` | Scan, track, and prioritize tech debt |
| `/scope-check` | Detect scope creep against plan |
| `/localize` | Localization scan, extract, validate |
| `/perf-profile` | Performance profiling and bottleneck ID |
| `/gate-check` | Validate phase readiness (PASS/CONCERNS/FAIL) |
| `/project-stage-detect` | Analyze project state, detect stage, identify gaps |
| `/reverse-document` | Generate design/architecture docs from existing code |
| `/setup-engine` | Configure engine + version, populate reference docs |
| `/design-systems` | Decompose concept into systems, map dependencies, guide per-system GDDs |
| `/team-combat` | Orchestrate full combat team pipeline |
| `/team-narrative` | Orchestrate full narrative team pipeline |
| `/team-ui` | Orchestrate full UI team pipeline |
| `/team-release` | Orchestrate full release team pipeline |
| `/team-polish` | Orchestrate full polish team pipeline |
| `/team-audio` | Orchestrate full audio team pipeline |
| `/team-level` | Orchestrate full level creation pipeline |
| `/launch-checklist` | Complete launch readiness validation |
| `/patch-notes` | Generate player-facing patch notes |
| `/brainstorm` | Guided game concept ideation from scratch |

### 4. Use Templates for New Documents

Templates are in `.claude/docs/templates/`:

- `game-design-document.md` -- for new mechanics and systems
- `architecture-decision-record.md` -- for technical decisions
- `risk-register-entry.md` -- for new risks
- `narrative-character-sheet.md` -- for new characters
- `test-plan.md` -- for feature test plans
- `sprint-plan.md` -- for sprint planning
- `milestone-definition.md` -- for new milestones
- `level-design-document.md` -- for new levels
- `game-pillars.md` -- for core design pillars
- `art-bible.md` -- for visual style reference
- `technical-design-document.md` -- for per-system technical designs
- `post-mortem.md` -- for project/milestone retrospectives
- `sound-bible.md` -- for audio style reference
- `release-checklist-template.md` -- for platform release checklists
- `changelog-template.md` -- for player-facing patch notes
- `release-notes.md` -- for player-facing release notes
- `incident-response.md` -- for live incident response playbooks
- `game-concept.md` -- for initial game concepts (MDA, SDT, Flow, Bartle)
- `pitch-document.md` -- for pitching the game to stakeholders
- `economy-model.md` -- for virtual economy design (sink/faucet model)
- `faction-design.md` -- for faction identity, lore, and gameplay role

### 5. Follow the Coordination Rules

1. Work flows down the hierarchy: Directors -> Leads -> Specialists
2. Conflicts escalate up the hierarchy
3. Cross-department work is coordinated by the `producer`
4. Agents do not modify files outside their domain without delegation
5. All decisions are documented

## First Steps for a New Project

**Don't know where to begin?** Run `/start`. It asks where you are and routes
you to the right workflow. No assumptions about your game, engine, or experience level.

If you already know what you need, jump directly to the relevant path:

### Path A: "I have no idea what to build"

1. **Run `/start`** (or `/brainstorm open`) — guided creative exploration:
   what excites you, what you've played, your constraints
   - Generates 3 concepts, helps you pick one, defines core loop and pillars
   - Produces a game concept document and recommends an engine
2. **Set up the engine** — Run `/setup-engine` (uses the brainstorm recommendation)
   - Configures CLAUDE.md, detects knowledge gaps, populates reference docs
   - Creates `.claude/docs/technical-preferences.md` with naming conventions,
     performance budgets, and engine-specific defaults
   - If the engine version is newer than the LLM's training data, it fetches
     current docs from the web so agents suggest correct APIs
3. **Validate the concept** — Run `/design-review design/gdd/game-concept.md`
4. **Test the core loop** — Run `/prototype [core-mechanic]`
5. **Playtest it** — Run `/playtest-report` to validate the hypothesis
6. **Plan the first sprint** — Run `/sprint-plan new`
7. Start building

### Path B: "I know what I want to build"

If you already have a game concept and engine choice:

1. **Set up the engine** — Run `/setup-engine [engine] [version]`
   (e.g., `/setup-engine godot 4.6`) — also creates technical preferences
2. **Write the Game Pillars** — delegate to `creative-director`
3. **Create the initial ADR** — Run `/architecture-decision`
4. **Create the first milestone** in `production/milestones/`
5. **Plan the first sprint** — Run `/sprint-plan new`
6. Start building

### Path C: "I know the game but not the engine"

If you have a concept but don't know which engine fits:

1. **Run `/setup-engine`** with no arguments — it will ask about your game's
   needs (2D/3D, platforms, team size, language preferences) and recommend
   an engine based on your answers
2. Follow Path B from step 2 onward

### Path D: "I have an existing project"

If you have design docs, prototypes, or code already:

1. **Run `/start`** (or `/project-stage-detect`) — analyzes what exists,
   identifies gaps, and recommends next steps
2. **Configure engine if needed** — Run `/setup-engine` if not yet configured
3. **Validate phase readiness** — Run `/gate-check` to see where you stand
4. **Plan the next sprint** — Run `/sprint-plan new`

## File Structure Reference

```
CLAUDE.md                          -- Master config (read this first, ~60 lines)
.claude/
  settings.json                    -- Claude Code hooks and project settings
  agents/                          -- 48 agent definitions (YAML frontmatter)
  skills/                          -- 36 slash command definitions (YAML frontmatter)
  hooks/                           -- 8 hook scripts (.sh) wired by settings.json
  rules/                           -- 11 path-specific rule files
  docs/
    quick-start.md                 -- This file
    technical-preferences.md       -- Project-specific standards (populated by /setup-engine)
    coding-standards.md            -- Coding and design doc standards
    coordination-rules.md          -- Agent coordination rules
    context-management.md          -- Context budgets and compaction instructions
    review-workflow.md             -- Review and sign-off process
    directory-structure.md         -- Project directory layout
    agent-roster.md                -- Full agent list with tiers
    skills-reference.md            -- All slash commands
    rules-reference.md             -- Path-specific rules
    hooks-reference.md             -- Active hooks
    agent-coordination-map.md      -- Full delegation and workflow map
    setup-requirements.md          -- System prerequisites (Git Bash, jq, Python)
    settings-local-template.md     -- Personal settings.local.json guide
    hooks-reference/               -- Hook documentation and git hook examples
    templates/                     -- 28 document templates
```
