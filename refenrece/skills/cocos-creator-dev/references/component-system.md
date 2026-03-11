# Component System

Cocos Creator 3.x component architecture and lifecycle management.

## Component Lifecycle

### Lifecycle Flow

```
onLoad() → onEnable() → start() → update() → lateUpdate()
               ↓                    ↓
         onDisable()           onDestroy()
```

### Lifecycle Methods

#### onLoad()

**When called**: When component is loaded and attached to node

**Characteristics**:
- Called once when component is initialized
- All components on same node are loaded
- Other nodes may not be loaded yet

**Use for**:
- Initial data setup
- Subscribing to node events
- Initializing internal state

**Example**:
```typescript
onLoad() {
    this.currentHealth = this.maxHealth;
    this.node.on(NodeEventType.TOUCH_START, this.onTouch, this);
}
```

#### onEnable()

**When called**: When node/component becomes active

**Characteristics**:
- Called every time node is activated
- Called after `onLoad()` on first activation

**Use for**:
- Registering input events
- Starting timers/schedules
- Resuming paused behavior

**Example**:
```typescript
onEnable() {
    input.on(Input.EventType.TOUCH_START, this.onTouchStart, this);
    this.schedule(this.updateTimer, 1);
}
```

#### start()

**When called**: Before first frame update

**Characteristics**:
- Called only once
- All components in scene have `onLoad()` called
- Safe to access other components

**Use for**:
- Accessing other components/nodes
- Post-initialization setup
- Logic requiring other components to be ready

**Example**:
```typescript
start() {
    // Safe to access components on other nodes
    this.player = find('Player').getComponent(PlayerController);
}
```

#### update(deltaTime: number)

**When called**: Every frame

**Characteristics**:
- Called every frame
- Receives delta time since last frame

**Use for**:
- Movement
- Animation
- Continuous game logic

**Example**:
```typescript
update(deltaTime: number) {
    this.node.setPosition(
        this.node.position.x + this.speed * deltaTime,
        this.node.position.y
    );
}
```

#### lateUpdate(deltaTime: number)

**When called**: After all `update()` calls

**Characteristics**:
- Called after all components' `update()`
- Good for following other objects

**Use for**:
- Camera follow
- UI updates based on game state
- Calculations dependent on other updates

**Example**:
```typescript
lateUpdate(deltaTime: number) {
    // Camera follows player after player moves
    const targetPos = this.target.position;
    this.node.setPosition(targetPos.x, targetPos.y, this.node.position.z);
}
```

#### onDisable()

**When called**: When node/component becomes inactive

**Use for**:
- Unregistering input events
- Stopping timers/schedules
- Pausing behavior

**Example**:
```typescript
onDisable() {
    input.off(Input.EventType.TOUCH_START, this.onTouchStart, this);
    this.unschedule(this.updateTimer);
}
```

#### onDestroy()

**When called**: When component/node is destroyed

**Use for**:
- Releasing resources
- Removing event listeners
- Cleanup before deletion

**Example**:
```typescript
onDestroy() {
    this.node.off(NodeEventType.TOUCH_START, this.onTouch, this);
    assetManager.releaseAsset(this.texture);
}
```

## Component Management

### Adding Components

#### In Editor

1. Select node in **Hierarchy**
2. **Add Component** → **Custom Script** → Select component

#### Dynamically in Code

```typescript
// Add component to current node
const rigidBody = this.node.addComponent(RigidBody2D);

// Add to other node
const sprite = otherNode.addComponent(Sprite);

// Add custom component
const myComp = this.node.addComponent(MyComponent);
```

### Getting Components

```typescript
// Get component on same node
const sprite = this.node.getComponent(Sprite);

// Get component in children
const childSprite = this.getComponentInChildren(Sprite);

// Get all components in children
const allSprites = this.getComponentsInChildren(Sprite);

// Get component in parent
const parentSprite = this.node.parent.getComponent(Sprite);

// Get specific component type
const myComp = this.node.getComponent('MyComponent') as MyComponent;
```

### Removing Components

```typescript
// Remove component
const comp = this.node.getComponent(MyComponent);
comp.destroy();

// Remove all components of type
const comps = this.node.getComponents(MyComponent);
comps.forEach(c => c.destroy());
```

## Component Execution Order

### Default Order

- Not guaranteed across different components
- Same component types execute in order of creation

### Controlling Order

#### Method 1: executionOrder Property

```typescript
@ccclass('EarlyUpdater')
export class EarlyUpdater extends Component {
    // Lower values execute first
    executionOrder = -1;

    update() {
        // Runs before normal components
    }
}

@ccclass('LateUpdater')
export class LateUpdater extends Component {
    // Higher values execute later
    executionOrder = 1;

    update() {
        // Runs after normal components
    }
}
```

#### Method 2: Dependency-Based

Use `start()` for dependent logic:

```typescript
// Component A
@ccclass('DataProvider')
export class DataProvider extends Component {
    data: number = 0;

    update() {
        this.data = calculate();
    }
}

// Component B - depends on A
@ccclass('DataConsumer')
export class DataConsumer extends Component {
    @property(DataProvider)
    provider: DataProvider = null;

    update() {
        // Access data updated by A
        const value = this.provider.data;
    }
}
```

## Component Communication

### Direct Reference

```typescript
@ccclass('ComponentA')
export class ComponentA extends Component {
    @property(ComponentB)
    target: ComponentB = null;

    doSomething() {
        target.performAction();
    }
}
```

### Node Finding

```typescript
// Find node by name
const playerNode = find('Player');
const player = playerNode.getComponent(PlayerController);

// Find by path
const enemy = find('Enemies/Enemy_01');
```

### Event System

```typescript
// Emitter
@ccclass('HealthComponent')
export class HealthComponent extends Component {
    takeDamage(amount: number) {
        this.health -= amount;
        this.node.emit('health-changed', { current: this.health });
    }
}

// Listener
@ccclass('UIController')
export class UIController extends Component {
    onLoad() {
        this.healthNode.on('health-changed', this.updateHealthBar, this);
    }

    updateHealthBar(data: { current: number }) {
        this.healthBar.progress = data.current / 100;
    }

    onDestroy() {
        this.healthNode.off('health-changed', this.updateHealthBar, this);
    }
}
```

### Singleton Manager

```typescript
@ccclass('EventManager')
export class EventManager extends Component {
    private static instance: EventManager = null;

    static get getInstance(): EventManager {
        return EventManager.instance;
    }

    onLoad() {
        if (EventManager.instance) {
            this.node.destroy();
            return;
        }
        EventManager.instance = this;
        game.addPersistRoot(this.node);
    }

    events: Map<string, Function[]> = new Map();

    on(eventName: string, callback: Function) {
        if (!this.events.has(eventName)) {
            this.events.set(eventName, []);
        }
        this.events.get(eventName).push(callback);
    }

    emit(eventName: string, data: any) {
        const callbacks = this.events.get(eventName);
        if (callbacks) {
            callbacks.forEach(cb => cb(data));
        }
    }
}
```

## Component Scheduling

### Timers

```typescript
// Schedule once
this.scheduleOnce(() => {
    console.log('Delayed action');
}, 1); // 1 second delay

// Schedule repeat
this.schedule(this.updateTimer, 1); // Every 1 second

// Schedule with interval
this.schedule(this.task, 0.5, repeat=5, delay=2);

// Unschedule specific
this.unschedule(this.updateTimer);

// Unschedule all
this.unscheduleAllCallbacks();
```

### Frame Callbacks

```typescript
// Register for specific component
this.node.addComponent(Component).scheduleOnce(...);

// Use component's schedule system
director.getScheduler().schedule(
    callback,
    this.target,
    interval,
    repeat,
    delay,
    !paused
);
```

## Best Practices

1. **Use onLoad for initialization**, not constructor
2. **Use start for accessing other components**
3. **Always unsubscribe events** in `onDisable()` or `onDestroy()`
4. **Cache component references** to avoid repeated `getComponent()`
5. **Use executionOrder** when update order matters
6. **Prefer events** over tight coupling
7. **Release resources** in `onDestroy()`
8. **Check for null** on `@property` references before use

## Common Pitfalls

### Accessing Components Too Early

```typescript
// WRONG - in onLoad
onLoad() {
    const player = find('Player').getComponent(Player); // May not exist
}

// CORRECT - in start
start() {
    const player = find('Player').getComponent(Player); // Safe
}
```

### Memory Leaks from Events

```typescript
// WRONG - forgetting to unsubscribe
onLoad() {
    this.node.on('click', this.onClick, this);
}

// CORRECT - unsubscribe in onDestroy
onLoad() {
    this.node.on('click', this.onClick, this);
}

onDestroy() {
    this.node.off('click', this.onClick, this);
}
```

### Expensive Operations in Update

```typescript
// WRONG - getting component every frame
update() {
    const sprite = this.node.getComponent(Sprite);
    // Use sprite
}

// CORRECT - cache in onLoad
onLoad() {
    this.sprite = this.node.getComponent(Sprite);
}

update() {
    // Use this.sprite
}
```
