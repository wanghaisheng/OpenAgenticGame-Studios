# Directory Structure - Team-Based Architecture

## 🏗️ Project Structure Overview

```text
Claude-Code-Game-Studios-main/
├── .claude/                           # Core configuration and agents
│   ├── agents/                        # Agent definitions (79 agents organized by team)
│   │   ├── leadership/                # Leadership team (7 agents)
│   │   ├── programming/               # Programming team (28 agents)
│   │   ├── design/                    # Design team (12 agents)
│   │   ├── art/                       # Art team (10 agents)
│   │   ├── qa/                        # Quality assurance team (6 agents)
│   │   ├── production/                # Production team (12 agents)
│   │   ├── support/                   # Support team (2 agents)
│   │   └── enhanced/                  # Enhanced team (4 agents)
│   ├── skills/                         # Skill files (72 skills)
│   │   ├── game-design/               # Game design skills (23 skills)
│   │   ├── unity/                     # Unity skills (7 skills)
│   │   ├── godot/                     # Godot skills (1 skill)
│   │   ├── cocos-creator/             # Cocos Creator skills (2 skills)
│   │   ├── quality-assurance/         # Quality assurance skills (1 skill)
│   │   ├── competitive-analysis/       # Competitive analysis skills (1 skill)
│   │   ├── development-tools/          # Development tool skills (1 skill)
│   │   └── team-collaboration/         # Team collaboration skills (37 skills)
│   ├── settings.json                   # Main configuration file
│   ├── hooks/                          # Automation hooks
│   └── docs/                           # Documentation
├── refenrece/                         # Centralized reference directory
│   ├── agents/                        # Agent definitions (same as .claude/agents/)
│   ├── skills/                        # Skill files (same as .claude/skills/)
│   ├── docs/                          # Reference documentation
│   └── README.md                      # Reference system overview
├── src/                              # Game source code
│   ├── Core/                          # Core game systems
│   ├── Gameplay/                       # Gameplay systems
│   ├── AI/                            # AI systems
│   ├── Networking/                     # Networking systems
│   ├── UI/                            # UI systems
│   └── Tools/                          # Development tools
├── assets/                           # Game assets
│   ├── Art/                           # Visual assets
│   ├── Audio/                         # Audio assets
│   ├── VFX/                           # Visual effects
│   ├── Shaders/                       # Shader files
│   └── Data/                          # Game data
├── design/                           # Game design documents
│   ├── GDD/                           # Game design documents
│   ├── Narrative/                      # Narrative documents
│   ├── Levels/                         # Level designs
│   └── Balance/                        # Balance sheets
├── docs/                             # Technical documentation
│   ├── Architecture/                   # Architecture documentation
│   ├── API/                           # API documentation
│   ├── engine-reference/               # Engine API references
│   │   ├── unity/                     # Unity API reference
│   │   ├── godot/                     # Godot API reference
│   │   ├── unreal/                    # Unreal API reference
│   │   └── cocos-creator/             # Cocos Creator API reference
│   └── Postmortems/                    # Postmortem analysis
├── tests/                            # Test suites
│   ├── Unit/                          # Unit tests
│   ├── Integration/                   # Integration tests
│   ├── Performance/                   # Performance tests
│   └── Playtest/                      # Playtest reports
├── tools/                            # Build and pipeline tools
│   ├── CI/                            # Continuous integration
│   ├── Build/                         # Build scripts
│   └── Asset-pipeline/                 # Asset pipeline tools
├── prototypes/                        # Throwaway prototypes
└── production/                        # Production management
    ├── Sprints/                       # Sprint documentation
    ├── Milestones/                    # Milestone tracking
    └── Releases/                      # Release documentation
```

## 🎯 Team Structure Details

### **Leadership Team** (.claude/agents/leadership/)
- `creative-director.md` - Creative vision and artistic direction
- `technical-director.md` - Technical strategy and architecture
- `producer.md` - Project management and delivery
- `art-director.md` - Visual direction and art standards
- `audio-director.md` - Audio direction and sound design
- `narrative-director.md` - Story and narrative vision
- `game-vision-architect.md` - Long-term vision and strategy

### **Programming Team** (.claude/agents/programming/)
#### **Core Programming**
- `lead-programmer.md` - Technical leadership and code standards
- `gameplay-programmer.md` - Gameplay systems implementation
- `engine-programmer.md` - Engine-level programming
- `ai-programmer.md` - AI systems implementation
- `network-programmer.md` - Multiplayer systems
- `ui-programmer.md` - UI implementation
- `tools-programmer.md` - Development tools

#### **Unity Specialists**
- `unity-specialist.md` - Unity best practices
- `unity-dots-specialist.md` - Unity DOTS/ECS
- `unity-addressables-specialist.md` - Unity asset management
- `unity-shader-specialist.md` - Unity shaders
- `unity-ui-specialist.md` - Unity UI systems
- `unity-development-specialist.md` - Unity development
- `unity-skills-automation.md` - Unity automation
- `unity-asset-guidelines-specialist.md` - Unity assets

#### **Godot Specialists**
- `godot-specialist.md` - Godot best practices
- `godot-gdscript-specialist.md` - GDScript programming
- `godot-gdextension-specialist.md` - Native extensions
- `godot-shader-specialist.md` - Godot shaders
- `godot-full-stack-specialist.md` - Complete Godot development

#### **Unreal Specialists**
- `unreal-specialist.md` - Unreal best practices
- `ue-blueprint-specialist.md` - Blueprint development
- `ue-gas-specialist.md` - Gameplay Ability System
- `ue-replication-specialist.md` - Network replication
- `ue-umg-specialist.md` - Unreal UI systems

#### **Cocos Specialists**
- `cocos-creator-specialist.md` - Cocos Creator development
- `cocos-skills-automation.md` - Cocos automation

#### **Skill Specialists**
- `skill-creation-specialist.md` - Skill development

### **Design Team** (.claude/agents/design/)
#### **Core Design**
- `game-designer.md` - Game design and mechanics
- `systems-designer.md` - Game systems design
- `level-designer.md` - Level design and layout
- `economy-designer.md` - Economy systems and balance
- `world-builder.md` - World building and lore
- `writer.md` - Narrative content and dialogue
- `live-ops-designer.md` - Live events and retention

#### **Design Framework**
- `narrative-game-generator.md` - Interactive narrative generation
- `aesthetic-direction-framework.md` - Visual philosophy
- `core-loop-designer.md` - Core gameplay loops
- `design-coherence-engine.md` - Design system alignment
- `competitive-analysis-specialist.md` - Market analysis

### **Art Team** (.claude/agents/art/)
#### **Core Art**
- `technical-artist.md` - Technical art and shaders
- `ux-designer.md` - User experience design
- `accessibility-specialist.md` - Accessibility features
- `sound-designer.md` - Audio effects and music

#### **Enhanced Art**
- `enhanced-technical-artist.md` - Advanced technical art
- `enhanced-sound-designer.md` - Advanced audio
- `enhanced-ui-specialist.md` - Advanced UI
- `enhanced-ux-designer.md` - Advanced UX
- `enhanced-art-director.md` - Advanced art direction
- `enhanced-composer.md` - Advanced music

### **Quality Assurance Team** (.claude/agents/qa/)
- `qa-lead.md` - QA coordination and strategy
- `qa-tester.md` - Testing execution and reporting
- `performance-analyst.md` - Performance monitoring
- `game-quality-gates-specialist.md` - Quality standards
- `enhanced-qa-tester.md` - Advanced testing
- `enhanced-performance-analyst.md` - Advanced performance

### **Production Team** (.claude/agents/production/)
#### **Core Production**
- `release-manager.md` - Release pipeline management
- `localization-lead.md` - Internationalization
- `community-manager.md` - Community engagement
- `analytics-engineer.md` - Player analytics
- `devops-engineer.md` - CI/CD and infrastructure
- `security-engineer.md` - Security and anti-cheat
- `prototyper.md` - Rapid prototyping

#### **Enhanced Production**
- `enhanced-release-manager.md` - Advanced release management
- `enhanced-community-manager.md` - Advanced community
- `enhanced-devops-engineer.md` - Advanced DevOps
- `enhanced-security-engineer.md` - Advanced security
- `enhanced-prototyper.md` - Advanced prototyping

### **Support Team** (.claude/agents/support/)
- `enhanced-analytics-engineer.md` - Advanced analytics
- `enhanced-network-engineer.md` - Advanced networking

### **Enhanced Team** (.claude/agents/enhanced/)
- `enhanced-game-designer.md` - Advanced game design
- `enhanced-tool-developer.md` - Advanced tool development
- `enhanced-art-director.md` - Advanced art direction
- `enhanced-network-engineer.md` - Advanced networking

## 🎮 Skills Structure Details

### **Game Design Skills** (refenrece/skills/game-design/)
- Core gameplay mechanics and systems design
- Game balance and economy systems
- Level design and world building
- Narrative design and storytelling
- Player experience and engagement

### **Unity Skills** (refenrece/skills/unity/)
- Unity development best practices
- Unity DOTS/ECS performance optimization
- Unity asset management and optimization
- Unity UI systems and implementation
- Unity shaders and visual effects
- Unity automation and tool development

### **Godot Skills** (refenrece/skills/godot/)
- Godot development best practices
- GDScript programming and optimization
- Godot shader development
- Godot performance optimization

### **Cocos Creator Skills** (refenrece/skills/cocos-creator/)
- Cocos Creator development best practices
- Cocos Creator performance optimization
- Cocos Creator automation

### **Quality Assurance Skills** (refenrece/skills/quality-assurance/)
- Quality standards and requirements
- Testing methodologies and best practices
- Performance monitoring and optimization
- Bug tracking and resolution

### **Competitive Analysis Skills** (refenrece/skills/competitive-analysis/)
- Market analysis and research
- Competitive landscape analysis
- Feature comparison and positioning

### **Development Tools Skills** (refenrece/skills/development-tools/)
- Development tool creation and optimization
- Automation and workflow improvement
- Build system optimization

### **Team Collaboration Skills** (refenrece/skills/team-collaboration/)
- Cross-team coordination and communication
- Project management and planning
- Quality assurance and testing
- Release management and deployment

## 📚 Documentation Structure

### **Reference Documentation** (refenrece/docs/)
- `agent-roster.md` - Complete agent listing
- `agent-coordination-map.md` - Delegation rules and workflows
- `skills-reference.md` - Available skills and commands
- `quick-start.md` - Getting started guide
- `coding-standards.md` - Development standards
- `context-management.md` - Context management
- `coordination-rules.md` - Coordination rules
- `directory-structure.md` - Project structure
- `technical-preferences.md` - Technical preferences

### **Engine Reference Documentation** (docs/engine-reference/)
- `unity/` - Unity API reference and best practices
- `godot/` - Godot API reference and best practices
- `unreal/` - Unreal API reference and best practices
- `cocos-creator/` - Cocos Creator API reference and best practices

## 🔧 Configuration Files

### **Main Configuration** (.claude/settings.json)
- Agent and skill file references
- Team-based organization settings
- Quality gate configurations
- Hook and automation settings

### **Reference Configuration** (refenrece/settings.json)
- Centralized reference system settings
- Cross-agent configuration templates
- Quality standards and requirements

## 📊 Statistics

### **Agent Statistics**
- **Total Agents**: 79 agents
- **Leadership Team**: 7 agents
- **Programming Team**: 28 agents
- **Design Team**: 12 agents
- **Art Team**: 10 agents
- **Quality Assurance Team**: 6 agents
- **Production Team**: 12 agents
- **Support Team**: 2 agents
- **Enhanced Team**: 4 agents

### **Skill Statistics**
- **Total Skills**: 72 skills
- **Game Design**: 23 skills
- **Unity**: 7 skills
- **Godot**: 1 skill
- **Cocos Creator**: 2 skills
- **Quality Assurance**: 1 skill
- **Competitive Analysis**: 1 skill
- **Development Tools**: 1 skill
- **Team Collaboration**: 37 skills

---

*Directory Structure Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Organization: Team-Based Structure*
*Total Agents: 79*
*Total Skills: 72*
*Total Teams: 8*
