---
paths:
  - "src/ai/**"
  - "src/artificial-intelligence/**"
---

# AI Code Rules - Team-Based Architecture

## 🏗️ Team Responsibilities

### **Primary Team**: Programming Team
- **Lead Agent**: `ai-programmer`
- **Contributors**: `lead-programmer`, engine specialists
- **Design Team**: `game-designer` (AI behavior design)
- **QA Team**: `qa-lead`, `performance-analyst`

### **Cross-Team Integration**
- **Art Team**: `technical-artist` (AI visualization)
- **Audio Team**: `audio-director` (AI audio feedback)
- **Production Team**: `producer` (AI milestone coordination)

## 🤖 Core AI Rules

### **Performance Rules**
- AI update budget: 2ms per frame maximum — profile to verify
- All AI parameters must be tunable from data files (behavior tree weights, perception ranges, timers)
- AI must be debuggable: implement visualization hooks for all AI state (paths, perception cones, decision trees)
- AI should telegraph intentions — players need time to read and react
- Prefer utility-based or behavior tree approaches over hard-coded if/else chains
- Group AI must support formation, flanking, and role assignment from data
- All AI state machines must log transitions for debugging
- Never trust AI input from the network without validation

### **Team Coordination**
- AI behaviors must be coordinated with Design Team
- AI performance must be coordinated with Performance Analyst
- AI visualization must be coordinated with Technical Artist
- AI audio must be coordinated with Audio Director
- AI testing must be coordinated with QA Team

## 🔧 Technical Rules

### **Code Organization**
- Use clear separation of concerns between AI systems
- Implement proper AI architecture patterns
- Use consistent naming conventions for AI components
- Implement proper error handling and logging
- Use object pooling for AI entities when appropriate

### **Performance Rules**
- Profile all AI systems for performance
- Optimize critical AI update paths
- Use efficient AI algorithms and data structures
- Implement proper memory management for AI systems
- Monitor AI system performance in real-time

### **Testing Rules**
- Write unit tests for all AI logic
- Write integration tests for AI systems
- Test AI systems with different configurations
- Test AI systems under load
- Test edge cases and error conditions

## 🧠 AI Architecture

### **Behavior Trees**
- Use behavior trees for complex AI decision making
- Implement proper behavior tree node types
- Use behavior tree debugging and visualization
- Test behavior trees with different configurations
- Document behavior tree design and limitations

### **State Machines**
- Use state machines for simple AI behaviors
- Implement proper state machine transition tables
- Use state machine debugging and visualization
- Test state machines with different configurations
- Document state machine design and limitations

### **Utility AI**
- Use utility-based AI for decision making
- Implement proper utility calculation systems
- Use utility AI debugging and visualization
- Test utility systems with different configurations
- Document utility AI design and limitations

## 🎮 Design Integration

### **Design Document Integration**
- Every AI behavior must reference the corresponding design document
- Implement AI behaviors exactly as specified in design documents
- Document any deviations from design documents with justification
- Coordinate design changes with Design Team
- Update design documents when AI implementation reveals issues

### **Design Validation**
- Validate AI behaviors with Design Team
- Test AI balance with Design Team
- Validate AI systems with Design Team
- Get approval for AI changes from Design Team
- Document AI design decisions

## 🎨 Art Integration

### **Visualization Requirements**
- Coordinate AI visualization requirements with Technical Artist
- Implement AI debugging visualization as specified by Technical Artist
- Use visualization assets according to Art Team specifications
- Implement AI visual effects according to Art Team guidelines
- Test AI visualization with Technical Artist

### **Debug Visualization**
- Implement AI state visualization for debugging
- Use color-coded visualization for AI states
- Implement AI path visualization for debugging
- Use visualization tools for AI decision making
- Test AI visualization with Technical Artist

## 🔊 Audio Integration

### **Audio Requirements**
- Coordinate AI audio requirements with Audio Director
- Implement AI audio feedback systems as specified by Audio Director
- Use audio assets according to Audio Team specifications
- Implement AI audio effects according to Audio Team guidelines
- Test AI audio integration with Audio Director

### **Sound Integration**
- Use sound assets according to Audio Team pipeline
- Implement proper sound loading and management
- Coordinate sound requirements with Audio Team
- Test sound integration with Audio Team
- Document sound integration issues

## 🧪 Testing Requirements

### **Unit Testing**
- Write unit tests for all AI logic
- Test AI systems with mock data
- Test AI systems with different configurations
- Test edge cases and error conditions
- Test AI systems in isolation

### **Integration Testing**
- Test AI systems integration with other systems
- Test AI systems with real data
- Test AI systems under load
- Test AI systems with different configurations
- Test AI systems with different platforms

### **Performance Testing**
- Test AI systems performance under load
- Test AI systems with different AI counts
- Test AI systems with different AI complexities
- Test AI systems with different environments
- Test AI systems with different platforms

## 📊 Performance Requirements

### **Performance Budgets**
- **AI Update Time**: < 2ms per frame
- **AI Memory Usage**: < 100MB for AI systems
- **AI CPU Usage**: < 50% of available CPU
- **AI Network Usage**: < 5KB/s for AI data

### **Performance Monitoring**
- Monitor AI system performance in real-time
- Profile AI systems regularly
- Log performance violations and issues
- Alert on performance budget violations
- Generate performance reports

## 🔒 Security Rules

### **AI Security**
- Validate all AI inputs and data
- Implement proper error handling and logging
- Use secure coding practices for AI code
- Implement proper memory management
- Validate all AI state changes

### **Network Security**
- Validate all network AI data
- Implement proper network security for multiplayer AI
- Use secure communication protocols
- Validate all network AI state
- Implement proper anti-cheat measures for AI

## 📝 Documentation Requirements

### **Code Documentation**
- Document all AI systems with examples
- Document AI system interfaces
- Document AI system dependencies
- Document AI system limitations
- Document troubleshooting guides

### **Design Documentation**
- Document AI design decisions
- Document AI behavior implementation
- Document AI balance calculations
- Document AI system interactions
- Document AI system limitations

## 🔄 Quality Gates

### **Pre-Implementation Gates**
- [ ] Design is reviewed and approved by `game-designer`
- [ ] Performance requirements are defined
- [ ] Testing requirements are defined
- [ ] Visualization requirements are defined
- [ ] Audio requirements are defined

### **Implementation Gates**
- [ ] Code follows AI coding standards
- [ ] Performance requirements are met
- [ ] Visualization requirements are met
- [ ] Audio requirements are met
- [ ] Tests are written and passing

### **Pre-Release Gates**
- [ ] All AI behaviors are implemented as specified
- [ ] All AI systems are balanced and tested
- [ ] All AI systems are performant
- [ ] All AI systems are secure
- [ ] All AI systems are documented

## 🚀 Examples

### **Correct** (data-driven AI):

#### Configuration Example
```gdscript
# AI configuration from data files
var ai_config: Dictionary = load_ai_config("enemy_ai.json")
var perception_range: float = ai_config.get("perception_range", 10.0)
var attack_damage: float = ai_config.get("attack_damage", 25.0)
```

#### Behavior Tree Example
```gdscript
# Behavior tree implementation
class BehaviorTree:
    var root: BehaviorNode
    
    func _init():
        root = SelectorNode.new()
        root.add_child(SequenceNode.new([
            CheckEnemyInRange.new(),
            AttackEnemy.new(),
            PatrolBehavior.new()
        ]))
```

### **Incorrect** (hardcoded AI):

#### Hardcoded Values Example
```gdscript
# VIOLATION: Hardcoded AI parameters
var perception_range: float = 15.0
var attack_damage: float = 30.0
var attack_cooldown: float = 2.0
```

#### Hardcoded Logic Example
```gdscript
# VIOLATION: Hardcoded AI logic
func _process(delta: float) -> void:
    if enemy_in_range:
        attack_enemy()
    else:
        patrol()
```

## 📋 Checklist

### **Development Checklist**
- [ ] AI parameters are data-driven
- [ ] AI update budget is met
- [ ] AI is debuggable with visualization
- [ ] AI telegraphs intentions
- [ ] AI uses appropriate AI architecture

### **Review Checklist**
- [ ] Code reviewed by `ai-programmer`
- [ ] Design reviewed by `game-designer`
- [ ] Performance reviewed by `performance-analyst`
- [ ] Visualization reviewed by `technical-artist`
- [ ] QA reviewed by `qa-lead`

---

*AI Code Rules Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: Programming Team, Design Team*
*Integration: Art Team, Audio Team, QA Team*