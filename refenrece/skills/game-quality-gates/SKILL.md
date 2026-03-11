---
name: game-quality-gates
description: Game development quality gates and mandatory checks. Activate when building, reviewing, debugging, or deploying any game project (H5/Canvas/WebGL/Phaser/Three.js/2D/3D). Covers state cleanup, lifecycle management, input handling, audio, persistence, networking, anti-cheat, and performance. Use as pre-deploy checklist or when diagnosing game-specific bugs (state leaks, phantom timers, buff conflicts, memory growth, touch issues). From dev/game-quality-gates-main integrated quality gates framework.
---

# Game Quality Gates

Mandatory quality standards for all game projects. Based on 70+ real bugs and industry best practices.

## Core Principle

> Bugs come from **cross-state interactions**, not individual features.
> Each feature works alone; they break in combination.

## 12 Universal Rules (all games)

### 1. Single Cleanup Entry Point 🔄
All exit paths (death/level-complete/quit/pause/scene-switch) call ONE cleanup method with options.

```js
cleanupGameState(opts) {
  // Fixed order: sub-objects → buffs+timers → UI → projectiles → (optional) enemies/controls/events
}
// Every exit: resetBall(), levelComplete(), gameOver(), onShutdown() → calls this
```

**New feature = add one line here. Never scatter cleanup across exits.**

### 2. Respect Active Buffs ⚡
Any code modifying attributes (speed/attack/size/defense) must check for active temporary effects first.

```js
// ❌ speed = Math.max(speed, BASE_SPEED);  // ignores slow buff
// ✅ speed = Math.max(speed, this._currentBaseSpeed);  // buff-aware baseline
```

### 3. Cache Before Destroy 📦
Extract all needed data before `destroy()`/`dispose()`/`remove()`.

```js
const { x, y } = obj; const color = obj.getData('color');
obj.destroy();
spawnParticles(x, y, color);
```

### 4. Timers Follow Lifecycle ⏰
Track all `setTimeout`/`setInterval`/`delayedCall`/`rAF`. Cancel in cleanup.

```js
this.activeTimers.push(this.time.delayedCall(10000, cb));
// In cleanup:
this.activeTimers.forEach(timer => timer.remove());
```

### 5. Input State Consistency 🎮
Never mix input methods (touch+keyboard+mouse) without explicit state.

```js
// ❌ if (pointer.isDown || key.isDown) attack();
// ✅ if (this.inputMethod === 'touch' && pointer.isDown) attack();
```

### 6. Audio Pool Management 🔊
Reuse audio instances; never create new sounds in loops.

```js
// ❌ this.sound.play('shoot'); // each call creates instance
// ✅ this.shootSound = this.sound.add('shoot'); // create once
// this.shootSound.play(); // reuse
```

### 7. Memory Leak Prevention 🧹
Remove all event listeners, references, and external callbacks.

```js
// In cleanup:
this.events.off('pointerdown', this.onPointerDown);
this.externalCallback = null;
```

### 8. State Validation ⚖️
Validate all critical state before use (null/undefined checks).

```js
if (!this.player || !this.player.active) return;
```

### 9. Async Operation Safety 🔄
Never assume async operations complete in order.

```js
// ❌ loadLevel(); spawnEnemies(); // enemies may spawn before level loads
// ✅ await loadLevel(); spawnEnemies(); // proper sequencing
```

### 10. Resource Loading Safety 📦
Always check resource existence before use.

```js
if (!this.textures.exists('player')) {
  this.textures.add('player', 'assets/player.png');
}
```

### 11. Error Boundary Implementation 🛡️
Wrap critical operations in try-catch with graceful fallbacks.

```js
try {
  this.player.move(x, y);
} catch (e) {
  console.error('Player move failed:', e);
  this.player.reset();
}
```

### 12. Performance Budgeting ⚡
Set and enforce performance budgets (FPS, memory, draw calls).

```js
if (this.physics.world.bodies.length > 100) {
  console.warn('Physics body count exceeds budget');
}
```

---

## Platform-Specific Gates

### Web (H5/Canvas/WebGL)
- **Canvas Memory**: Never exceed 16MB texture memory
- **Audio Context**: Handle audio context suspension/resume
- **Touch Events**: Prevent default touch behaviors
- **LocalStorage**: Check quota before writing

### Mobile
- **Battery Impact**: Reduce effects on low battery
- **Network**: Handle offline/disconnected states
- **Memory**: Monitor and limit memory growth
- **Performance**: Adapt to device capabilities

### Desktop
- **Window Focus**: Pause/resume on focus changes
- **Keyboard**: Handle all keyboard shortcuts
- **Mouse**: Prevent cursor lock issues
- **File System**: Handle file access permissions

---

## Anti-Cheat Gates

### Client-Side Validation
- **Server Validation**: Never trust client data
- **Checksum**: Validate critical game state
- **Rate Limiting**: Prevent rapid actions
- **Obfuscation**: Protect sensitive code

### Network Security
- **HTTPS**: Always use secure connections
- **Token Validation**: Validate all tokens
- **Input Sanitization**: Sanitize all inputs
- **Error Handling**: Don't expose internal errors

---

## Performance Gates

### Memory Management
- **Object Pooling**: Reuse objects instead of creating/destroying
- **Texture Atlases**: Combine small textures
- **Garbage Collection**: Minimize GC pressure
- **Memory Leaks**: Regular memory leak detection

### Rendering Optimization
- **Draw Calls**: Minimize draw calls
- **Culling**: Implement frustum culling
- **LOD**: Use level of detail systems
- **Batching**: Batch similar operations

### Physics Optimization
- **Collision Detection**: Optimize collision detection
- **Body Count**: Limit active physics bodies
- **Update Frequency**: Reduce physics update frequency
- **Spatial Partitioning**: Use spatial partitioning

---

## Testing Gates

### Unit Testing
- **Coverage**: Minimum 80% code coverage
- **Edge Cases**: Test all edge cases
- **Performance**: Include performance tests
- **Integration**: Test component integration

### Integration Testing
- **Cross-Platform**: Test on all target platforms
- **Cross-Browser**: Test on all target browsers
- **Device Testing**: Test on various devices
- **Network**: Test network conditions

### Stress Testing
- **Memory**: Test memory limits
- **Performance**: Test performance limits
- **Load**: Test high-load scenarios
- **Longevity**: Test long-running sessions

---

## Deployment Gates

### Pre-Deployment Checklist
- [ ] All quality gates passed
- [ ] Performance benchmarks met
- [ ] Security audit completed
- [ ] Accessibility compliance verified
- [ ] Localization tested
- [ ] Documentation updated

### Post-Deployment Monitoring
- **Error Tracking**: Monitor error rates
- **Performance**: Monitor performance metrics
- **User Feedback**: Collect and analyze feedback
- **Analytics**: Track usage patterns

---

## Bug Prevention Checklist

### Common Bug Patterns
- [ ] State leaks between scenes
- [ ] Phantom timers after cleanup
- [ ] Memory growth over time
- [ ] Input conflicts between methods
- [ ] Audio instance proliferation
- [ ] Event listener memory leaks
- [ ] Async operation race conditions
- [ ] Resource loading failures
- [ ] Performance degradation
- [ ] Cross-platform inconsistencies

### Prevention Strategies
- **Code Review**: Mandatory code review for all changes
- **Automated Testing**: Comprehensive automated test suite
- **Static Analysis**: Use static analysis tools
- **Performance Profiling**: Regular performance profiling
- **Security Audits**: Regular security audits

---

## Quality Metrics

### Code Quality
- **Complexity**: Maintain low cyclomatic complexity
- **Duplication**: Minimize code duplication
- **Documentation**: Maintain comprehensive documentation
- **Testing**: Maintain high test coverage

### Performance Metrics
- **FPS**: Maintain target FPS (60/30)
- **Memory**: Stay within memory budget
- **Load Time**: Meet load time targets
- **Network**: Optimize network usage

### User Experience
- **Responsiveness**: Ensure responsive UI
- **Accessibility**: Support accessibility features
- **Localization**: Support multiple languages
- **Compatibility**: Ensure cross-platform compatibility

---

## Implementation Guidelines

### Code Organization
- **Single Responsibility**: Each function has single responsibility
- **DRY Principle**: Don't repeat yourself
- **SOLID Principles**: Follow SOLID principles
- **Clean Code**: Write clean, readable code

### Error Handling
- **Graceful Degradation**: Degrade gracefully on errors
- **User Feedback**: Provide clear error messages
- **Recovery**: Implement error recovery mechanisms
- **Logging**: Log all errors for debugging

### Security
- **Input Validation**: Validate all inputs
- **Output Encoding**: Encode all outputs
- **Authentication**: Implement proper authentication
- **Authorization**: Implement proper authorization

---

## Tools and Resources

### Quality Assurance Tools
- **Linters**: Use code quality linters
- **Static Analysis**: Use static analysis tools
- **Testing Frameworks**: Use comprehensive testing frameworks
- **Performance Tools**: Use performance profiling tools

### Monitoring Tools
- **Error Tracking**: Use error tracking services
- **Performance Monitoring**: Use performance monitoring
- **User Analytics**: Use user analytics tools
- **Security Scanning**: Use security scanning tools

### Documentation Tools
- **API Documentation**: Generate API documentation
- **Code Comments**: Maintain comprehensive code comments
- **User Guides**: Create user-friendly guides
- **Technical Specs**: Write detailed technical specifications

---

## Continuous Improvement

### Quality Metrics Tracking
- **Bug Rate**: Track bug discovery rate
- **Fix Time**: Track bug fix time
- **Performance**: Track performance metrics
- **User Satisfaction**: Track user satisfaction

### Process Improvement
- **Retrospectives**: Regular retrospectives
- **Process Updates**: Update processes based on feedback
- **Tool Updates**: Keep tools up to date
- **Training**: Regular team training

### Quality Culture
- **Standards**: Maintain high quality standards
- **Accountability**: Foster accountability for quality
- **Continuous Learning**: Encourage continuous learning
- **Knowledge Sharing**: Promote knowledge sharing

---

*Game Quality Gates*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
