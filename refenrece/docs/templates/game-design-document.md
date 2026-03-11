# [Mechanic/System Name]

> **Status**: Draft | In Review | Approved | Implemented
> **Author**: [Agent or person]
> **Last Updated**: [Date]
> **Implements Pillar**: [Which game pillar this supports]
> **Team**: [Design Team | Programming Team | Cross-Team]
> **Lead Agent**: [Lead agent responsible]

## Overview

[One paragraph that explains this mechanic to someone who knows nothing about
the project. What is it, what does the player do, and why does it exist?]

## Player Fantasy

[What should the player FEEL when engaging with this mechanic? What is the
emotional or power fantasy being served? This section guides all detail
decisions below.]

## Team Responsibilities

### Design Team
- **Lead Agent**: `game-designer`
- **Contributors**: `systems-designer`, `level-designer`, `economy-designer`
- **Deliverables**: Design specification, balance formulas, user experience

### Programming Team
- **Lead Agent**: `lead-programmer`
- **Contributors**: `gameplay-programmer`, `ui-programmer`, engine specialists
- **Deliverables**: Implementation, performance optimization, bug fixes

### Art Team
- **Lead Agent**: `art-director`
- **Contributors**: `technical-artist`, `ux-designer`, `sound-designer`
- **Deliverables**: Visual assets, UI design, audio assets

### Quality Assurance Team
- **Lead Agent**: `qa-lead`
- **Contributors**: `qa-tester`, `performance-analyst`
- **Deliverables**: Test plan, bug reports, performance analysis

## Detailed Design

### Core Rules

[Precise, unambiguous rules. A programmer should be able to implement this
section without asking questions. Use numbered rules for sequential processes
and bullet points for properties.]

### States and Transitions

[If this system has states (e.g., weapon states, status effects, phases),
document every state and every valid transition between states.]

| State | Entry Condition | Exit Condition | Behavior |
|-------|----------------|----------------|----------|

### Interactions with Other Systems

[How does this system interact with combat? Inventory? Progression? UI?
For each interaction, specify the interface: what data flows in, what flows
out, and who is responsible for what.]

#### Team-Specific Interactions

**Programming Team Interactions:**
- Engine-specific implementations (Unity/Godot/Unreal/Cocos)
- Performance optimization requirements
- Network synchronization (if applicable)

**Art Team Interactions:**
- Visual effects and animations
- UI/UX design requirements
- Audio integration

**Quality Assurance Interactions:**
- Test scenarios and edge cases
- Performance benchmarks
- Accessibility requirements

## Formulas

[Every mathematical formula used by this system. For each formula:]

### [Formula Name]

```
result = base_value * (1 + modifier_sum) * scaling_factor
```

**Variables:**
- `base_value`: [description]
- `modifier_sum`: [description]
- `scaling_factor`: [description]

**Team Responsibility:**
- **Design**: Formula design and balance
- **Programming**: Implementation and optimization
- **QA**: Validation and testing

## Technical Requirements

### Performance Requirements

| Metric | Target | Team | Notes |
|--------|--------|------|-------|
| Frame Rate Impact | < 2ms per frame | Programming | Must be profiled |
| Memory Usage | < 10MB | Programming | Monitor leaks |
| Network Bandwidth | < 1KB/s | Programming | If multiplayer |

### Engine-Specific Requirements

#### Unity Implementation
- **Lead Agent**: `unity-specialist`
- **Components**: [List required Unity components]
- **Optimizations**: [Unity-specific optimizations]
- **Build Targets**: [Target platforms]

#### Godot Implementation
- **Lead Agent**: `godot-specialist`
- **Nodes**: [Required Godot node types]
- **Optimizations**: [Godot-specific optimizations]
- **Export Settings**: [Export configurations]

#### Unreal Implementation
- **Lead Agent**: `unreal-specialist`
- **Classes**: [Required Unreal classes]
- **Optimizations**: [Unreal-specific optimizations]
- **Build Targets**: [Target platforms]

#### Cocos Creator Implementation
- **Lead Agent**: `cocos-creator-specialist`
- **Components**: [Required Cocos components]
- **Optimizations**: [Cocos-specific optimizations]
- **Build Targets**: [Target platforms]

## Art Requirements

### Visual Design
- **Art Style**: [Reference to art bible]
- **Asset Requirements**: [List required assets]
- **Animation Requirements**: [Animation specifications]
- **UI Requirements**: [UI design specifications]

### Audio Requirements
- **Sound Effects**: [Required SFX]
- **Music**: [Music requirements]
- **Voice**: [Voice requirements if applicable]

## Testing Requirements

### Unit Tests
- **Programming Team**: Core logic tests
- **Design Team**: Formula validation tests
- **QA Team**: Edge case tests

### Integration Tests
- **Cross-Team**: System integration tests
- **Performance**: Performance tests
- **Accessibility**: Accessibility tests

### User Testing
- **Design Team**: Playability tests
- **QA Team**: Usability tests
- **Art Team**: Visual appeal tests

## Quality Gates

### Before Implementation
- [ ] Design is approved by `game-designer`
- [ ] Technical feasibility confirmed by `lead-programmer`
- [ ] Art requirements reviewed by `art-director`
- [ ] Test plan approved by `qa-lead`

### During Implementation
- [ ] Code reviews completed
- [ ] Art assets integrated
- [ ] Performance benchmarks met
- [ ] Test coverage achieved

### Before Release
- [ ] All acceptance criteria met
- [ ] Performance requirements met
- [ ] Accessibility requirements met
- [ ] Security requirements met (if applicable)

## Success Metrics

| Metric | Target | Team | Measurement Method |
|--------|--------|------|-------------------|
| Player Engagement | [Target] | Design | Analytics |
| Performance | [Target] | Programming | Profiling |
| Bug Count | < 5 | QA | Testing |
| User Satisfaction | [Target] | All | Feedback |

## Revision History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | [Date] | Initial version | [Author] |

---

*Updated for Team-Based Architecture*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: 8*
*Agents: 79*