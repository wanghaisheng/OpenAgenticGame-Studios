---
paths:
  - "src/gameplay/**"
  - "src/systems/**"
---

# Gameplay Code Rules - Team-Based Architecture

## 🏗️ Team Responsibilities

### **Primary Team**: Design Team
- **Lead Agent**: `game-designer`
- **Contributors**: `systems-designer`, `level-designer`, `economy-designer`
- **Programming Team**: `gameplay-programmer`, `lead-programmer`
- **QA Team**: `qa-lead`, `qa-tester`

### **Cross-Team Integration**
- **Art Team**: `art-director` (visual feedback)
- **Audio Team**: `audio-director` (audio feedback)
- **Production Team**: `producer` (milestone coordination)

## 🎮 Core Gameplay Rules

### **Data-Driven Design**
- ALL gameplay values MUST come from external config/data files, NEVER hardcoded
- Use delta time for ALL time-dependent calculations (frame-rate independence)
- NO direct references to UI code — use events/signals for cross-system communication
- Every gameplay system must implement a clear interface
- State machines must have explicit transition tables with documented states
- Write unit tests for all gameplay logic — separate logic from presentation
- Document which design doc each feature implements in code comments
- No static singletons for game state — use dependency injection

### **Team Coordination**
- Gameplay features must be coordinated with Design Team
- Art requirements must be coordinated with Art Team
- Audio requirements must be coordinated with Audio Team
- Testing requirements must be coordinated with QA Team
- Production requirements must be coordinated with Production Team

## 🔧 Technical Rules

### **Code Organization**
- Use clear separation of concerns between gameplay systems
- Implement proper dependency injection for game state
- Use event-driven architecture for cross-system communication
- Implement proper error handling and logging
- Use consistent naming conventions for gameplay systems

### **Performance Rules**
- Profile all gameplay systems for performance
- Optimize critical gameplay paths
- Use object pooling for frequently created/destroyed objects
- Implement proper memory management for gameplay systems
- Monitor gameplay system performance in real-time

### **Testing Rules**
- Write unit tests for all gameplay logic
- Write integration tests for gameplay systems
- Test gameplay systems with different configurations
- Test gameplay systems under load
- Test edge cases and error conditions

## 🎯 Design Integration

### **Design Document Integration**
- Every gameplay feature must reference the corresponding design document
- Implement gameplay mechanics exactly as specified in design documents
- Document any deviations from design documents with justification
- Coordinate design changes with Design Team
- Update design documents when gameplay implementation reveals issues

### **Design Validation**
- Validate gameplay mechanics with Design Team
- Test gameplay balance with Design Team
- Validate gameplay systems with Design Team
- Get approval for gameplay changes from Design Team
- Document gameplay design decisions

## 🎨 Art Integration

### **Visual Requirements**
- Coordinate visual requirements with Art Team
- Implement visual feedback systems as specified by Art Team
- Use art assets according to Art Team specifications
- Implement visual effects according to Art Team guidelines
- Test visual integration with Art Team

### **Asset Integration**
- Use art assets according to Art Team pipeline
- Implement proper asset loading and management
- Coordinate asset requirements with Art Team
- Test asset integration with Art Team
- Document asset integration issues

## 🔊 Audio Integration

### **Audio Requirements**
- Coordinate audio requirements with Audio Team
- Implement audio feedback systems as specified by Audio Team
- Use audio assets according to Audio Team specifications
- Implement audio effects according to Audio Team guidelines
- Test audio integration with Audio Team

### **Sound Integration**
- Use sound assets according to Audio Team pipeline
- Implement proper sound loading and management
- Coordinate sound requirements with Audio Team
- Test sound integration with Audio Team
- Document sound integration issues

## 🧪 Testing Requirements

### **Unit Testing**
- Write unit tests for all gameplay logic
- Test gameplay systems with mock data
- Test gameplay systems with different configurations
- Test edge cases and error conditions
- Test gameplay systems in isolation

### **Integration Testing**
- Test gameplay systems integration with other systems
- Test gameplay systems with real data
- Test gameplay systems under load
- Test gameplay systems with different configurations
- Test gameplay systems with different platforms

### **User Testing**
- Test gameplay systems with user feedback
- Test gameplay systems with Design Team
- Test gameplay systems with Art Team
- Test gameplay systems with Audio Team
- Test gameplay systems with QA Team

## 📊 Performance Requirements

### **Performance Budgets**
- **Gameplay Update Time**: < 5ms per frame
- **Gameplay Memory Usage**: < 100MB for gameplay systems
- **Gameplay CPU Usage**: < 50% of available CPU
- **Gameplay Network Usage**: < 10KB/s for gameplay data

### **Performance Monitoring**
- Monitor gameplay system performance in real-time
- Profile gameplay systems regularly
- Log performance violations and issues
- Alert on performance budget violations
- Generate performance reports

## 🔒 Security Rules

### **Gameplay Security**
- Validate all gameplay inputs and data
- Implement proper error handling and logging
- Use secure coding practices for gameplay code
- Implement proper memory management
- Validate all gameplay state changes

### **Network Security**
- Validate all network gameplay data
- Implement proper network security for multiplayer
- Use secure communication protocols
- Validate all network gameplay state
- Implement proper anti-cheat measures

## 📝 Documentation Requirements

### **Code Documentation**
- Document all gameplay systems with examples
- Document gameplay system interfaces
- Document gameplay system dependencies
- Document gameplay system limitations
- Document troubleshooting guides

### **Design Documentation**
- Document gameplay design decisions
- Document gameplay mechanics implementation
- Document gameplay balance calculations
- Document gameplay system interactions
- Document gameplay system limitations

## 🔄 Quality Gates

### **Pre-Implementation Gates**
- [ ] Design is reviewed and approved by `game-designer`
- [ ] Performance requirements are defined
- [ ] Testing requirements are defined
- [ ] Art requirements are defined
- [ ] Audio requirements are defined

### **Implementation Gates**
- [ ] Code follows gameplay coding standards
- [ ] Performance requirements are met
- [ ] Art requirements are met
- [ ] Audio requirements are met
- [ ] Tests are written and passing

### **Pre-Release Gates**
- [ ] All gameplay mechanics are implemented as specified
- [ ] All gameplay systems are balanced and tested
- [ ] All gameplay systems are performant
- [ ] All gameplay systems are secure
- [ ] All gameplay systems are documented

## 🚀 Examples

### **Correct** (data-driven):

#### Configuration Example
```gdscript
var damage: float = config.get_value("combat", "base_damage", 10.0)
var speed: float = stats_resource.movement_speed * delta
```

#### Event-Driven Example
```gdscript
# Event-driven gameplay system
signal health_changed(new_health: float)
signal game_over(winner: String)

func take_damage(amount: float) -> void:
    health -= amount
    emit_signal("health_changed", health)
    if health <= 0:
        emit_signal("game_over", "enemy")
```

### **Incorrect** (hardcoded):

#### Hardcoded Values Example
```gdscript
var damage: float = 25.0   # VIOLATION: hardcoded gameplay value
var speed: float = 5.0      # VIOLATION: not from config, not using delta
```

#### Direct UI Access Example
```gdscript
func update_ui() -> void:
    ui.health_bar.value = health  # VIOLATION: direct UI access
    ui.score_text.text = str(score)  # VIOLATION: direct UI access
```

## 📋 Checklist

### **Development Checklist**
- [ ] Gameplay values are data-driven
- [ ] Delta time is used for time-dependent calculations
- [ ] Event-driven architecture is used
- [ ] Unit tests are written and passing
- [ ] Design documents are referenced

### **Review Checklist**
- [ ] Code reviewed by `gameplay-programmer`
- [ ] Design reviewed by `game-designer`
- [ ] Art reviewed by `art-director`
- [ ] Audio reviewed by `audio-director`
- [ ] QA reviewed by `qa-lead`

---

*Gameplay Code Rules Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: Design Team, Programming Team*
*Integration: Art Team, Audio Team, QA Team*