---
paths:
  - "src/ui/**"
  - "src/user-interface/**"
---

# UI Code Rules - Team-Based Architecture

## 🏗️ Team Responsibilities

### **Primary Team**: Art Team
- **Lead Agent**: `art-director`
- **Contributors**: `ux-designer`, `technical-artist`, `accessibility-specialist`
- **Programming Team**: `ui-programmer`, `lead-programmer`
- **QA Team**: `qa-lead`, `qa-tester`

### **Cross-Team Integration**
- **Design Team**: `game-designer` (gameplay feedback)
- **Audio Team**: `audio-director` (audio feedback)
- **Production Team**: `producer` (milestone coordination)

## 🎨 Core UI Rules

### **UI Architecture**
- UI must NEVER own or directly modify game state — display only, use commands/events to request changes
- All UI text must go through the localization system — no hardcoded user-facing strings
- Support both keyboard/mouse AND gamepad input for all interactive elements
- All animations must be skippable and respect user motion/accessibility preferences
- UI sounds trigger through the audio event system, not directly
- UI must never block the game thread
- Scalable text and colorblind modes are mandatory, not optional
- Test all screens at minimum and maximum supported resolutions

### **Team Coordination**
- UI features must be coordinated with Art Team
- UX requirements must be coordinated with UX Designer
- Technical requirements must be coordinated with Technical Artist
- Accessibility requirements must be coordinated with Accessibility Specialist
- Testing requirements must be coordinated with QA Team

## 🔧 Technical Rules

### **Code Organization**
- Use clear separation of concerns between UI logic and presentation
- Implement proper event-driven architecture for UI updates
- Use consistent naming conventions for UI components
- Implement proper error handling and logging
- Use object pooling for UI elements when appropriate

### **Performance Rules**
- Profile all UI systems for performance
- Optimize UI rendering and update cycles
- Use efficient UI update strategies
- Implement proper memory management for UI systems
- Monitor UI system performance in real-time

### **Accessibility Rules**
- Implement WCAG 2.1 AA compliance for all UI elements
- Support high contrast mode and colorblind-friendly palettes
- Implement keyboard navigation for all UI elements
- Support screen readers and other assistive technologies
- Test UI accessibility with Accessibility Specialist

## 🎮 Multi-Engine Support

### **Unity UI Rules**
- Use Unity's UI Toolkit or UGUI system
- Implement proper canvas scaling and resolution independence
- Use Unity's event system for UI interactions
- Optimize UI for Unity's rendering pipeline
- Support Unity's input system for multiple input types

### **Godot UI Rules**
- Use Godot's Control nodes and scene system
- Implement proper anchor-based layout system
- Use Godot's signal system for UI events
- Optimize UI for Godot's rendering pipeline
- Support Godot's input system for multiple input types

### **Unreal UI Rules**
- Use Unreal's UMG system for UI implementation
- Implement proper widget hierarchy and layout
- Use Unreal's delegate system for UI events
- Optimize UI for Unreal's rendering pipeline
- Support Unreal's input system for multiple input types

### **Cocos Creator UI Rules**
- Use Cocos Creator's UI components and system
- Implement proper layout and positioning system
- Use Cocos Creator's event system for UI interactions
- Optimize UI for web and mobile platforms
- Support Cocos Creator's input system for multiple input types

## 🎨 Art Integration

### **Visual Requirements**
- Implement UI according to Art Team specifications
- Use art assets according to Art Team pipeline
- Implement visual effects according to Art Team guidelines
- Test visual integration with Art Team
- Document visual integration issues

### **Asset Management**
- Use proper asset loading and management
- Implement asset optimization for UI
- Coordinate asset requirements with Art Team
- Test asset integration with Art Team
- Document asset integration issues

## 🔊 Audio Integration

### **Audio Requirements**
- Implement UI audio according to Audio Team specifications
- Use audio assets according to Audio Team pipeline
- Implement audio feedback systems
- Test audio integration with Audio Team
- Document audio integration issues

### **Sound Management**
- Use proper audio loading and management
- Implement audio optimization for UI
- Coordinate audio requirements with Audio Team
- Test audio integration with Audio Team
- Document audio integration issues

## 🧪 Testing Requirements

### **Unit Testing**
- Write unit tests for all UI logic
- Test UI components with mock data
- Test UI systems with different configurations
- Test edge cases and error conditions
- Test UI systems in isolation

### **Integration Testing**
- Test UI systems integration with gameplay systems
- Test UI systems with real data
- Test UI systems under load
- Test UI systems with different configurations
- Test UI systems with different platforms

### **User Testing**
- Test UI systems with user feedback
- Test UI systems with UX Designer
- Test UI systems with Art Team
- Test UI systems with Accessibility Specialist
- Test UI systems with QA Team

## 📊 Performance Requirements

### **Performance Budgets**
- **UI Update Time**: < 2ms per frame
- **UI Memory Usage**: < 50MB for UI systems
- **UI CPU Usage**: < 20% of available CPU
- **UI Render Time**: < 5ms per frame

### **Performance Monitoring**
- Monitor UI system performance in real-time
- Profile UI systems regularly
- Log performance violations and issues
- Alert on performance budget violations
- Generate performance reports

## 🔒 Security Rules

### **UI Security**
- Validate all UI inputs and data
- Implement proper error handling and logging
- Use secure coding practices for UI code
- Implement proper memory management
- Validate all UI state changes

### **Input Security**
- Validate all user inputs
- Implement proper input sanitization
- Use secure input handling practices
- Validate all input state changes
- Implement proper input validation

## 📝 Documentation Requirements

### **Code Documentation**
- Document all UI systems with examples
- Document UI component interfaces
- Document UI system dependencies
- Document UI system limitations
- Document troubleshooting guides

### **Design Documentation**
- Document UI design decisions
- Document UI implementation details
- Document UI asset requirements
- Document UI interaction patterns
- Document UI accessibility features

## 🔄 Quality Gates

### **Pre-Implementation Gates**
- [ ] Design is reviewed and approved by `art-director`
- [ ] UX requirements are defined
- [ ] Accessibility requirements are defined
- [ ] Performance requirements are defined
- [ ] Testing requirements are defined

### **Implementation Gates**
- [ ] Code follows UI coding standards
- [ ] Art requirements are met
- [ ] UX requirements are met
- [ ] Accessibility requirements are met
- [ ] Tests are written and passing

### **Pre-Release Gates**
- [ ] All UI elements are accessible
- [ ] All UI elements are responsive
- [ ] All UI elements are performant
- [ ] All UI elements are secure
- [ ] All UI elements are documented

## 🚀 Examples

### **Correct** (event-driven UI):

#### Event-Driven UI Example
```gdscript
# Event-driven UI system
signal health_changed(new_health: float)
signal game_over(winner: String)

func _ready() -> void:
    # Connect to gameplay events
    player.connect("health_changed", _on_health_changed)
    game.connect("game_over", _on_game_over)

func _on_health_changed(new_health: float) -> void:
    health_bar.value = new_health

func _on_game_over(winner: String) -> void:
    game_over_text.text = winner + " Wins!"
    game_over_panel.visible = true
```

#### Localized UI Example
```gdscript
# Localized UI text
func _ready() -> void:
    title_label.text = tr("ui.title")
    start_button.text = tr("ui.start_button")
    settings_button.text = tr("ui.settings_button")
```

### **Incorrect** (direct state modification):

#### Direct State Modification Example
```gdscript
func _ready() -> void:
    # VIOLATION: Directly modifying game state
    player.health = 100
    player.score = 0

func update_ui() -> void:
    # VIOLATION: Directly modifying UI state
    health_bar.value = player.health
    score_text.text = str(player.score)
```

#### Hardcoded Text Example
```gdscript
func _ready() -> void:
    # VIOLATION: Hardcoded UI text
    title_label.text = "Game Title"
    start_button.text = "Start Game"
    settings_button.text = "Settings"
```

## 📋 Checklist

### **Development Checklist**
- [ ] UI uses event-driven architecture
- [ ] All UI text is localized
- [ ] Multiple input types are supported
- [ ] Accessibility features are implemented
- [ ] Performance requirements are met

### **Review Checklist**
- [ ] Code reviewed by `ui-programmer`
- [ ] Design reviewed by `art-director`
- [ ] UX reviewed by `ux-designer`
- [ ] Accessibility reviewed by `accessibility-specialist`
- [ ] QA reviewed by `qa-lead`

---

*UI Code Rules Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: Art Team, Programming Team*
*Integration: Design Team, Audio Team, QA Team*
*Engines: Unity, Godot, Unreal, Cocos Creator*