# Script Basics

Cocos Creator 3.x TypeScript scripting fundamentals.

## Language Requirements

**Cocos Creator 3.x ONLY supports TypeScript.** JavaScript is not supported.

### TypeScript Configuration

Configure `tsconfig.json` in project root:

```json
{
    "compilerOptions": {
        "target": "ES2020",
        "module": "ES2020",
        "experimentalDecorators": true,
        "strict": true
    }
}
```

## Creating Scripts

### Method 1: Editor UI

1. Open **Assets Manager**
2. Right-click in folder → **Create** → **TypeScript**
3. Name the file (e.g., `MyComponent.ts`)
4. Script automatically generates component template

### Method 2: Manual Creation

Create `.ts` file in `assets/` directory with proper naming.

## Component Class Definition

### Basic Structure

```typescript
import { _decorator, Component, Node } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('MyComponent')
export class MyComponent extends Component {
    // Component code here
}
```

### Decorators

#### @ccclass

Required decorator for component classes:

```typescript
@ccclass('PlayerController')
export class PlayerController extends Component {
    // Component name in editor will be "PlayerController"
}
```

#### @property

Expose properties to editor:

```typescript
@ccclass('Example')
export class Example extends Component {
    // Numeric property
    @property
    speed: number = 10;

    // With min/max limits
    @property({ min: 0, max: 100 })
    health: number = 100;

    // Node reference
    @property(Node)
    targetNode: Node = null;

    // Component reference
    @property(Sprite)
    sprite: Sprite = null;

    // Array
    @property([Node])
    waypoints: Node[] = [];

    // Read-only
    @property({ readonly: true })
    id: string = 'player_001';

    // Tooltip
    @property({
        tooltip: 'Movement speed in units per second'
    })
    moveSpeed: number = 5;

    // Display name
    @property({
        displayName: 'Max Health'
    })
    maximumHealth: number = 100;
}
```

#### @menu

Customize menu location:

```typescript
@ccclass('Player')
@menu('Game/Player')
export class Player extends Component {
    // Appears in "Add Component" under "Game" category
}
```

#### @executeInEditMode

Execute in editor mode:

```typescript
@ccclass('Visualizer')
@executeInEditMode
export class Visualizer extends Component {
    update() {
        // Runs in edit mode for real-time visualization
    }
}
```

## Property Types

### Primitive Types

```typescript
@property
    num: number = 0;

@property
    str: string = '';

@property
    flag: boolean = false;

// Enum
enum Direction { Up, Down, Left, Right }
@property({ type: Direction })
direction: Direction = Direction.Up;
```

### Engine Types

```typescript
import { Sprite, Label, UITransform, Vec3 } from 'cc';

@property(Sprite)
spriteComp: Sprite = null;

@property(Label)
labelComp: Label = null;

@property(Vec3)
position: Vec3 = new Vec3();
```

### Array Properties

```typescript
@property([Node])
nodes: Node[] = [];

@property([SpriteFrame])
frames: SpriteFrame[] = [];

@property([Color])
colors: Color[] = [];
```

## Component Inheritance

```typescript
@ccclass('BaseEnemy')
export class BaseEnemy extends Component {
    @property
    health: number = 100;

    takeDamage(amount: number) {
        this.health -= amount;
    }
}

@ccclass('BossEnemy')
export class BossEnemy extends BaseEnemy {
    @property
    phase: number = 1;

    takeDamage(amount: number) {
        super.takeDamage(amount);
        // Additional boss logic
    }
}
```

## Accessing Components

### Get Self Component

```typescript
// Within component
const transform = this.node.getComponent(UITransform);
```

### Get Other Components

```typescript
// On same node
const sprite = this.node.getComponent(Sprite);

// On parent node
const parentSprite = this.node.parent.getComponent(Sprite);

// In child nodes
const childSprite = this.getComponentInChildren(Sprite);

// All components in children
const allSprites = this.getComponentsInChildren(Sprite);
```

### Node References

```typescript
// Via @property
@property(Node)
target: Node = null;

// Find by path
const child = this.node.getChildByName('ChildName');

// Find by path string
const deepChild = this.node.getChildByPath('Parent/Child/Grandchild');
```

## Component Lifecycle

```typescript
@ccclass('LifecycleExample')
export class LifecycleExample extends Component {
    onLoad() {
        // Called when component is loaded
        // All other components on same node are loaded
        // Good for initialization
    }

    onEnable() {
        // Called when node is enabled
        // Subscribe to events here
    }

    start() {
        // Called before first update
        // All components are started
        // Good for accessing other components
    }

    update(deltaTime: number) {
        // Called every frame
    }

    lateUpdate(deltaTime: number) {
        // Called after all updates
        // Good for camera follow
    }

    onDisable() {
        // Called when node is disabled
        // Unsubscribe from events here
    }

    onDestroy() {
        // Called when component is destroyed
        // Release resources, cleanup
    }
}
```

## Best Practices

1. **Always use TypeScript types** for better IDE support
2. **Initialize properties** to avoid null reference errors
3. **Use @property** for values that should be configurable in editor
4. **Null check references** before using `@property` Node/Component references
5. **Release resources** in `onDestroy()` to prevent memory leaks
6. **Subscribe to events** in `onEnable()`, unsubscribe in `onDisable()`

## Common Patterns

### Singleton Pattern

```typescript
@ccclass('GameManager')
export class GameManager extends Component {
    private static instance: GameManager = null;

    static get getInstance(): GameManager {
        return GameManager.instance;
    }

    onLoad() {
        if (GameManager.instance === null) {
            GameManager.instance = this;
            game.addPersistRoot(this.node);
        } else {
            this.node.destroy();
        }
    }
}
```

### Object Pool Pattern

```typescript
@ccclass('BulletPool')
export class BulletPool extends Component {
    @property(Prefab)
    bulletPrefab: Prefab = null;

    private pool: Node[] = [];

    getBullet(): Node {
        if (this.pool.length > 0) {
            return this.pool.pop();
        }
        return instantiate(this.bulletPrefab);
    }

    returnBullet(bullet: Node) {
        bullet.active = false;
        this.pool.push(bullet);
    }
}
```

## TypeScript Tips

1. **Use ES modules**: `import { ... } from 'cc'`
2. **Enable strict mode** in tsconfig for type safety
3. **Use interface** for complex data structures
4. **Leverage generics** for reusable components
5. **Use async/await** for resource loading with promises
