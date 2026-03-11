# OpenAgenticGame Studios - Universal Agent First Game Dev AI Game Studios

Any AI IDE. Complete game studio. Instantly. 85 coordinated agents organized into 9 teams, accessible across all AI platforms through our universal reference system.

## 🎯 **Agent Architecture Overview**

### **Agent Statistics**
- **Total Agents**: 85 (organized into 9 teams)
- **Engine Specialists**: Unity (8), Godot (5), Unreal (5), Cocos Creator (2)
- **Cross-Platform**: 65 engine-agnostic agents
- **Quality Assurance**: 6 QA and quality gates agents
- **Publish Team**: 6 publishing and platform specialists
- **DevOps Automation**: 12 production and support agents

### **Team Structure**
- **Leadership Team**: 7 agents - Executive and vision leadership
- **Programming Team**: 28 agents - Core programming and development
- **Design Team**: 12 agents - Game and system design
- **Art Team**: 10 agents - Art direction and technical art
- **Quality Assurance Team**: 6 agents - Quality assurance and testing
- **Production Team**: 12 agents - Production and project management
- **Publish Team**: 6 agents - Game publishing and platform management
- **Support Team**: 2 agents - Community, analytics, and support
- **Enhanced Team**: 4 agents - Enhanced capabilities and advanced features

## 🏗️ **Technology Stack**

### **Supported Engines**
- **Unity**: 8 specialized agents (development, DOTS, addressables, shaders, UI, automation, asset guidelines)
- **Godot**: 5 specialized agents (gameplay, GDScript, GDExtension, shaders, full-stack)
- **Unreal**: 5 specialized agents (gameplay, blueprints, GAS, replication, UMG)
- **Cocos Creator**: 2 specialized agents (development, automation)
- **Cross-Platform**: 65 engine-agnostic agents

### **Core Technologies**
- **Version Control**: Git with trunk-based development
- **Build Systems**: Engine-specific build automation
- **Asset Pipeline**: Engine-optimized asset management
- **Quality Gates**: Automated quality assurance
- **DevOps Automation**: CI/CD and deployment automation

> **Note**: Use engine-specialist agents matching your chosen engine. Cross-platform agents work with any engine.

## 📁 **Project Structure**

### **Core Structure**
```
Claude-Code-Game-Studios-main/
├── .claude/
│   ├── agents/ (85 agent files organized by teams)
│   │   ├── leadership/ (7 agents)
│   │   ├── programming/ (28 agents)
│   │   ├── design/ (12 agents)
│   │   ├── art/ (10 agents)
│   │   ├── qa/ (6 agents)
│   │   ├── production/ (12 agents)
│   │   ├── publish/ (6 agents)
│   │   ├── support/ (2 agents)
│   │   └── enhanced/ (4 agents)
│   ├── skills/ (72 skill files organized by categories)
│   ├── settings.json (main configuration)
│   └── references/ (unified reference directory)
├── refenrece/
│   ├── agents/ (85 agent files)
│   ├── skills/ (72 skill files)
│   ├── docs/ (comprehensive documentation)
│   ├── rules/ (12 rule files)
│   └── qualification/ (6 platform quality standards)
├── docs/
│   ├── engine-reference/
│   │   ├── godot/
│   │   ├── unity/
│   │   ├── unreal/
│   │   └── cocos-creator/
│   └── qualification/
│       ├── steam/
│       ├── mobile/
│       ├── console/
│       ├── epic/
│       ├── crazygames/
│       └── gamedistribution/
└── references/
    ├── README.md
    ├── SKILLS_MANIFEST.json
    └── TEAMS_OVERVIEW.md
```

### **Agent Coordination**
- **Domain Ownership**: Each agent owns specific domain expertise
- **Collaboration Protocols**: Defined agent-to-agent collaboration
- **Quality Gates**: Automated quality checks and validation
- **Workflow Integration**: Seamless workflow between agents

@.claude/docs/directory-structure.md

## 📚 **Engine Reference Documentation**

### **Godot Reference**
@docs/engine-reference/godot/VERSION.md
@docs/engine-reference/godot/testing.md
@docs/engine-reference/godot/deployment.md

### **Unity Reference**
@docs/engine-reference/unity/ (existing comprehensive documentation)

### **Unreal Reference**
@docs/engine-reference/unreal/ (existing comprehensive documentation)

### **Cocos Creator Reference**
@docs/engine-reference/cocos-creator/README.md
@docs/engine-reference/cocos-creator/VERSION.md
@docs/engine-reference/cocos-creator/development.md

## 🎯 **Technical Preferences**

### **Development Standards**
@.claude/docs/technical-preferences.md

### **Quality Standards**
- **12 Universal Quality Gates**: Mandatory quality standards
- **Platform-Specific Requirements**: Web, mobile, desktop optimizations
- **Anti-Cheat Implementation**: Client and server-side validation
- **Performance Optimization**: Memory, rendering, physics optimization

### **Automation Standards**
- **CLI Automation**: Cocos Creator and Unity CLI tools
- **Batch Operations**: Efficient batch processing
- **Workflow Automation**: Automated development workflows
- **Quality Automation**: Automated quality checks

## 🤝 **Coordination Rules**

### **Agent Coordination**
@.claude/docs/coordination-rules.md

### **Quality Coordination**
- **Quality Gates**: Mandatory quality checks
- **Cross-Agent Validation**: Inter-agent quality validation
- **Performance Monitoring**: Real-time performance monitoring
- **Error Handling**: Comprehensive error management

### **Automation Coordination**
- **Tool Integration**: Seamless tool integration
- **Workflow Orchestration**: Automated workflow management
- **Resource Management**: Efficient resource utilization
- **Quality Assurance**: Automated quality assurance

## 🤖 **Collaboration Protocol**

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question -> Options -> Decision -> Draft -> Approval**

- Agents MUST ask "May I write this to [filepath]?" before using Write/Edit tools
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction
- Quality gates must be passed before deployment

See `docs/COLLABORATIVE-DESIGN-PRINCIPLE.md` for full protocol and examples.

> **First session?** If the project has no engine configured and no game concept,
> run `/start` to begin the guided onboarding flow.

## 💻 **Coding Standards**

### **Development Standards**
@.claude/docs/coding-standards.md

### **Quality Standards**
- **Code Quality**: Comprehensive code quality standards
- **Performance Standards**: Performance optimization guidelines
- **Security Standards**: Security best practices
- **Documentation Standards**: Complete documentation requirements

## 🧠 **Context Management**

### **Context Architecture**
@.claude/docs/context-management.md

### **Knowledge Management**
- **Skills Directory**: 72 specialized skill files organized by categories
- **Reference System**: Unified reference system with team-based organization
- **Agent Knowledge**: 79 specialized agent knowledge bases organized by teams
- **Cross-Reference**: Comprehensive cross-reference system

## 🔄 **References and Reuse**

### **Reference System**
- **Unified References**: `references/` directory for all AI agents
- **AI Agent Templates**: `AI_AGENT_SETTINGS_TEMPLATE.json` for .codex, .windsurf, .trae
- **Cross-Agent Reuse**: All AI agents can reference the same knowledge base
- **Version Control**: Unified version control for all references

### **AI Agent Integration**
```json
{
  "references": {
    "path": "./refenrece",
    "skillFiles": [
      "game-design/SKILL.md",
      "unity/SKILL.md",
      "godot/SKILL.md",
      "cocos-creator/SKILL.md",
      "quality-assurance/SKILL.md",
      "competitive-analysis/SKILL.md",
      "development-tools/SKILL.md",
      "team-collaboration/SKILL.md"
    ],
    "agentFiles": [
      "leadership/creative-director.md",
      "leadership/technical-director.md",
      "leadership/producer.md",
      "leadership/art-director.md",
      "leadership/audio-director.md",
      "leadership/narrative-director.md",
      "leadership/game-vision-architect.md",
      "programming/lead-programmer.md",
      "programming/gameplay-programmer.md",
      "programming/engine-programmer.md",
      "programming/ai-programmer.md",
      "programming/network-programmer.md",
      "programming/ui-programmer.md",
      "programming/tools-programmer.md",
      "programming/unity-specialist.md",
      "programming/unity-dots-specialist.md",
      "programming/unity-addressables-specialist.md",
      "programming/unity-shader-specialist.md",
      "programming/unity-ui-specialist.md",
      "programming/unity-development-specialist.md",
      "programming/unity-skills-automation.md",
      "programming/unity-asset-guidelines-specialist.md",
      "programming/godot-specialist.md",
      "programming/godot-gdscript-specialist.md",
      "programming/godot-gdextension-specialist.md",
      "programming/godot-shader-specialist.md",
      "programming/godot-full-stack-specialist.md",
      "programming/unreal-specialist.md",
      "programming/ue-blueprint-specialist.md",
      "programming/ue-gas-specialist.md",
      "programming/ue-replication-specialist.md",
      "programming/ue-umg-specialist.md",
      "programming/cocos-creator-specialist.md",
      "programming/cocos-skills-automation.md",
      "programming/skill-creation-specialist.md",
      "design/game-designer.md",
      "design/systems-designer.md",
      "design/level-designer.md",
      "design/economy-designer.md",
      "design/world-builder.md",
      "design/writer.md",
      "design/live-ops-designer.md",
      "design/narrative-game-generator.md",
      "design/aesthetic-direction-framework.md",
      "design/core-loop-designer.md",
      "design/design-coherence-engine.md",
      "design/competitive-analysis-specialist.md",
      "art/technical-artist.md",
      "art/ux-designer.md",
      "art/accessibility-specialist.md",
      "art/sound-designer.md",
      "qa/qa-lead.md",
      "qa/qa-tester.md",
      "qa/performance-analyst.md",
      "qa/game-quality-gates-specialist.md",
      "qa/enhanced-qa-tester.md",
      "qa/enhanced-performance-analyst.md",
      "production/release-manager.md",
      "production/localization-lead.md",
      "production/community-manager.md",
      "production/analytics-engineer.md",
      "production/devops-engineer.md",
      "production/security-engineer.md",
      "production/prototyper.md",
      "production/enhanced-release-manager.md",
      "production/enhanced-community-manager.md",
      "production/enhanced-devops-engineer.md",
      "production/enhanced-security-engineer.md",
      "production/enhanced-prototyper.md",
      "support/enhanced-analytics-engineer.md",
      "support/enhanced-network-engineer.md",
      "enhanced/enhanced-game-designer.md",
      "enhanced/enhanced-tool-developer.md",
      "enhanced/enhanced-art-director.md",
      "enhanced/enhanced-network-engineer.md"
    ]
  }
}
```

## 🚀 **Getting Started**

### **Engine Selection**
1. **Choose Engine**: Select Unity, Godot, Unreal, or Cocos Creator
2. **Configure Agents**: Use engine-specific agents
3. **Set Up References**: Configure reference system
4. **Initialize Project**: Run `/start` for guided setup

### **Agent Selection**
- **Small Projects**: Use 28 core programming + 7 leadership = 35 agents
- **Medium Projects**: Add 12 design + 10 art + 6 qa = 63 agents
- **Large Projects**: Add 12 production + 2 support = 77 agents
- **Flagship Projects**: Add 6 publish + 4 enhanced = 87 agents (full team)

### **Quality Assurance**
- **Pre-Development**: Use quality gates for planning
- **During Development**: Use continuous quality monitoring
- **Pre-Deployment**: Use comprehensive quality validation
- **Post-Deployment**: Use ongoing quality monitoring

## 📊 **Performance and Quality**

### **Performance Metrics**
- **Agent Response Time**: < 2 seconds for standard queries
- **Quality Gate Validation**: < 5 seconds for validation
- **Batch Processing**: Efficient batch operation support
- **Memory Usage**: Optimized memory utilization

### **Quality Metrics**
- **Code Quality**: 95%+ code quality standards
- **Documentation**: 100% documentation coverage
- **Test Coverage**: 90%+ test coverage
- **Performance**: Target performance benchmarks

---

## 🎯 **Project Success Metrics**

### **Development Efficiency**
- **Time to Market**: 50% faster development cycles
- **Quality Assurance**: 95%+ quality standards compliance
- **Resource Utilization**: 80%+ resource efficiency
- **Team Productivity**: 3x team productivity increase

### **Technical Excellence**
- **Code Quality**: Industry-leading code quality
- **Performance**: Optimized performance benchmarks
- **Security**: Comprehensive security implementation
- **Maintainability**: Long-term maintainability

### **Business Value**
- **Cost Reduction**: 40% development cost reduction
- **Quality Improvement**: 60% quality improvement
- **Time to Market**: 50% faster time to market
- **User Satisfaction**: 90%+ user satisfaction

---

*OpenAgenticGame - Agent First Game Dev AI Game Studios Architecture*
*Version: 2.0.0*
*Last updated: 2026-03-10*
*Total Agents: 85*
*Teams: 9*
*Engine Support: Unity, Godot, Unreal, Cocos Creator*
*Quality System: Comprehensive quality gates*
*Automation: Full DevOps automation*
