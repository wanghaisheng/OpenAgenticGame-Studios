---
name: cocos-creator-dev
description: Comprehensive Cocos Creator 3.x development guide covering TypeScript scripting, component system, node hierarchy, scene management, resource loading, and event handling. Use this skill when: (1) Writing or debugging Cocos Creator 3.x TypeScript scripts, (2) Creating and managing components and their lifecycle, (3) Working with nodes, hierarchy, and scene organization, (4) Loading and managing game resources, (5) Implementing event systems and input handling, (6) Optimizing performance and memory in Cocos Creator projects, (7) Migrating from 2.x to 3.x versions
---

# Cocos Creator 3.x Development Guide

Guide for Cocos Creator 3.x game development using TypeScript.

## Quick Start

### Basic Component Template

```typescript
import { _decorator, Component, Node } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('MyComponent')
export class MyComponent extends Component {
    @property(Node)
    targetNode: Node = null;

    @property
    speed: number = 10;

    onLoad() {
        // Initialization
    }

    start() {
        // First frame update
    }

    update(deltaTime: number) {
        // Per-frame update
    }
}
```

### Common Operations

**Add component dynamically:**
```typescript
this.node.addComponent(MyComponent);
```

**Get component:**
```typescript
const comp = this.node.getComponent(MyComponent);
```

**Load scene:**
```typescript
director.loadScene('SceneName');
```

**Load resource:**
```typescript
resources.load('textures/sprite', SpriteFrame, (err, asset) => {
    this.node.getComponent(Sprite).spriteFrame = asset;
});
```

## Reference Documentation

For detailed information on specific topics, consult these reference files:

- **Script Basics**: [references/script-basics.md](references/script-basics.md) - TypeScript setup, decorators, class definitions, property declarations
- **Component System**: [references/component-system.md](references/component-system.md) - Lifecycle methods, component management, execution order
- **Node & Hierarchy**: [references/node-hierarchy.md](references/node-hierarchy.md) - Node creation, traversal, transformations, coordinate systems
- **Scene Management**: [references/scene-management.md](references/scene-management.md) - Scene loading, persist nodes, preloading
- **Resource Management**: [references/resource-management.md](references/resource-management.md) - Asset loading, releasing, Asset Bundles, memory management
- **Event System**: [references/event-system.md](references/event-system.md) - Input handling, custom events, node events

## Development Guidelines

### Version Check

Always confirm the user is working with **Cocos Creator 3.x**, not 2.x. APIs and workflows differ significantly.

### Code Style

- Use **TypeScript** exclusively (JavaScript not supported in 3.x)
- Follow decorator pattern: `@ccclass`, `@property`
- Use type annotations for all properties
- Prefer `this.node` for current node access

### Performance Best Practices

- Release unused resources with `assetManager.releaseAsset()`
- Use object pooling for frequently created/destroyed nodes
- Cache component references instead of repeated `getComponent()` calls
- Use `scheduleOnce` instead of timers for one-time delays

### Common Pitfalls

- **Lifecycle order**: `onLoad` → `start` → `update`. Don't access other components in `onLoad` if they might not be ready.
- **Resource leaks**: Always release dynamically loaded assets
- **Node activation**: Check `node.active` before accessing components
- **Scene switching**: Use persist nodes for data that needs to survive scene changes

## Key APIs Reference

### Node Operations
- `this.node` - Current node
- `this.node.parent` - Parent node
- `this.node.children` - Child nodes array
- `this.node.addChild(child)` - Add child node
- `this.node.removeFromParent()` - Remove from parent
- `this.node.destroy()` - Destroy node
- `this.node.setPosition(x, y, z)` - Set position
- `this.node.setRotation(x, y, z)` - Set rotation
- `this.node.setScale(x, y, z)` - Set scale

### Component Operations
- `this.node.addComponent(T)` - Add component
- `this.node.getComponent(T)` - Get component
- `this.getComponentInChildren(T)` - Get component in children
- `this.getComponentsInChildren(T)` - Get all components in children

### Scene Operations
- `director.loadScene(name)` - Load scene
- `director.preloadScene(name)` - Preload scene
- `director.getScene()` - Get current scene
- `game.addPersistRoot(node)` - Add persist node
- `game.removePersistRoot(node)` - Remove persist node

### Resource Operations
- `resources.load(path, type, callback)` - Load resource
- `assetManager.loadRemote(url, type, callback)` - Load remote resource
- `assetManager.releaseAsset(asset)` - Release resource
- `resources.loadDir(path, type, callback)` - Load directory

### Event Operations
- `this.node.on(type, callback, target)` - Register event
- `this.node.off(type, callback, target)` - Unregister event
- `this.node.emit(type, detail)` - Emit event
- `input.on(type, callback, target)` - Register input event

## External Resources

- **Official Manual**: https://docs.cocos.com/creator/3.8/manual/zh/
- **API Reference**: https://docs.cocos.com/creator/3.8/api/zh/
- **Example Projects**: https://github.com/cocos/cocos-example-projects

## Troubleshooting

### Component Not Found
- Verify component is attached in editor
- Check node is active: `if (this.node.active)`
- Use `getComponentInChildren()` for nested components

### Scene Not Loading
- Check scene name in Build Settings
- Verify scene is added to build
- Use `preloadScene()` for large scenes

### Memory Leaks
- Release assets after use
- Destroy unused nodes
- Remove event listeners in `onDestroy`
- Use Asset Bundles for modular loading

### Performance Issues
- Profile with Chrome DevTools
- Reduce draw calls with batching
- Use object pooling
- Optimize sprite atlases
- Check script execution time in updates

## When to Read References

Read specific reference files when:

- **script-basics.md**: Creating new components, defining properties, configuring TypeScript
- **component-system.md**: Implementing lifecycle callbacks, managing component dependencies
- **node-hierarchy.md**: Creating/destroying nodes, building scene hierarchy, coordinate transformations
- **scene-management.md**: Loading scenes, passing data between scenes, managing game flow
- **resource-management.md**: Loading assets, managing memory, using Asset Bundles
- **event-system.md**: Handling user input, implementing custom events, component communication

## Decision Guide

**Multiple valid approaches?** Use high freedom - provide options and let context guide choice.

**Standard pattern exists?** Use medium freedom - provide template code with parameters.

**Error-prone operation?** Use low freedom - provide specific, validated code pattern.
