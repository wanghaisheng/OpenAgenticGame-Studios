# Event System

Handling input, node events, and custom events in Cocos Creator 3.x.

## Input Events

### Touch Events

```typescript
import { input, Input, EventTouch } from 'cc';

@ccclass('TouchHandler')
export class TouchHandler extends Component {
    onEnable() {
        // Register touch events
        input.on(Input.EventType.TOUCH_START, this.onTouchStart, this);
        input.on(Input.EventType.TOUCH_MOVE, this.onTouchMove, this);
        input.on(Input.EventType.TOUCH_END, this.onTouchEnd, this);
        input.on(Input.EventType.TOUCH_CANCEL, this.onTouchCancel, this);
    }

    onTouchStart(event: EventTouch) {
        const touchPos = event.getUILocation();
        console.log('Touch start:', touchPos.x, touchPos.y);
    }

    onTouchMove(event: EventTouch) {
        const touchPos = event.getUILocation();
        const delta = event.getDelta();
        console.log('Touch move:', touchPos.x, touchPos.y);
        console.log('Delta:', delta.x, delta.y);
    }

    onTouchEnd(event: EventTouch) {
        const touchPos = event.getUILocation();
        console.log('Touch end:', touchPos.x, touchPos.y);
    }

    onTouchCancel(event: EventTouch) {
        console.log('Touch canceled');
    }

    onDisable() {
        // Unregister events
        input.off(Input.EventType.TOUCH_START, this.onTouchStart, this);
        input.off(Input.EventType.TOUCH_MOVE, this.onTouchMove, this);
        input.off(Input.EventType.TOUCH_END, this.onTouchEnd, this);
        input.off(Input.EventType.TOUCH_CANCEL, this.onTouchCancel, this);
    }
}
```

### Mouse Events

```typescript
import { input, Input, EventMouse } from 'cc';

@ccclass('MouseHandler')
export class MouseHandler extends Component {
    onEnable() {
        input.on(Input.EventType.MOUSE_DOWN, this.onMouseDown, this);
        input.on(Input.EventType.MOUSE_MOVE, this.onMouseMove, this);
        input.on(Input.EventType.MOUSE_UP, this.onMouseUp, this);
        input.on(Input.EventType.MOUSE_WHEEL, this.onMouseWheel, this);
    }

    onMouseDown(event: EventMouse) {
        const pos = event.getUILocation();
        const button = event.getButton();

        console.log('Mouse down:', button, 'at', pos.x, pos.y);

        // Button: 0 = left, 1 = middle, 2 = right
        if (button === EventMouse.BUTTON_LEFT) {
            console.log('Left click');
        }
    }

    onMouseMove(event: EventMouse) {
        const pos = event.getUILocation();
        const delta = event.getDelta();
        console.log('Mouse move:', pos.x, pos.y, 'delta:', delta.x, delta.y);
    }

    onMouseUp(event: EventMouse) {
        console.log('Mouse up');
    }

    onMouseWheel(event: EventMouse) {
        const scrollY = event.getScrollY();
        console.log('Scroll:', scrollY);
    }

    onDisable() {
        input.off(Input.EventType.MOUSE_DOWN, this.onMouseDown, this);
        input.off(Input.EventType.MOUSE_MOVE, this.onMouseMove, this);
        input.off(Input.EventType.MOUSE_UP, this.onMouseUp, this);
        input.off(Input.EventType.MOUSE_WHEEL, this.onMouseWheel, this);
    }
}
```

### Keyboard Events

```typescript
import { input, Input, EventKeyboard, KeyCode } from 'cc';

@ccclass('KeyboardHandler')
export class KeyboardHandler extends Component {
    onEnable() {
        input.on(Input.EventType.KEY_DOWN, this.onKeyDown, this);
        input.on(Input.EventType.KEY_UP, this.onKeyUp, this);
    }

    onKeyDown(event: EventKeyboard) {
        const keyCode = event.keyCode;
        console.log('Key pressed:', keyCode);

        switch (keyCode) {
            case KeyCode.KEY_W:
                console.log('Move forward');
                break;
            case KeyCode.KEY_SPACE:
                console.log('Jump');
                break;
            case KeyCode.KEY_ESCAPE:
                console.log('Pause game');
                break;
        }
    }

    onKeyUp(event: EventKeyboard) {
        console.log('Key released:', event.keyCode);
    }

    onDisable() {
        input.off(Input.EventType.KEY_DOWN, this.onKeyDown, this);
        input.off(Input.EventType.KEY_UP, this.onKeyUp, this);
    }
}
```

### Joystick/Gamepad Events

```typescript
import { input, Input, EventGamepad } from 'cc';

@ccclass('GamepadHandler')
export class GamepadHandler extends Component {
    onEnable() {
        input.on(Input.EventType.GAMEPAD_CHANGE, this.onGamepadChange, this);
    }

    onGamepadChange(event: EventGamepad) {
        const gamepad = event.gamepad;
        console.log('Gamepad:', gamepad.mapping);

        // Button press
        for (let i = 0; i < gamepad.buttons.length; i++) {
            if (gamepad.buttons[i].pressed) {
                console.log('Button pressed:', i);
            }
        }

        // Axis values
        const leftStick = gamepad.axes[0];
        console.log('Left stick:', leftStick.x, leftStick.y);
    }

    onDisable() {
        input.off(Input.EventType.GAMEPAD_CHANGE, this.onGamepadChange, this);
    }
}
```

## Node Events

### Node Lifecycle Events

```typescript
import { Node, NodeEventType } from 'cc';

@ccclass('NodeEventHandler')
export class NodeEventHandler extends Component {
    onLoad() {
        // Node events
        this.node.on(NodeEventType.SIZE_CHANGED, this.onSizeChanged, this);
        this.node.on(NodeEventType.ANCHOR_CHANGED, this.onAnchorChanged, this);
        this.node.on(NodeEventType.CHILD_ADDED, this.onChildAdded, this);
        this.node.on(NodeEventType.CHILD_REMOVED, this.onChildRemoved, this);
        this.node.on(NodeEventType.SIBLING_ORDER_CHANGED, this.onSiblingOrderChanged, this);
    }

    onSizeChanged() {
        console.log('Node size changed');
    }

    onAnchorChanged() {
        console.log('Anchor changed');
    }

    onChildAdded(child: Node) {
        console.log('Child added:', child.name);
    }

    onChildRemoved(child: Node) {
        console.log('Child removed:', child.name);
    }

    onSiblingOrderChanged() {
        console.log('Sibling order changed');
    }

    onDestroy() {
        this.node.off(NodeEventType.SIZE_CHANGED, this.onSizeChanged, this);
        this.node.off(NodeEventType.ANCHOR_CHANGED, this.onAnchorChanged, this);
        this.node.off(NodeEventType.CHILD_ADDED, this.onChildAdded, this);
        this.node.off(NodeEventType.CHILD_REMOVED, this.onChildRemoved, this);
        this.node.off(NodeEventType.SIBLING_ORDER_CHANGED, this.onSiblingOrderChanged, this);
    }
}
```

### Touch Events on Nodes

```typescript
import { Node, EventTouch } from 'cc';

@ccclass('NodeTouchHandler')
export class NodeTouchHandler extends Component {
    onLoad() {
        // Node-specific touch events
        this.node.on(NodeEventType.TOUCH_START, this.onTouchStart, this);
        this.node.on(NodeEventType.TOUCH_MOVE, this.onTouchMove, this);
        this.node.on(NodeEventType.TOUCH_END, this.onTouchEnd, this);
        this.node.on(NodeEventType.TOUCH_CANCEL, this.onTouchCancel, this);
    }

    onTouchStart(event: EventTouch) {
        // Get local position
        const localPos = event.getLocalLocation();
        console.log('Local touch:', localPos.x, localPos.y);

        // Prevent event bubbling
        event.propagationStopped = true;
    }

    onTouchMove(event: EventTouch) {
        const localPos = event.getLocalLocation();
        console.log('Touch move:', localPos.x, localPos.y);
    }

    onTouchEnd(event: EventTouch) {
        console.log('Touch end');
    }

    onTouchCancel(event: EventTouch) {
        console.log('Touch canceled');
    }

    onDestroy() {
        this.node.off(NodeEventType.TOUCH_START, this.onTouchStart, this);
        this.node.off(NodeEventType.TOUCH_MOVE, this.onTouchMove, this);
        this.node.off(NodeEventType.TOUCH_END, this.onTouchEnd, this);
        this.node.off(NodeEventType.TOUCH_CANCEL, this.onTouchCancel, this);
    }
}
```

### Mouse Events on Nodes

```typescript
import { Node, EventMouse } from 'cc';

@ccclass('NodeMouseHandler')
export class NodeMouseHandler extends Component {
    onLoad() {
        this.node.on(NodeEventType.MOUSE_DOWN, this.onMouseDown, this);
        this.node.on(NodeEventType.MOUSE_ENTER, this.onMouseEnter, this);
        this.node.on(NodeEventType.MOUSE_LEAVE, this.onMouseLeave, this);
        this.node.on(NodeEventType.MOUSE_UP, this.onMouseUp, this);
        this.node.on(NodeEventType.MOUSE_WHEEL, this.onMouseWheel, this);
    }

    onMouseDown(event: EventMouse) {
        console.log('Mouse down on node');
        event.propagationStopped = true;  // Stop bubbling
    }

    onMouseEnter(event: EventMouse) {
        console.log('Mouse entered node');
    }

    onMouseLeave(event: EventMouse) {
        console.log('Mouse left node');
    }

    onMouseUp(event: EventMouse) {
        console.log('Mouse up on node');
    }

    onMouseWheel(event: EventMouse) {
        console.log('Mouse wheel on node');
    }

    onDestroy() {
        this.node.off(NodeEventType.MOUSE_DOWN, this.onMouseDown, this);
        this.node.off(NodeEventType.MOUSE_ENTER, this.onMouseEnter, this);
        this.node.off(NodeEventType.MOUSE_LEAVE, this.onMouseLeave, this);
        this.node.off(NodeEventType.MOUSE_UP, this.onMouseUp, this);
        this.node.off(NodeEventType.MOUSE_WHEEL, this.onMouseWheel, this);
    }
}
```

## Custom Events

### Emitting Custom Events

```typescript
@ccclass('EventEmitter')
export class EventEmitter extends Component {
    triggerExplosion(data: { damage: number, position: Vec3 }) {
        // Emit custom event
        this.node.emit('explosion', data);
    }

    start() {
        // Emit with data
        this.node.emit('player-jumped', { height: 5 });
        this.node.emit('health-changed', { current: 80, max: 100 });
    }
}
```

### Listening to Custom Events

```typescript
@ccclass('EventListener')
export class EventListener extends Component {
    onLoad() {
        // Listen to custom events
        this.node.on('explosion', this.onExplosion, this);
        this.node.on('player-jumped', this.onPlayerJumped, this);
        this.node.on('health-changed', this.onHealthChanged, this);
    }

    onExplosion(data: { damage: number, position: Vec3 }) {
        console.log('Explosion at', data.position, 'damage:', data.damage);
        this.applyDamage(data.damage);
    }

    onPlayerJumped(data: { height: number }) {
        console.log('Player jumped height:', data.height);
    }

    onHealthChanged(data: { current: number, max: number }) {
        const percentage = (data.current / data.max) * 100;
        console.log('Health:', percentage + '%');
    }

    onDestroy() {
        this.node.off('explosion', this.onExplosion, this);
        this.node.off('player-jumped', this.onPlayerJumped, this);
        this.node.off('health-changed', this.onHealthChanged, this);
    }
}
```

### Cross-Node Communication

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

    // Register event
    on(eventName: string, callback: Function, target: any) {
        this.node.on(eventName, callback, target);
    }

    // Unregister event
    off(eventName: string, callback: Function, target: any) {
        this.node.off(eventName, callback, target);
    }

    // Emit event
    emit(eventName: string, data: any) {
        this.node.emit(eventName, data);
    }
}

// Usage
@ccclass('Player')
export class Player extends Component {
    takeDamage(amount: number) {
        this.health -= amount;
        EventManager.getInstance.emit('health-changed', {
            current: this.health,
            max: this.maxHealth
        });
    }
}

@ccclass('HealthUI')
export class HealthUI extends Component {
    onLoad() {
        EventManager.getInstance.on('health-changed', this.updateHealthBar, this);
    }

    updateHealthBar(data: { current: number, max: number }) {
        this.healthBar.progress = data.current / data.max;
    }

    onDestroy() {
        EventManager.getInstance.off('health-changed', this.updateHealthBar, this);
    }
}
```

## Event Bubbling

### Understanding Bubbling

Events bubble up the node hierarchy:
```
Child Node (emits event)
    ↓
Parent Node (receives event)
    ↓
Grandparent Node (receives event)
```

### Stopping Propagation

```typescript
@ccclass('ButtonHandler')
export class ButtonHandler extends Component {
    onTouchStart(event: EventTouch) {
        console.log('Button clicked');

        // Stop event from bubbling to parent
        event.propagationStopped = true;
    }
}
```

### Target vs Current Target

```typescript
@cclass('EventInfo')
export class EventInfo extends Component {
    onTouchStart(event: EventTouch) {
        // The node that emitted the event
        console.log('Target:', event.target.name);

        // The node that's currently handling the event
        console.log('Current target:', event.currentTarget.name);
    }
}
```

## Button Component

### Using Button Component

```typescript
import { Button } from 'cc';

@ccclass('UIButton')
export class UIButton extends Component {
    onLoad() {
        const button = this.node.getComponent(Button);

        // Register click handler
        button.node.on(Button.EventType.CLICK, this.onClick, this);
    }

    onClick() {
        console.log('Button clicked!');
    }

    onDestroy() {
        const button = this.node.getComponent(Button);
        button.node.off(Button.EventType.CLICK, this.onClick, this);
    }
}
```

### Button with Transition

```typescript
@ccclass('AnimatedButton')
export class AnimatedButton extends Component {
    @property(Button)
    button: Button = null;

    onLoad() {
        // Configure button transition
        this.button.transition = Button.Transition.SCALE;
        this.button.zoomScale = 1.1;

        this.button.node.on(Button.EventType.CLICK, this.onClick, this);
    }

    onClick() {
        console.log('Button clicked with animation!');
    }
}
```

## Best Practices

1. **Always unsubscribe** events in `onDisable()` or `onDestroy()`
2. **Use event manager** for cross-node communication
3. **Stop propagation** when event shouldn't bubble
4. **Check event target** to avoid unintended triggers
5. **Use custom events** for component communication
6. **Debounce rapid events** (scroll, resize, etc.)
7. **Pool event handlers** for frequently created/destroyed nodes

## Common Patterns

### Input Action Map

```typescript
@ccclass('InputManager')
export class InputManager extends Component {
    private moveDirection: Vec3 = new Vec3();
    private isJumping: boolean = false;

    onEnable() {
        input.on(Input.EventType.KEY_DOWN, this.onKeyDown, this);
        input.on(Input.EventType.KEY_UP, this.onKeyUp, this);
    }

    onKeyDown(event: EventKeyboard) {
        switch (event.keyCode) {
            case KeyCode.KEY_W:
            case KeyCode.KEY_UP:
                this.moveDirection.z = -1;
                break;
            case KeyCode.KEY_S:
            case KeyCode.KEY_DOWN:
                this.moveDirection.z = 1;
                break;
            case KeyCode.KEY_A:
            case KeyCode.KEY_LEFT:
                this.moveDirection.x = -1;
                break;
            case KeyCode.KEY_D:
            case KeyCode.KEY_RIGHT:
                this.moveDirection.x = 1;
                break;
            case KeyCode.KEY_SPACE:
                this.isJumping = true;
                break;
        }
    }

    onKeyUp(event: EventKeyboard) {
        switch (event.keyCode) {
            case KeyCode.KEY_W:
            case KeyCode.KEY_UP:
            case KeyCode.KEY_S:
            case KeyCode.KEY_DOWN:
                this.moveDirection.z = 0;
                break;
            case KeyCode.KEY_A:
            case KeyCode.KEY_LEFT:
            case KeyCode.KEY_D:
            case KeyCode.KEY_RIGHT:
                this.moveDirection.x = 0;
                break;
            case KeyCode.KEY_SPACE:
                this.isJumping = false;
                break;
        }
    }

    update(deltaTime: number) {
        // Apply movement
        this.node.setPosition(
            this.node.position.x + this.moveDirection.x * this.speed * deltaTime,
            this.node.position.y,
            this.node.position.z + this.moveDirection.z * this.speed * deltaTime
        );
    }

    onDisable() {
        input.off(Input.EventType.KEY_DOWN, this.onKeyDown, this);
        input.off(Input.EventType.KEY_UP, this.onKeyUp, this);
    }
}
```

### Double Tap Detection

```typescript
@ccclass('DoubleTapDetector')
export class DoubleTapDetector extends Component {
    private lastTapTime: number = 0;
    private doubleTapDelay: number = 300;  // ms

    onTouchStart(event: EventTouch) {
        const now = Date.now();

        if (now - this.lastTapTime < this.doubleTapDelay) {
            // Double tap detected
            this.onDoubleTap(event);
            this.lastTapTime = 0;
        } else {
            // Single tap
            this.lastTapTime = now;
        }
    }

    onDoubleTap(event: EventTouch) {
        console.log('Double tap detected!');
    }
}
```

### Swipe Detection

```typescript
@ccclass('SwipeDetector')
export class SwipeDetector extends Component {
    private startPos: Vec3 = new Vec3();
    private swipeThreshold: number = 50;  // pixels

    onTouchStart(event: EventTouch) {
        const pos = event.getUILocation();
        this.startPos.set(pos.x, pos.y, 0);
    }

    onTouchEnd(event: EventTouch) {
        const pos = event.getUILocation();
        const deltaX = pos.x - this.startPos.x;
        const deltaY = pos.y - this.startPos.y;

        if (Math.abs(deltaX) > this.swipeThreshold ||
            Math.abs(deltaY) > this.swipeThreshold) {

            // Detect direction
            if (Math.abs(deltaX) > Math.abs(deltaY)) {
                // Horizontal
                if (deltaX > 0) {
                    this.onSwipeRight();
                } else {
                    this.onSwipeLeft();
                }
            } else {
                // Vertical
                if (deltaY > 0) {
                    this.onSwipeUp();
                } else {
                    this.onSwipeDown();
                }
            }
        }
    }

    onSwipeLeft() {
        console.log('Swipe left');
    }

    onSwipeRight() {
        console.log('Swipe right');
    }

    onSwipeUp() {
        console.log('Swipe up');
    }

    onSwipeDown() {
        console.log('Swipe down');
    }
}
```

## Troubleshooting

### Events Not Firing

```typescript
// Check if node is active
if (!this.node.activeInHierarchy) {
    console.log('Node inactive, events won\'t fire');
}

// Check if event is registered
console.log('Event listeners:', this.node.eventListeners.size);
```

### Memory Leaks from Events

```typescript
// PROBLEM: Forgetting to unsubscribe
this.node.on('click', this.onClick, this);

// SOLUTION: Always unsubscribe
onDestroy() {
    this.node.off('click', this.onClick, this);
}
```

### Event Fires Multiple Times

```typescript
// PROBLEM: Registering multiple times
onEnable() {
    this.node.on('click', this.onClick, this);
    // If called multiple times, event fires multiple times
}

// SOLUTION: Check if already registered
onEnable() {
    this.node.off('click', this.onClick, this);
    this.node.on('click', this.onClick, this);
}
```
