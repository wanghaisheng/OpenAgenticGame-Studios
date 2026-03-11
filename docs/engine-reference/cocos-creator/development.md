# Cocos Creator Development Reference

## Overview

This document provides comprehensive development guidelines for Cocos Creator game development within Claude Code Game Studios.

## Development Environment Setup

### Prerequisites
- **Node.js** - Version 16.x or higher
- **Cocos Creator** - Version 3.8.x recommended
- **TypeScript** - Version 4.x for Cocos Creator 3.8.x
- **IDE** - VS Code with Cocos Creator extension recommended

### Project Structure
```
project/
├── assets/                    # Game assets
│   ├── scenes/               # Scene files
│   ├── scripts/               # TypeScript scripts
│   ├── resources/             # Resource files
│   └── prefabs/               # Prefab files
├── temp/                      # Temporary build files
├── build/                     # Build output
├── tsconfig.json              # TypeScript configuration
├── package.json               # Node.js dependencies
└── project.json               # Cocos Creator project config
```

## TypeScript Development

### TypeScript Configuration
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ES2020",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "baseUrl": "./",
    "paths": {
      "@/*": ["./assets/*"]
    }
  },
  "include": [
    "assets/**/*"
  ],
  "exclude": [
    "node_modules",
    "temp",
    "build"
  ]
}
```

### Component Development
```typescript
import { _decorator, Component, Node } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('PlayerController')
export class PlayerController extends Component {
    @property(Number)
    speed: number = 200;

    @property(Node)
    targetNode: Node | null = null;

    start() {
        // Initialize component
        this.initPlayer();
    }

    update(deltaTime: number) {
        // Update logic
        this.handleInput(deltaTime);
    }

    private initPlayer() {
        // Player initialization
        console.log('Player initialized');
    }

    private handleInput(deltaTime: number) {
        // Input handling
        const input = systemEvent(Event.EventType.KEYBOARD);
        // Handle keyboard input
    }
}
```

### Prefab Development
```typescript
import { _decorator, Component, Prefab, instantiate } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('PrefabManager')
export class PrefabManager extends Component {
    @property(Prefab)
    enemyPrefab: Prefab | null = null;

    spawnEnemy(position: Vec3) {
        if (this.enemyPrefab) {
            const enemy = instantiate(this.enemyPrefab);
            enemy.setPosition(position);
            this.node.addChild(enemy);
        }
    }
}
```

## Scene Management

### Scene Loading
```typescript
import { director, Scene } from 'cc';

export class SceneManager {
    static loadScene(sceneName: string): Promise<Scene> {
        return new Promise((resolve, reject) => {
            director.loadScene(sceneName, (err, scene) => {
                if (err) {
                    reject(err);
                } else {
                    resolve(scene);
                }
            });
        });
    }

    static async loadSceneWithTransition(sceneName: string) {
        // Add transition effect
        await this.showTransition();
        await this.loadScene(sceneName);
        await this.hideTransition();
    }

    private static showTransition(): Promise<void> {
        return new Promise(resolve => {
            // Show transition effect
            setTimeout(resolve, 500);
        });
    }

    private static hideTransition(): Promise<void> {
        return new Promise(resolve => {
            // Hide transition effect
            setTimeout(resolve, 500);
        });
    }
}
```

### Scene Data Management
```typescript
import { JsonAsset } from 'cc';

@ccclass('SceneDataManager')
export class SceneDataManager extends Component {
    @property(JsonAsset)
    sceneData: JsonAsset | null = null;

    getSceneData(key: string): any {
        if (this.sceneData) {
            const data = this.sceneData.json;
            return data[key] || null;
        }
        return null;
    }

    saveSceneData(key: string, data: any): void {
        // Save scene data (implementation depends on storage system)
        console.log(`Saving data for key: ${key}`);
    }
}
```

## Asset Management

### Resource Loading
```typescript
import { resources, SpriteFrame, AudioClip } from 'cc';

export class ResourceManager {
    static async loadSpriteFrame(path: string): Promise<SpriteFrame> {
        return new Promise((resolve, reject) => {
            resources.load(path, SpriteFrame, (err, spriteFrame) => {
                if (err) {
                    reject(err);
                } else {
                    resolve(spriteFrame);
                }
            });
        });
    }

    static async loadAudioClip(path: string): Promise<AudioClip> {
        return new Promise((resolve, reject) => {
            resources.load(path, AudioClip, (err, audioClip) => {
                if (err) {
                    reject(err);
                } else {
                    resolve(audioClip);
                }
            });
        });
    }

    static preloadResources(paths: string[]): Promise<void> {
        return new Promise((resolve, reject) => {
            resources.load(paths, (err, loadedAssets) => {
                if (err) {
                    reject(err);
                } else {
                    console.log('Resources preloaded:', loadedAssets);
                    resolve();
                }
            });
        });
    }
}
```

### Bundle Management
```typescript
import { bundleManager, Bundle } from 'cc';

export class BundleManager {
    private static bundles: Map<string, Bundle> = new Map();

    static async loadBundle(bundleName: string): Promise<Bundle> {
        return new Promise((resolve, reject) => {
            bundleManager.loadBundle(bundleName, (err, bundle) => {
                if (err) {
                    reject(err);
                } else {
                    this.bundles.set(bundleName, bundle);
                    resolve(bundle);
                }
            });
        });
    }

    static getBundle(bundleName: string): Bundle | null {
        return this.bundles.get(bundleName) || null;
    }

    static async loadAssetFromBundle<T>(
        bundleName: string, 
        path: string, 
        type: typeof T
    ): Promise<T> {
        const bundle = this.getBundle(bundleName);
        if (!bundle) {
            await this.loadBundle(bundleName);
        }
        
        return new Promise((resolve, reject) => {
            bundle.load(path, type, (err, asset) => {
                if (err) {
                    reject(err);
                } else {
                    resolve(asset);
                }
            });
        });
    }
}
```

## UI Development

### UI Component Development
```typescript
import { _decorator, Component, Node, Button, Label } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('UIMenu')
export class UIMenu extends Component {
    @property(Button)
    startButton: Button | null = null;

    @property(Button)
    settingsButton: Button | null = null;

    @property(Label)
    titleLabel: Label | null = null;

    onEnable() {
        this.setupUI();
    }

    private setupUI() {
        if (this.startButton) {
            this.startButton.node.on(Button.EventType.CLICK, this.onStartGame, this);
        }
        
        if (this.settingsButton) {
            this.settingsButton.node.on(Button.EventType.CLICK, this.onSettings, this);
        }
    }

    private onStartGame() {
        console.log('Start game clicked');
        // Start game logic
    }

    private onSettings() {
        console.log('Settings clicked');
        // Open settings logic
    }

    public setTitle(title: string) {
        if (this.titleLabel) {
            this.titleLabel.string = title;
        }
    }
}
```

### UI Animation
```typescript
import { tween, Vec3 } from 'cc';

@ccclass('UIAnimation')
export class UIAnimation extends Component {
    private buttonScale: Vec3 = new Vec3(1, 1, 1);

    playButtonAnimation(button: Node) {
        // Scale down
        tween(button)
            .to(0.1, { scale: new Vec3(0.9, 0.9, 1) })
            .call(() => {
                // Scale up
                tween(button)
                    .to(0.1, { scale: this.buttonScale })
                    .start();
            })
            .start();
    }

    playFadeInAnimation(node: Node, duration: number = 0.5) {
        node.opacity = 0;
        tween(node)
            .to(duration, { opacity: 1 })
            .start();
    }

    playFadeOutAnimation(node: Node, duration: number = 0.5) {
        tween(node)
            .to(duration, { opacity: 0 })
            .call(() => {
                node.active = false;
            })
            .start();
    }
}
```

## Audio System

### Audio Manager
```typescript
import { _decorator, Component, AudioSource, AudioClip } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('AudioManager')
export class AudioManager extends Component {
    @property(AudioClip)
    backgroundMusic: AudioClip | null = null;

    @property(AudioClip)
    clickSound: AudioClip | null = null;

    private audioSource: AudioSource | null = null;

    start() {
        this.audioSource = this.getComponent(AudioSource);
        this.playBackgroundMusic();
    }

    playBackgroundMusic() {
        if (this.audioSource && this.backgroundMusic) {
            this.audioSource.clip = this.backgroundMusic;
            this.audioSource.loop = true;
            this.audioSource.play();
        }
    }

    playClickSound() {
        if (this.audioSource && this.clickSound) {
            this.audioSource.playOneShot(this.clickSound);
        }
    }

    stopBackgroundMusic() {
        if (this.audioSource) {
            this.audioSource.stop();
        }
    }

    setVolume(volume: number) {
        if (this.audioSource) {
            this.audioSource.volume = volume;
        }
    }
}
```

## Physics System

### Physics Components
```typescript
import { _decorator, Component, RigidBody2D, Collider2D, Vec2 } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('PhysicsObject')
export class PhysicsObject extends Component {
    @property(Number)
    mass: number = 1;

    @property(Number)
    friction: number = 0.5;

    private rigidBody: RigidBody2D | null = null;

    start() {
        this.rigidBody = this.getComponent(RigidBody2D);
        this.setupPhysics();
    }

    private setupPhysics() {
        if (this.rigidBody) {
            this.rigidBody.mass = this.mass;
            this.rigidBody.linearDamping = this.friction;
        }
    }

    addForce(force: Vec2) {
        if (this.rigidBody) {
            this.rigidBody.applyForce(force);
        }
    }

    setVelocity(velocity: Vec2) {
        if (this.rigidBody) {
            this.rigidBody.linearVelocity = velocity;
        }
    }
}
```

## Input System

### Input Manager
```typescript
import { _decorator, Component, systemEvent, Event, Vec2 } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('InputManager')
export class InputManager extends Component {
    @property(Number)
    sensitivity: number = 1.0;

    private touchStartPos: Vec2 = new Vec2();
    private isTouching: boolean = false;

    onEnable() {
        this.registerInputEvents();
    }

    onDisable() {
        this.unregisterInputEvents();
    }

    private registerInputEvents() {
        systemEvent.on(Event.EventType.TOUCH_START, this.onTouchStart, this);
        systemEvent.on(Event.EventType.TOUCH_MOVE, this.onTouchMove, this);
        systemEvent.on(Event.EventType.TOUCH_END, this.onTouchEnd, this);
    }

    private unregisterInputEvents() {
        systemEvent.off(Event.EventType.TOUCH_START, this.onTouchStart, this);
        systemEvent.off(Event.EventType.TOUCH_MOVE, this.onTouchMove, this);
        systemEvent.off(Event.EventType.TOUCH_END, this.onTouchEnd, this);
    }

    private onTouchStart(event: Event.EventTouch) {
        this.isTouching = true;
        this.touchStartPos = event.getUILocation();
    }

    private onTouchMove(event: Event.EventTouch) {
        if (this.isTouching) {
            const currentPos = event.getUILocation();
            const delta = currentPos.subtract(this.touchStartPos);
            this.handleInput(delta);
        }
    }

    private onTouchEnd() {
        this.isTouching = false;
    }

    private handleInput(delta: Vec2) {
        // Handle input based on delta
        const scaledDelta = delta.multiplyScalar(this.sensitivity);
        // Apply input to game objects
    }
}
```

## Performance Optimization

### Object Pooling
```typescript
import { _decorator, Component, Node, instantiate, Prefab } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('ObjectPool')
export class ObjectPool extends Component {
    @property(Prefab)
    prefab: Prefab | null = null;

    @property(Number)
    initialSize: number = 10;

    private pool: Node[] = [];
    private activeObjects: Set<Node> = new Set();

    start() {
        this.initializePool();
    }

    private initializePool() {
        for (let i = 0; i < this.initialSize; i++) {
            if (this.prefab) {
                const obj = instantiate(this.prefab);
                obj.active = false;
                this.node.addChild(obj);
                this.pool.push(obj);
            }
        }
    }

    getObject(): Node | null {
        let obj: Node | null = null;
        
        if (this.pool.length > 0) {
            obj = this.pool.pop()!;
        } else if (this.prefab) {
            obj = instantiate(this.prefab);
            this.node.addChild(obj);
        }
        
        if (obj) {
            obj.active = true;
            this.activeObjects.add(obj);
        }
        
        return obj;
    }

    returnObject(obj: Node) {
        if (this.activeObjects.has(obj)) {
            obj.active = false;
            this.activeObjects.delete(obj);
            this.pool.push(obj);
        }
    }

    returnAllObjects() {
        const objects = Array.from(this.activeObjects);
        objects.forEach(obj => this.returnObject(obj));
    }
}
```

### Performance Monitoring
```typescript
import { _decorator, Component, director, game } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('PerformanceMonitor')
export class PerformanceMonitor extends Component {
    @property(Number)
    targetFPS: number = 60;

    private frameCount: number = 0;
    private lastTime: number = 0;
    private currentFPS: number = 0;

    start() {
        this.startMonitoring();
    }

    private startMonitoring() {
        director.on(director.Director.EVENT_AFTER_DRAW, this.updateFPS, this);
    }

    private updateFPS() {
        this.frameCount++;
        const currentTime = game.totalTime;
        
        if (currentTime - this.lastTime >= 1.0) {
            this.currentFPS = this.frameCount;
            this.frameCount = 0;
            this.lastTime = currentTime;
            
            this.checkPerformance();
        }
    }

    private checkPerformance() {
        if (this.currentFPS < this.targetFPS * 0.8) {
            console.warn(`Low FPS detected: ${this.currentFPS}`);
            this.optimizePerformance();
        }
    }

    private optimizePerformance() {
        // Implement performance optimization
        console.log('Optimizing performance...');
    }
}
```

## Build and Deployment

### Build Configuration
```json
{
  "version": "3.8.0",
  "platform": "web-mobile",
  "debug": false,
  "sourceMaps": false,
  "md5Cache": true,
  "compressTexture": true,
  "excludeModules": [],
  "orientation": {
    "landscapeLeft": true,
    "landscapeRight": true,
    "portrait": false
  }
}
```

### Platform-Specific Settings
```typescript
export class PlatformSettings {
    static getPlatformSettings(): any {
        const platform = sys.getPlatform();
        
        switch (platform) {
            case sys.Platform.IOS:
                return {
                    bundleName: "com.company.game",
                    bundleVersion: "1.0.0",
                    orientation: {
                        "landscapeLeft": true,
                        "landscapeRight": true
                    }
                };
                
            case sys.Platform.ANDROID:
                return {
                    packageName: "com.company.game",
                    versionCode: 1,
                    orientation: {
                        "landscape": true
                    }
                };
                
            case sys.Platform.MOBILE_BROWSER:
                return {
                    orientation: {
                        "landscape": true
                    }
                };
                
            default:
                return {};
        }
    }
}
```

## Testing

### Unit Testing
```typescript
import { _decorator, Component } from 'cc';
const { ccclass } = _decorator;

@ccclass('TestRunner')
export class TestRunner extends Component {
    start() {
        this.runTests();
    }

    private runTests() {
        this.testResourceManager();
        this.testSceneManager();
        this.testAudioManager();
        console.log('All tests completed');
    }

    private testResourceManager() {
        // Test resource loading
        console.log('Testing ResourceManager...');
        // Add resource loading tests
    }

    private testSceneManager() {
        // Test scene management
        console.log('Testing SceneManager...');
        // Add scene management tests
    }

    private testAudioManager() {
        // Test audio management
        console.log('Testing AudioManager...');
        // Add audio management tests
    }
}
```

## Best Practices

### Code Organization
- **Modular Design** - Separate concerns into different modules
- **TypeScript Best Practices** - Use strong typing and interfaces
- **Error Handling** - Implement proper error handling
- **Documentation** - Document code with JSDoc comments

### Performance
- **Object Pooling** - Use object pooling for frequently created objects
- **Asset Loading** - Load assets asynchronously
- **Memory Management** - Properly manage memory and avoid leaks
- **Update Optimization** - Optimize update loops

### Platform Compatibility
- **Cross-Platform Testing** - Test on all target platforms
- **Platform-Specific Code** - Handle platform differences
- **Responsive Design** - Design for different screen sizes
- **Input Handling** - Handle different input methods

---

*Development Reference*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
