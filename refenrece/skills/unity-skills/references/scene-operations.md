# Unity Skills Scene Operations Reference

## Overview

This document provides detailed reference for scene operations in Unity Skills CLI, covering node management, scene lifecycle, and automation workflows.

## Scene Operations

### Scene Management Commands

#### Open Scene
```bash
# Open specific scene by path
unity-skills scene open-scene <scene-path>

# Open last opened scene
unity-skills scene open-last-scene

# Open scene in read-only mode
unity-skills scene open-scene <scene-path> --read-only

# Open scene with specific camera
unity-skills scene open-scene <scene-path> --camera <camera-uuid>
```

#### Save Scene
```bash
# Save current scene
unity-skills scene save-scene

# Save scene with custom path
unity-skills scene save-scene --path <custom-path>

# Save scene with backup
unity-skills scene save-scene --backup

# Save scene with metadata
unity-skills scene save-scene --metadata <metadata>
```

#### Create Scene
```bash
# Create new scene
unity-skills scene create-scene <scene-name>

# Create scene with template
unity-skills scene create-scene <scene-name> --template <template-name>

# Create scene with initial node
unity-skills scene create-scene <scene-name> --initial-node <node-data>
```

#### Delete Scene
```bash
# Delete scene by path
unity-skills scene delete-scene <scene-path>

# Delete scene with confirmation
unity-skills scene delete-scene <scene-path> --confirm
```

### Scene Information

#### Scene Properties
```bash
# Get scene properties
unity-skills scene get-properties

# Get scene metadata
unity-skills scene get-metadata

# Get scene statistics
unity-skills scene get-stats

# Get scene hierarchy
unity-skills scene get-hierarchy
```

#### Scene Validation
```bash
# Validate scene structure
unity-skills scene validate-structure

# Validate scene references
unity-skills validate-references

# Validate scene assets
unity-skills validate-assets

# Validate scene components
unity-skills validate-components
```

---

## Node Operations

### Node Creation

#### Create Node
```bash
# Create basic node
unity-skills gameobject create-node '{"name":"NewNode","type":"Node"}'

# Create node with parent
unity-skills gameobject create-node '{"name":"ChildNode","parent":"<parent-uuid>"}'

# Create node with position
unity-skills gameobject create-node '{"name":"PositionedNode","x":100,"y":200,"z":0}'

# Create node with properties
unity-skills gameobject create-node '{"name":"CustomNode","properties":{"width":100,"height":100}}'

# Create primitive node
unity-skills gameobject create-node '{"name":"Cube","primitiveType":"Cube","x":0,"y":0,"z":0}'
```

#### Create Component
```bash
# Add component to node
unity-skills component add-component <node-uuid> <component-type>

# Create node with component
unity-skills gameobject create-node '{"name":"NodeWithComponent","components":[{"type":"Sprite","properties":{"spriteFrame":"path/to/sprite"}}]'

# Add multiple components
unity-skills component add-components <node-uuid> '[{"type":"Sprite"},{"type":"Animation"}]'
```

### Node Operations

#### Find Nodes
```bash
# Find node by name
unity-skills gameobject find-by-name <scene-path> <node-name>

# Find node by UUID
unity-skills gameobject get-node <node-uuid>

# Find nodes by type
unity-skills gameobject find-by-type <component-type>

# Find all nodes
unity-skills gameobject list-nodes <scene-path>

# Find nodes by tag
unity-skills gameobject find-by-tag <tag>
```

#### Node Properties
```bash
# Get node properties
unity-skills gameobject get-properties <node-uuid>

# Get node position
unity-skills gameobject get-position <node-uuid>

# Set node position
unity-skills gameobject set-position <node-uuid> <x> <y> <z>

# Set node rotation
unity-skills gameobject set-rotation <node-uuid> <x> <y> <z>

# Set node scale
unity-skills gameobject set-scale <node-uuid> <scale-x> <scale-y> <scale-z>

# Set node size
unity-skills gameobject set-size <node-uuid> <width> <height>
```

#### Node Hierarchy
```bash
# Get parent node
unity-skills gameobject get-parent <node-uuid>

# Get children nodes
unity-skills gameobject get-children <node-uuid>

# Get root nodes
unity-skills gameobject get-root-nodes <scene-path>

# Move node to new parent
unity-skills gameobject set-parent <node-uuid> <new-parent-uuid>

# Remove node from parent
unity-skills gameobject remove-from-parent <node-uuid>

# Delete node
unity-skills gameobject delete-node <node-uuid>

# Delete node and children
unity-skills gameobject delete-node <node-uuid> --include-children
```

### Node Transform
```bash
# Get transform
unity-skills gameobject get-transform <node-uuid>

# Set position
unity-skills gameobject set-position <node-uuid> <x> <y> <z>

# Set rotation
unity-skills gameobject set-rotation <node-uuid> <x> <y> <z>

# Set scale
unity-skills gameobject set-scale <node-uuid> <scale-x> <scale-y> <scale-z>

# Set anchor
unity-skills gameobject set-anchor <node-uuid> <anchor-x> <anchor-y>

# Set size
unity-skills gameobject set-size <node-uuid> <width> <height>

# Reset transform
unity-skills gameobject reset-transform <node-uuid>
```

### Node Physics
```bash
# Add rigidbody
unity-skills gameobject add-rigidbody <node-uuid>

# add collider
unity-skills gameobject add-collider <node-uuid> <collider-type>

# Set physics properties
unity-skills gameobject set-rigidbody-properties <node-uuid> <properties>

# Remove physics components
unity-skills gameobject remove-physics-components <node-uuid>
```

---

## Component Operations

### Component Management
```bash
# Add component to node
unity-skills component add-component <node-uuid> <component-type>

# Create node with component
unity-skills gameobject create-node '{"name":"NodeWithComponent","components":[{"type":"Sprite","properties":{"spriteFrame":"path/to/sprite"}}]'

# Add multiple components
unity-skills component add-components <node-uuid> '[{"type":"Sprite"},{"type":"Animation"}]'

# Remove component from node
unity-skills component remove-component <node-uuid> <component-uuid>

# Get components on node
unity-skills component get-components <node-uuid>

# Find component by type
unity-skills component find-by-type <component-type> <scene-path>
```

### Component Configuration
```bash
# Set component property
unity-skills component set-property <node-uuid> <component-uuid> <property-name> <value>

# Set multiple properties
unity-skills component set-properties <node-uuid> <properties-json>

# Get component properties
unity-skills component get-properties <node-uuid> <component-uuid>

# Validate component configuration
unity-skills component validate-component <node-uuid> <component-uuid>
```

### Component Templates
```bash
# Create component from template
unity-skills component create-from-template <template-name> <node-uuid>

# Apply template to component
unity-skills component apply-template <node-uuid> <template-name>

# List available templates
unity-skills component list-templates
```

---

## Asset Operations

### Asset Management
```bash
# Create new asset
unity-skills asset create-asset <asset-path> <asset-type>

# Import external asset
unity-skills asset import-asset <file-path> <target-path>

# Delete asset
unity-skills asset delete-asset <asset-path>

# Validate asset
unity-skills asset validate-asset <asset-path>

# Get asset metadata
unity-skills asset get-metadata <asset-path>

# List assets in directory
unity-skills asset list-assets <directory-path>
```

### Asset Types
- **Textures**: 2D/3D textures, sprite atlases, UI textures
- **Models**: 3D models, prefabs, animations
- **Audio**: Audio clips, music tracks, sound effects
- **Scripts**: TypeScript/C# scripts, editor scripts
- **Scenes**: Scene files, scene templates
- **Prefabs**: Prefab files, prefabs with components
- **Materials**: Material files, shader graphs
- **Animation**: Animation clips, state machines
- **UI**: UI prefabs, UI templates, UI components

---

## Batch Operations

### Batch Node Operations
```bash
# Batch create nodes
unity-skills gameobject create-batch '[{"name":"Node1","primitiveType":"Cube","x":0,"y":0,"z":0},{"name":"Node2","primitiveType":"Sphere","x":10,"y":0,"z":0}]'

# Batch set properties
unity-skills property set-batch <node-uuid> '{"x":100,"y":200,"z":0}'

# Batch add components
unity-skills component add-batch <node-uuid> '[{"type":"Rigidbody"},{"type":"Collider","properties":{"isTrigger":true}}]'

# Batch save scenes
unity-skills scene save-all-scenes

# Batch import assets
unity-skills asset import-batch <asset-list>
```

### Performance Optimization
```bash
# Enable optimization mode
unity-skills --optimize

# Check performance metrics
unity-skills performance check

# Optimize scene performance
unity-skills scene optimize <scene-path>

# Clean up unused assets
unity-skills cleanup <scene-path>
```

---

## Scene Templates

### Template Management
```bash
# List available templates
unity-skills template list-templates

# Create scene from template
unity-skills scene create-from-template <scene-name> <template-name>

# Create custom template
unity-skills template create-template <template-name> <template-data>

# Apply template to existing scene
unity-skills template apply-template <scene-path> <template-name>

# Update existing template
unity-skills template update-template <template-name> <template-data>
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

## Debugging and Monitoring

### Debug Commands
```bash
# Enable debug mode
unity-skills --debug

# Show verbose output
unity-skills --verbose

# Show detailed logs
unity-skills --logs

# Check system health
unity-skills health --detailed

# Check editor status
unity-skills editor status --detailed
```

### Monitoring
```bash
# Monitor scene changes
unity-skills monitor <scene-path>

# Watch for file changes
unity-skills watch <scene-path>

# Check performance metrics
unity-skills performance check

# Profile specific operation
unity-skills profile <operation> <parameters>
```

### Error Recovery
```bash
# Auto-retry failed operations
unity-skills --retry

# Reset editor state
unity-skills editor reset

# Recover from backup
unity-skills editor restore <backup-id>

# Validate editor state
unity-skills editor validate
```

---

## Integration Examples

### VS Code Integration
```typescript
// Example: Programmatic scene creation
import { UnitySkills } from 'unity-skills';

const skills = new UnitySkills();

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
unity-skills scene validate-all-scenes --ci

# Automated scene optimization
unity-skills scene optimize-all-scenes --ci

# Automated scene testing
unity-skills scene test-all-scenes --ci
```

---

## Best Practices

### Scene Organization
- **Logical Grouping**: Group related nodes logically
- **Naming Conventions**: Use consistent naming conventions
- **Hierarchy Structure**: Maintain clean hierarchy structure
- **Asset Organization**: Organize assets efficiently

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

### Security Considerations
- **Input Validation**: Strict input parameter validation
- **Permission Checks**: Complete permission checks
- **Logging**: Detailed operation logging
- **Audit Trail**: Complete audit trail

---

*Unity Skills Scene Operations Reference*
*Version: 1.6.1*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
