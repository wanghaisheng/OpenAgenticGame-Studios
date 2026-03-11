# Scene Management

Loading, switching, and managing scenes in Cocos Creator 3.x.

## Scene Basics

### What is a Scene?

A scene is a container for all game objects (nodes) in a particular game state. Examples:
- `MainMenu` - Title screen with menu options
- `GamePlay` - Main game scene
- `Settings` - Options interface
- `GameOver` - End game screen

**Key principle**: Only ONE scene can be active at a time.

## Loading Scenes

### Direct Scene Loading

```typescript
import { director } from 'cc';

// Load scene by name
director.loadScene('GamePlay');

// Load with callback (for error handling)
director.loadScene('GamePlay', (err) => {
    if (err) {
        console.error('Failed to load scene:', err);
        return;
    }
    console.log('Scene loaded successfully');
});
```

### Preloading Scenes

```typescript
// Preload scene in background
director.preloadScene('GamePlay', (completed, total, item) => {
    const progress = (completed / total) * 100;
    console.log(`Loading: ${progress.toFixed(2)}%`);
}, (err) => {
    if (err) {
        console.error('Preload failed:', err);
        return;
    }
    console.log('Scene preloaded');

    // Now can load instantly
    director.loadScene('GamePlay');
});
```

### Show Loading Screen

```typescript
@ccclass('SceneTransition')
export class SceneTransition extends Component {
    @property(Node)
    loadingScreen: Node = null;

    transitionToScene(sceneName: string) {
        // Show loading screen
        this.loadingScreen.active = true;

        // Preload scene
        director.preloadScene(sceneName, (completed, total, item) => {
            // Update progress bar
            const progress = completed / total;
            this.updateProgressBar(progress);
        }, (err) => {
            if (err) {
                console.error('Failed to preload:', err);
                this.loadingScreen.active = false;
                return;
            }

            // Scene preloaded, now load
            director.loadScene(sceneName);
        });
    }

    updateProgressBar(progress: number) {
        // Update UI progress bar
    }
}
```

## Scene Lifecycle

### Scene Loading Callbacks

```typescript
@ccclass('SceneLifecycle')
export class SceneLifecycle extends Component {
    onLoad() {
        // Subscribe to scene events
        director.on(Director.EVENT_BEFORE_SCENE_LAUNCH, this.onBeforeSceneLaunch, this);
        director.on(Director.EVENT_AFTER_SCENE_LAUNCH, this.onAfterSceneLaunch, this);
    }

    onBeforeSceneLaunch(sceneName: string) {
        console.log('About to launch:', sceneName);
        // Prepare for scene change
    }

    onAfterSceneLaunch(scene: Scene) {
        console.log('Scene launched:', scene.name);
        // Scene fully loaded and initialized
    }

    onDestroy() {
        director.off(Director.EVENT_BEFORE_SCENE_LAUNCH, this.onBeforeSceneLaunch, this);
        director.off(Director.EVENT_AFTER_SCENE_LAUNCH, this.onAfterSceneLaunch, this);
    }
}
```

### Scene Unloading

When a scene is unloaded:
1. `onDisable()` called on all components
2. `onDestroy()` called on all components
3. All nodes and components destroyed
4. Scene removed from memory

**Important**: Any data not persisted will be lost.

## Persist Nodes

### What are Persist Nodes?

Persist nodes are nodes that **survive scene changes**. They're useful for:
- GameManager (global game state)
- AudioManager (music/sound)
- NetworkManager (online connections)
- Data that needs to persist across scenes

### Creating Persist Nodes

```typescript
@ccclass('GameManager')
export class GameManager extends Component {
    private static instance: GameManager = null;

    static get getInstance(): GameManager {
        return GameManager.instance;
    }

    onLoad() {
        // Singleton pattern
        if (GameManager.instance) {
            // Already exists, destroy this duplicate
            this.node.destroy();
            return;
        }

        GameManager.instance = this;

        // Make persist across scenes
        game.addPersistRoot(this.node);
    }

    onDestroy() {
        if (GameManager.instance === this) {
            GameManager.instance = null;
            game.removePersistRoot(this.node);
        }
    }
}
```

### Accessing Persist Nodes

```typescript
@ccclass('GameScene')
export class GameScene extends Component {
    start() {
        // Access persist node
        const gameManager = GameManager.getInstance;
        gameManager.startGame();
    }
}
```

### Removing Persist Nodes

```typescript
// Remove persist status
game.removePersistRoot(this.node);

// Now node will be destroyed when scene changes
this.node.destroy();
```

## Data Transfer Between Scenes

### Method 1: Persist Node with Data

```typescript
@ccclass('SceneData')
export class SceneData extends Component {
    private static instance: SceneData = null;

    // Data to transfer
    playerScore: number = 0;
    playerName: string = '';

    onLoad() {
        if (SceneData.instance) {
            this.node.destroy();
            return;
        }
        SceneData.instance = this;
        game.addPersistRoot(this.node);
    }

    static get getInstance(): SceneData {
        return SceneData.instance;
    }

    // Clear data when needed
    clear() {
        this.playerScore = 0;
        this.playerName = '';
    }
}

// In MainMenu scene
const data = SceneData.getInstance;
data.playerName = 'Player1';
director.loadScene('GamePlay');

// In GamePlay scene
const data = SceneData.getInstance;
console.log('Welcome', data.playerName);
```

### Method 2: Global Variables

```typescript
// globals.ts
export const GameGlobals = {
    playerLevel: 1,
    unlockedItems: [],
    settings: {
        musicVolume: 0.8,
        sfxVolume: 1.0
    }
};

// In any scene
import { GameGlobals } from './globals';

GameGlobals.playerLevel = 5;
director.loadScene('NextScene');

console.log(GameGlobals.playerLevel);  // 5
```

### Method 3: Event System

```typescript
// Persist node with event bus
@ccclass('EventBus')
export class EventBus extends Component {
    private static instance: EventBus = null;

    onLoad() {
        if (EventBus.instance) {
            this.node.destroy();
            return;
        }
        EventBus.instance = this;
        game.addPersistRoot(this.node);
    }

    static get getInstance(): EventBus {
        return EventBus.instance;
    }

    private events: Map<string, any[]> = new Map();

    emit(eventName: string, data: any) {
        const callbacks = this.events.get(eventName);
        if (callbacks) {
            callbacks.forEach(cb => cb(data));
        }
    }

    on(eventName: string, callback: (data: any) => void) {
        if (!this.events.has(eventName)) {
            this.events.set(eventName, []);
        }
        this.events.get(eventName).push(callback);
    }
}

// Usage
const eventBus = EventBus.getInstance;
eventBus.emit('level-complete', { score: 100 });
```

## Scene Configuration

### Build Settings

Scenes must be added to build settings in **Project Settings**:

1. Open **Project Settings** → **Build**
2. Add scenes to build list
3. Set first scene as "Start Scene"

### Scene Properties

```typescript
// Get current scene
const currentScene = director.getScene();
console.log('Current scene:', currentScene.name);

// Get scene by name (if loaded)
const scene = director.getSceneByName('GamePlay');
```

### Auto-Release Resources

Configure scenes to auto-release resources:

```typescript
// In scene's root component
@ccclass('SceneRoot')
export class SceneRoot extends Component {
    onLoad() {
        // Configure auto-release
        assetManager.dependUtil.init(this.node);
    }

    onDestroy() {
        // Release scene resources
        assetManager.dependUtil.destroy(this.node);
    }
}
```

## Common Patterns

### Scene Manager

```typescript
@ccclass('SceneManager')
export class SceneManager extends Component {
    private static instance: SceneManager = null;

    onLoad() {
        if (SceneManager.instance) {
            this.node.destroy();
            return;
        }
        SceneManager.instance = this;
        game.addPersistRoot(this.node);
    }

    static get getInstance(): SceneManager {
        return SceneManager.instance;
    }

    // Navigate to scene with loading screen
    navigateToScene(sceneName: string) {
        // Show loading UI
        this.showLoadingScreen();

        // Preload then load
        director.preloadScene(sceneName, null, (err) => {
            if (err) {
                console.error('Failed to load scene:', err);
                this.hideLoadingScreen();
                return;
            }

            // Load scene
            director.loadScene(sceneName);
        });
    }

    showLoadingScreen() {
        // Show loading UI
    }

    hideLoadingScreen() {
        // Hide loading UI
    }
}

// Usage
SceneManager.getInstance.navigateToScene('GamePlay');
```

### Scene State Management

```typescript
@ccclass('SceneState')
export class SceneState extends Component {
    private state: Map<string, any> = new Map();

    setState(key: string, value: any) {
        this.state.set(key, value);
    }

    getState(key: string): any {
        return this.state.get(key);
    }

    clearState() {
        this.state.clear();
    }
}
```

### Scene Transitions

```typescript
@ccclass('SceneTransitionEffect')
export class SceneTransitionEffect extends Component {
    @property(Sprite)
    fadeSprite: Sprite = null;

    transitionToScene(sceneName: string) {
        // Fade out
        tween(this.fadeSprite)
            .to(0.5, { color: new Color(0, 0, 0, 255) })
            .call(() => {
                // Load scene after fade
                director.loadScene(sceneName);
            })
            .start();
    }
}
```

## Best Practices

1. **Preload large scenes** to avoid long loading times
2. **Use persist nodes** for data that needs to survive scene changes
3. **Release resources** when switching scenes to prevent memory leaks
4. **Show loading screen** for better UX
5. **Validate scene names** before loading to prevent crashes
6. **Clean up** in `onDestroy()` when leaving a scene
7. **Use singleton managers** for global state
8. **Organize scenes** by game state (menu, game, pause, etc.)

## Troubleshooting

### Scene Not Found

```typescript
// Check if scene exists in build settings
const scenes = builder.getSettings().getSceneSettings();
const sceneExists = scenes.some(s => s.sceneName === 'MyScene');

if (sceneExists) {
    director.loadScene('MyScene');
} else {
    console.error('Scene not in build settings');
}
```

### Data Lost After Scene Load

```typescript
// SOLUTION: Use persist node
game.addPersistRoot(dataManagerNode);
```

### Memory Increasing After Scene Loads

```typescript
// SOLUTION: Release resources
onDestroy() {
    assetManager.dependUtil.destroy(this.node);
    resources.release('textures/background');
}
```

### Scene Loading Too Slow

```typescript
// SOLUTION: Preload scene
director.preloadScene('NextScene', null, () => {
    // Now load is instant
    director.loadScene('NextScene');
});
```
