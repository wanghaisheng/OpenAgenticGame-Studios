# Cocos Creator Scene Operations Reference

## Overview

This document provides detailed reference for scene operations in Cocos Creator, covering node management, scene lifecycle, and automation workflows.

## Scene Operations

### Scene Management Commands

#### Open Scene
```bash
# Open specific scene
cocos-skills scene open-scene <scene-path>

# Open last opened scene
cocos-skills scene open-last-scene

# Open scene in read-only mode
cocos-skills scene open-scene <scene-path> --read-only
```

#### Save Scene
```bash
# Save current scene
cocos-skills scene save-scene

# Save scene with custom path
cocos-skills scene save-scene --path <custom-path>

# Save scene with backup
cocos-skills scene save-scene --backup
```

#### Create Scene
```bash
# Create new scene
cocos-skills scene create-scene <scene-name>

# Create scene with template
cocos-skills scene create-scene <scene-name> --template <template-name>

# Create scene with initial node
cocos-skills scene create-scene <scene-name> --initial-node <node-data>
```

#### Delete Scene
```bash
# Delete scene
cocos-skills scene delete-scene <scene-path>

# Delete scene with confirmation
cocos-skills scene delete-scene <scene-path> --confirm
```

### Scene Information

#### Scene Properties
```bash
# Get scene properties
cocos-skills scene get-properties

# Get scene metadata
cocos-skills scene get-metadata

# Get scene statistics
cocos-skills scene get-stats
```

#### Scene Validation
```bash
# Validate scene structure
cocos-skills scene validate-structure

# Validate scene references
cocos-skills validate-references

# Validate scene assets
cocos-skills validate-assets
```

---

## Node Operations

### Node Creation

#### Create Node
```bash
# Create basic node
cocos-skills node create-node '{"name":"NewNode","type":"Node"}'

# Create node with parent
cocos-skills node create-node '{"name":"ChildNode","parent":"<parent-uuid>"}'

# Create node with position
cocos-skills node create-node '{"name":"PositionedNode","x":100,"y":200}'

# Create node with properties
cocos-skills node create-node '{"name":"CustomNode","properties":{"width":100,"height":100}}'
```

#### Create Component
```bash
# Add component to node
cocos-skills component add-component <node-uuid> <component-type>

# Create node with component
cocos-skills node create-node '{"name":"NodeWithComponent","components":[{"type":"Sprite","properties":{"spriteFrame":"path/to/sprite"}}]}'

# Add multiple components
cocos-skills component add-components <node-uuid> '[{"type":"Sprite"},{"type":"Animation"}]'
```

### Node Operations

#### Find Nodes
```bash
# Find node by name
cocos-skills node find-by-name <scene-path> <node-name>

# Find node by type
cocos-skills node find-by-type <scene-path> <component-type>

# Find node by UUID
cocos-skills node get-node <node-uuid>

# Find all nodes
cocos-skills node list-nodes <scene-path>
```

#### Node Properties
```bash
# Get node properties
cocos-skills node get-properties <node-uuid>

# Set node property
cocos-skills node set-property <node-uuid> <property-name> <value>

# Set multiple properties
cocos-skills node set-properties <node-uuid> '{"x":100,"y":200,"scale":1.5}'

# Get node position
cocos-skills node get-position <node-uuid>

# Set node position
cocos-skills node set-position <node-uuid> <x> <y>
```

#### Node Hierarchy
```bash
# Get parent node
cocos-skills node get-parent <node-uuid>

# Get children nodes
cocos-skills node get-children <node-uuid>

# Move node to new parent
cocos-skills node set-parent <node-uuid> <new-parent-uuid>

# Remove node from parent
cocos-skills node remove-from-parent <node-uuid>

# Delete node
cocos-skills node delete-node <node-uuid>
```

### Node Transform
```bash
# Get transform
cocos-skills node get-transform <node-uuid>

# Set position
cocos-skills node set-position <node-uuid> <x> <y>

# Set rotation
cocos-skills node set-rotation <node-uuid> <angle>

# Set scale
cocos-skills node set-scale <node-uuid> <scale-x> <scale-y>

# Set anchor
cocos-skills node set-anchor <node-uuid> <anchor-x> <anchor-y>

# Set size
cocos-skills node set-size <node-uuid> <width> <height>
```

---

## Scene Tree Operations

### Tree Navigation
```bash
# Get scene tree structure
cocos-skills scene query-node-tree <scene-path>

# Get minimal tree (only names and UUIDs)
cocos-skills scene query-node-tree <scene-path> minimal

# Get full tree (all properties)
cocos-skills scene query-node-tree <scene-path> full

# Get tree statistics
cocos-skills scene query-node-tree <scene-path> stats
```

### Tree Analysis
```bash
# Count nodes
cocos-skills scene count-nodes <scene-path>

# Count nodes by type
cocos-skills scene count-nodes-by-type <scene-path> <component-type>

# Find orphaned nodes
cocos-skills scene find-orphaned-nodes <scene-path>

# Find duplicate nodes
cocos-skills scene find-duplicate-nodes <scene-path>
```

### Tree Validation
```bash
# Validate tree structure
cocos-skills scene validate-tree <scene-path>

# Check for circular references
cocos-skills scene check-circular-references <scene-path>

# Validate node naming
cocos-skills scene validate-node-naming <scene-path>

# Check component dependencies
cocos-skills scene check-dependencies <scene-path>
```

---

## Scene Templates

### Template Management
```bash
# List available templates
cocos-skills template list-templates

# Create scene from template
cocos-skills scene create-from-template <scene-name> <template-name>

# Create custom template
cocos-skills template create-template <template-name> <template-data>

# Apply template to existing scene
cocos-skills template apply-template <scene-path> <template-name>
```

### Built-in Templates
- **Basic Scene**: Empty scene with Canvas and Camera
- **UI Scene**: Scene with UI components
- **Game Scene**: Scene with game components
- **Menu Scene**: Scene with menu components
- **Loading Scene**: Scene with loading components

### Custom Templates
```json
{
  "name": "CustomGameScene",
  "description": "Custom game scene template",
  "nodes": [
    {
      "name": "Canvas",
      "type": "Canvas",
      "properties": {
        "designResolution": {
          "width": 1920,
          "height": 1080
        }
      },
      "children": [
        {
          "name": "Camera",
          "type": "Camera",
          "properties": {
            "clearFlags": 7
          }
        }
      ]
    }
  ]
}
```

---

## Performance Optimization

### Batch Operations
```bash
# Batch create nodes
cocos-skills node create-batch '[{"name":"Node1"},{"name":"Node2"},{"name":"Node3"}]'

# Batch set properties
cocos-skills node set-properties-batch <node-uuids> '[{"x":100},{"y":200}]'

# Batch save scenes
cocos-skills scene save-all-scenes
```

### Memory Management
```bash
# Check memory usage
cocos-skills scene check-memory <scene-path>

# Optimize scene
cocos-skills scene optimize <scene-path>

# Clean unused assets
cocos-skills scene clean-unused-assets <scene-path>

# Compress scene
cocos-skills scene compress <scene-path>
```

### Scene Streaming
```bash
# Enable scene streaming
cocos-skills scene enable-streaming <scene-path>

# Stream scene in background
cocos-skills scene stream-scene <scene-path> --background

# Check streaming status
cocos-skills scene streaming-status <scene-path>
```

---

## Debugging and Monitoring

### Debug Commands
```bash
# Enable debug mode
cocos-skills --debug

# Show verbose output
cocos-skills --verbose

# Show operation timing
cocos-skills --timing

# Show detailed logs
cocos-skills --logs
```

### Monitoring
```bash
# Monitor scene changes
cocos-skills scene monitor <scene-path>

# Watch for file changes
cocos-skills watch <scene-path>

# Check system health
cocos-skills health --detailed

# Performance profiling
cocos-skills profile <operation>
```

---

## Error Handling

### Common Errors
1. **Scene Not Found**: Check scene path and file existence
2. **Node Not Found**: Verify node UUID and scene context
3. **Invalid JSON**: Validate JSON syntax and data types
4. **Permission Denied**: Check file permissions and access rights
5. **Server Connection**: Verify Cocos Creator HTTP Server status

### Error Recovery
```bash
# Auto-retry failed operations
cocos-skills --retry

# Reset scene state
cocos-skills scene reset <scene-path>

# Recover from backup
cocos-skills scene recover <scene-path>

# Validate and repair scene
cocos-skills scene repair <scene-path>
```

---

## Integration Examples

### VS Code Integration
```typescript
// Example: Programmatic scene creation
import { CocosSkills } from 'cocos-skills';

const skills = new CocosSkills();

// Create scene programmatically
const scene = await skills.scene.createScene({
  name: "NewScene",
  template: "BasicScene",
  initialNodes: [
    {
      name: "Player",
      type: "Sprite",
      properties: { spriteFrame: "path/to/player.png" }
    }
  ]
});
```

### Build System Integration
```bash
# Pre-build scene validation
npm run validate-scenes

# Build with scene optimization
npm run build --optimize-scenes

# Deploy with scene validation
npm run deploy --validate-scenes
```

### CI/CD Integration
```bash
# Automated scene validation
cocos-skills scene validate-all-scenes --ci

# Automated scene optimization
cocos-skills scene optimize-all-scenes --ci

# Automated scene testing
cocos-skills scene test-all-scenes --ci
```

---

## Best Practices

### Scene Organization
- **Logical Grouping**: Group related nodes logically
- **Naming Conventions**: Use consistent naming conventions
- **Hierarchy Structure**: Maintain clean hierarchy structure
- **Asset Management**: Organize assets efficiently

### Performance Optimization
- **Batch Operations**: Use batch operations when possible
- **Memory Management**: Manage memory usage effectively
- **Asset Loading**: Load assets asynchronously
- **Scene Streaming**: Use scene streaming for large scenes

### Error Prevention
- **Input Validation**: Validate all input parameters
- **Type Safety**: Use TypeScript for type safety
- **Error Handling**: Implement comprehensive error handling
- **Logging**: Log operations for debugging

---

*Scene Operations Reference*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
