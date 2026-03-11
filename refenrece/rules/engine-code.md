---
paths:
  - "src/core/**"
  - "src/engine/**"
---

# Engine Code Rules - Team-Based Architecture

## 🏗️ Team Responsibilities

### **Primary Team**: Programming Team
- **Lead Agent**: `lead-programmer`
- **Contributors**: `engine-programmer`, engine specialists
- **QA Team**: `qa-lead`, `performance-analyst`
- **Art Team**: `technical-artist` (for engine-specific art)

### **Engine Specialists**
- **Unity**: `unity-specialist`, `unity-dots-specialist`, `unity-shader-specialist`
- **Godot**: `godot-specialist`, `godot-gdscript-specialist`, `godot-shader-specialist`
- **Unreal**: `unreal-specialist`, `ue-blueprint-specialist`, `ue-gas-specialist`
- **Cocos**: `cocos-creator-specialist`

## 🔧 Core Engine Rules

### **Performance Rules**
- ZERO allocations in hot paths (update loops, rendering, physics) — pre-allocate, pool, reuse
- All engine APIs must be thread-safe OR explicitly documented as single-thread-only
- Profile before AND after every optimization — document the measured numbers
- Engine code must NEVER depend on gameplay code (strict dependency direction: engine <- gameplay)
- Every public API must have usage examples in its doc comment
- Changes to public interfaces require a deprecation period and migration guide
- Use RAII / deterministic cleanup for all resources
- All engine systems must support graceful degradation

### **Multi-Engine Compatibility**
- Before writing engine API code, consult `docs/engine-reference/` for the current engine version
- Engine-specific code must be isolated in engine-specific modules
- Use abstraction layers for cross-engine compatibility
- Document engine-specific limitations and workarounds
- Test engine-specific features on target platforms

### **Code Quality Rules**
- All engine code must be reviewed by `lead-programmer`
- Use consistent coding conventions for each engine
- Implement comprehensive error handling and logging
- Write unit tests for all engine systems
- Document all engine-specific APIs and limitations

## 🎮 Engine-Specific Rules

### **Unity Engine Rules**
- Follow Unity coding standards and best practices
- Use Unity-specific optimization techniques (DOTS, Job System, Burst)
- Implement proper asset management and loading strategies
- Use Unity's component-based architecture
- Optimize for Unity's garbage collection
- Support Unity's build pipeline and deployment

### **Godot Engine Rules**
- Follow GDScript coding standards and conventions
- Use Godot's scene and node system effectively
- Implement proper signal-based communication
- Optimize for Godot's performance characteristics
- Support Godot's export system and platforms
- Use Godot's resource management system

### **Unreal Engine Rules**
- Follow Unreal C++ coding standards
- Use Unreal's component and actor system
- Implement proper Blueprint integration
- Optimize for Unreal's performance characteristics
- Support Unreal's build system and deployment
- Use Unreal's asset management system

### **Cocos Creator Rules**
- Follow TypeScript coding standards
- Use Cocos Creator's component system
- Implement proper scene and node management
- Optimize for web and mobile platforms
- Support Cocos Creator's build system
- Use Cocos Creator's asset management system

## 📊 Performance Requirements

### **Performance Budgets**
- **Frame Time**: < 16.67ms (60 FPS)
- **Memory Usage**: < 512MB for engine systems
- **CPU Usage**: < 80% of available CPU
- **GPU Usage**: < 90% of available GPU

### **Performance Monitoring**
- Implement performance profiling hooks
- Monitor engine system performance in real-time
- Log performance metrics and violations
- Alert on performance budget violations
- Generate performance reports

## 🔒 Security Rules

### **Engine Security**
- Validate all external inputs and data
- Implement proper error handling and logging
- Use secure coding practices for network code
- Implement proper memory management
- Validate all file system operations

### **Platform Security**
- Follow platform-specific security guidelines
- Implement proper sandboxing where needed
- Validate all platform-specific APIs
- Use secure communication protocols
- Implement proper data encryption

## 🧪 Testing Requirements

### **Unit Testing**
- Write unit tests for all engine systems
- Test engine-specific APIs and functionality
- Test performance-critical code paths
- Test cross-platform compatibility
- Test edge cases and error conditions

### **Integration Testing**
- Test engine integration with gameplay systems
- Test multi-engine compatibility
- Test performance under load
- Test platform-specific features
- Test asset loading and management

### **Performance Testing**
- Profile engine performance regularly
- Test performance budgets compliance
- Test performance optimizations
- Test performance regressions
- Generate performance reports

## 📝 Documentation Requirements

### **API Documentation**
- Document all public APIs with examples
- Document engine-specific limitations
- Document performance characteristics
- Document platform-specific behavior
- Document troubleshooting guides

### **Architecture Documentation**
- Document engine architecture decisions
- Document design patterns used
- Document dependency relationships
- Document performance considerations
- Document future roadmap

## 🔄 Quality Gates

### **Pre-Implementation Gates**
- [ ] Design is reviewed and approved by `lead-programmer`
- [ ] Performance requirements are defined
- [ ] Security requirements are defined
- [ ] Testing requirements are defined
- [ ] Documentation requirements are defined

### **Implementation Gates**
- [ ] Code follows engine coding standards
- [ ] Performance requirements are met
- [ ] Security requirements are met
- [ ] Unit tests are written and passing
- [ ] Integration tests are written and passing

### **Pre-Release Gates**
- [ ] All performance budgets are met
- [ ] All security requirements are met
- [ ] All tests are passing
- [ ] Documentation is complete and accurate
- [ ] Platform compatibility is verified

## 🚀 Examples

### **Correct** (zero-alloc hot path):

#### Unity Example
```csharp
// Pre-allocated array reused each frame
private readonly List<GameObject> _nearbyCache = new List<GameObject>();

void Update() {
    _nearbyCache.Clear();  // Reuse, don't reallocate
    _spatialGrid.QueryRadius(position, radius, _nearbyCache);
}
```

#### Godot Example
```gdscript
# Pre-allocated array reused each frame
var _nearby_cache: Array[Node3D] = []

func _physics_process(delta: float) -> void:
    _nearby_cache.clear()  # Reuse, don't reallocate
    _spatial_grid.query_radius(position, radius, _nearby_cache)
```

### **Incorrect** (allocating in hot path):

#### Unity Example
```csharp
void Update() {
    var nearby = new List<GameObject>();  // VIOLATION: allocates every frame
    nearby = GetTree().GetNodesInGroup("enemies");  // VIOLATION: tree query every frame
}
```

#### Godot Example
```gdscript
func _physics_process(delta: float) -> void:
    var nearby: Array[Node3D] = []  # VIOLATION: allocates every frame
    nearby = get_tree().get_nodes_in_group("enemies")  # VIOLATION: tree query every frame
```

## 📋 Checklist

### **Development Checklist**
- [ ] Code follows engine-specific standards
- [ ] Performance budgets are met
- [ ] Security requirements are met
- [ ] Tests are written and passing
- [ ] Documentation is complete

### **Review Checklist**
- [ ] Code reviewed by `lead-programmer`
- [ ] Performance reviewed by `performance-analyst`
- [ ] Security reviewed by `security-engineer`
- [ ] Art integration reviewed by `technical-artist`
- [ ] QA reviewed by `qa-lead`

---

*Engine Code Rules Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: Programming Team*
*Engines: Unity, Godot, Unreal, Cocos Creator*