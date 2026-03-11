---
name: unity-asset-guide
description: Use when writing Unity package code (FEEL, SOAP, DOTween), debugging package-related issues, or checking best practices before implementation.
argument-hint: "[package]"
user-invocable: true
---

# Unity Assets Guidelines

Best practices and pitfalls for Unity packages used in this project.

## Available Packages

| Package | Description | Status |
|---------|-------------|--------|
| soap | Scriptable Object Architecture | ✅ |
| feel | MMFeedbacks feedback system | ✅ |
| dotween | Tween animation | 🚧 Coming soon |

## Instructions

If argument provided (`$ARGUMENTS`):
1. Read `./docs/$ARGUMENTS/patterns.md` for usage patterns
2. Read `./docs/$ARGUMENTS/pitfalls.md` for checklist and troubleshooting
3. If debugging specific issue, check detailed files in `./docs/$ARGUMENTS/pitfalls/`

If no argument provided:
- Display available packages list above

---

## SOAP (Scriptable Object Architecture)

### Overview
SOAP provides a robust architecture for managing game data through ScriptableObjects, enabling data-driven design and runtime configuration.

### Usage Patterns
- Data containers for game configuration
- Runtime state management
- Event systems and messaging
- Asset references and management

### Common Pitfalls
- Memory leaks from circular references
- Serialization issues with complex data types
- Performance considerations for large datasets

---

## FEEL (MMFeedbacks Feedback System)

### Overview
FEEL provides a comprehensive feedback system for creating responsive game feel through visual, audio, and haptic feedback.

### Usage Patterns
- Impact feedback and screen shake
- UI feedback animations
- Particle system integration
- Audio feedback coordination

### Common Pitfalls
- Performance impact from excessive feedback
- Timing synchronization issues
- Platform-specific feedback differences

---

## DOTween (Tween Animation)

### Overview
DOTween provides high-performance tweening animations for smooth object transformations and UI animations.

### Usage Patterns
- Object movement and rotation
- UI element transitions
- Color and material animations
- Sequenced animation chains

### Common Pitfalls
- Memory management for ongoing tweens
- Performance optimization for batch animations
- Timing and sequencing conflicts

---

*Unity Asset Guidelines*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
