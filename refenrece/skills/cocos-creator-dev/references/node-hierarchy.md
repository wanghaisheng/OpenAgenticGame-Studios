# Node & Hierarchy Management

Working with nodes, scene hierarchy, and coordinate systems in Cocos Creator 3.x.

## Node Basics

### What is a Node?

Nodes (`Node`) are the building blocks of Cocos Creator scenes. They form a hierarchical tree structure where:
- Each node can have multiple children
- Each node has exactly one parent (except root)
- Components are attached to nodes to add functionality

### Node Properties

```typescript
const node = this.node;

// Active state
node.active = true;  // Enable/disable node

// Name
node.name = 'Player';  // Node name for finding

// Position (local)
node.setPosition(x, y, z);
node.setPosition(new Vec3(x, y, z));

// Rotation (local)
node.setRotationFromEuler(x, y, z);

// Scale (local)
node.setScale(x, y, z);

// Layer
node.layer = 1 << 0;  // Bitmask for layers
```

## Creating Nodes

### Creating Empty Node

```typescript
const newNode = new Node('NewNode');
this.node.addChild(newNode);
```

### Creating Node with Component

```typescript
// Method 1: Create and add component
const spriteNode = new Node('Sprite');
const sprite = spriteNode.addComponent(Sprite);
sprite.spriteFrame = spriteFrame;

// Method 2: Use prefab
const newNode = instantiate(this.prefab);
this.node.addChild(newNode);
```

### Creating from Prefab

```typescript
@ccclass('Spawner')
export class Spawner extends Component {
    @property(Prefab)
    enemyPrefab: Prefab = null;

    spawnEnemy() {
        const enemy = instantiate(this.enemyPrefab);
        enemy.setParent(this.node);
        enemy.setPosition(0, 0, 0);
    }
}
```

## Node Hierarchy

### Parent-Child Relationships

```typescript
// Add child
this.node.addChild(childNode);

// Set parent (removes from current parent)
childNode.setParent(newParent);

// Insert at specific index
this.node.insertChild(childNode, 0);  // Insert at beginning

// Remove from parent
childNode.removeFromParent();

// Remove all children
this.node.removeAllChildren();
```

### Accessing Hierarchy

```typescript
// Get parent
const parent = this.node.parent;

// Get children (array)
const children = this.node.children;

// Get child by name
const child = this.node.getChildByName('ChildName');

// Get child by path
const deepChild = this.node.getChildByPath('Parent/Child/Grandchild');

// Get sibling index
const index = this.node.getSiblingIndex();

// Set sibling order
this.node.setSiblingIndex(2);
```

### Searching Hierarchy

```typescript
// Find anywhere in scene
const player = find('Player');
const healthBar = find('Canvas/HealthBar');

// Search in children
const sprite = this.node.getComponentInChildren(Sprite);

// Search all descendants
const allSprites = this.node.getComponentsInChildren(Sprite);
```

## Node Transformations

### Position

```typescript
// Local position (relative to parent)
const localPos = this.node.position;
this.node.setPosition(x, y, z);

// World position
const worldPos = this.node.worldPosition;
this.node.setWorldPosition(x, y, z);

// Move relative
this.node.setPosition(
    this.node.position.x + deltaX,
    this.node.position.y + deltaY,
    this.node.position.z
);

// Shortcut methods
this.node.setPosition(x, y);
this.node.setPosition(x, y, z);
this.node.setPosition(vec3);
```

### Rotation

```typescript
// Euler angles (degrees)
this.node.setRotationFromEuler(x, y, z);

// Quaternion
const quat = new Quat();
this.node.setRotation(quat);

// Get rotation
const rotation = this.node.rotation;  // Quaternion
const euler = this.node.eulerAngles;  // Euler angles

// Rotate relative
this.node.rotate(new Vec3(0, 90, 0));  // Rotate 90° around Y
```

### Scale

```typescript
// Set scale
this.node.setScale(x, y, z);

// Uniform scale
this.node.setScale(2);  // Scale all by 2

// Get scale
const scale = this.node.scale;

// Scale relative
this.node.setScale(
    this.node.scale.x * 2,
    this.node.scale.y * 2,
    this.node.scale.z * 2
);
```

### Coordinate Conversion

```typescript
// Local to world
const worldPos = new Vec3();
this.node.getWorldPosition(worldPos);

// World to local
const localPos = new Vec3();
this.node.inverseTransformPoint(localPos, worldPos);

// Convert point to another node's space
const targetPos = new Vec3();
targetNode.inverseTransformPoint(targetPos, worldPos);
```

## Node Activation

### Active State

```typescript
// Get/set active
const isActive = this.node.active;
this.node.active = true;

// Set active recursively
this.node.active = true;  // Affects children

// Check if active in hierarchy
const activeInHierarchy = this.node.activeInHierarchy;
```

### Activation Events

```typescript
@ccclass('ActivationHandler')
export class ActivationHandler extends Component {
    onEnable() {
        console.log('Node activated');
        // Resume timers, restart animations
    }

    onDisable() {
        console.log('Node deactivated');
        // Pause timers, save state
    }
}
```

## Destroying Nodes

### Destroy vs Remove

```typescript
// Remove from hierarchy (node still exists)
this.node.removeFromParent();

// Destroy completely (will be freed at end of frame)
this.node.destroy();

// Destroy immediately
this.node.destroyAllChildren();
this.node.destroy();
```

### Safe Destruction Pattern

```typescript
@ccclass('Bullet')
export class Bullet extends Component {
    lifetime: number = 2;

    start() {
        this.scheduleOnce(() => {
            if (isValid(this.node)) {
                this.node.destroy();
            }
        }, this.lifetime);
    }

    onDestroy() {
        console.log('Bullet destroyed');
    }
}
```

### Checking Validity

```typescript
// Check if node/object is valid
if (isValid(this.node)) {
    // Safe to use
}

// Check if component exists
if (this.target && isValid(this.target)) {
    this.target.doSomething();
}
```

## Hierarchy Organization Best Practices

### Scene Structure

```
SceneRoot
├── Canvas (UI root)
│   ├── UI_MainMenu
│   ├── UI_HUD
│   └── UI_PauseMenu
├── GameManager
├── Player
├── Enemies
│   ├── Enemy_01
│   └── Enemy_02
├── Collectibles
└── Environment
    ├── Ground
    └── Obstacles
```

### Naming Conventions

- Use descriptive names: `Player`, `Enemy_01`, `HealthBar`
- Group with prefixes for organization: `UI_`, `FX_`, `Temp_`
- Use consistent numbering: `Waypoint_01`, `Waypoint_02`

### Logical Grouping

```typescript
// Create container node
const enemyContainer = new Node('Enemies');
this.node.addChild(enemyContainer);

// Spawn enemies in container
for (let i = 0; i < 10; i++) {
    const enemy = instantiate(this.enemyPrefab);
    enemy.setParent(enemyContainer);
}

// Move entire group
enemyContainer.setPosition(x, y, z);

// Destroy entire group
enemyContainer.destroy();
```

### Node Layers

```typescript
// Set layer for filtering
this.node.layer = LayerManager.Mask.UI;

// Check layer
if (node.layer === LayerManager.Mask.UI) {
    // Handle UI
}

// Common layers
enum Layers {
    UI = 1 << 0,
    Player = 1 << 1,
    Enemy = 1 << 2,
    Ground = 1 << 3,
}
```

## Performance Optimization

### Object Pooling

```typescript
@ccclass('BulletPool')
export class BulletPool extends Component {
    @property(Prefab)
    bulletPrefab: Prefab = null;

    private pool: Node[] = [];

    get(): Node {
        if (this.pool.length > 0) {
            const bullet = this.pool.pop();
            bullet.active = true;
            return bullet;
        }
        return instantiate(this.bulletPrefab);
    }

    put(bullet: Node) {
        bullet.active = false;
        bullet.removeFromParent();
        this.pool.push(bullet);
    }
}
```

### Minimize Hierarchy Depth

```
GOOD: Flat structure
Player
├── Sprite
├── Body
└── Weapon

AVOID: Deep nesting
Player
└── Container
    └── Container2
        └── Container3
            └── Sprite
```

### Batch Similar Objects

```typescript
// Group static objects
const staticContainer = new Node('StaticObjects');
this.node.addChild(staticContainer);

// Enable static batching
staticContainer.addComponentStatic(UIMeshRenderer);
```

## Common Patterns

### Scene Loading Hook

```typescript
@ccclass('SceneLoader')
export class SceneLoader extends Component {
    onLoad() {
        // Wait for scene to fully load
        director.once(Director.EVENT_AFTER_SCENE_LAUNCH, this.onSceneLoaded, this);
    }

    onSceneLoaded() {
        // Safe to access all nodes
        this.initializeGame();
    }
}
```

### Dynamic UI Creation

```typescript
@ccclass('InventoryUI')
export class InventoryUI extends Component {
    @property(Prefab)
    itemSlotPrefab: Prefab = null;

    @property(Node)
    container: Node = null;

    createSlots(count: number) {
        for (let i = 0; i < count; i++) {
            const slot = instantiate(this.itemSlotPrefab);
            slot.setParent(this.container);
            slot.setPosition(i * 100, 0, 0);
        }
    }
}
```

### Following Node

```typescript
@ccclass('FollowTarget')
export class FollowTarget extends Component {
    @property(Node)
    target: Node = null;

    @property
    smoothness: number = 5;

    lateUpdate() {
        if (!this.target) return;

        const targetPos = this.target.worldPosition.clone();
        const currentPos = this.node.worldPosition.clone();

        Vec3.lerp(currentPos, currentPos, targetPos, this.smoothness * deltaTime);
        this.node.setWorldPosition(currentPos);
    }
}
```

## Troubleshooting

### Node Not Found

```typescript
// WRONG - case sensitive
const node = find('player');

// CORRECT - exact case
const node = find('Player');
```

### Position Not Updating

```typescript
// Check if node is active
if (!this.node.activeInHierarchy) {
    console.log('Node is inactive');
}

// Check if parent is active
if (!this.node.parent.activeInHierarchy) {
    console.log('Parent is inactive');
}
```

### Transform Issues

```typescript
// Remember local vs world space
// Local is relative to parent
this.node.setPosition(x, y, z);

// World is absolute in scene
this.node.setWorldPosition(x, y, z);
```
