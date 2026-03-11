# Phaser Architecture Guide

## 🎯 Overview

This guide covers the architecture and best practices for Phaser JS game development within the OpenAgenticGame architecture. Understanding Phaser's architecture is essential for building scalable, maintainable, and performant web games.

## 🏗️ Team Integration

### **Primary Team**: Programming Team
- **Lead Agent**: `cocos-creator-specialist` - Web game development specialist
- **Contributors**: `technical-programmer`, `performance-analyst`
- **Cross-Team**: Design Team (game mechanics), Art Team (visual assets), QA Team (testing)

### **Agent Responsibilities**
- **cocos-creator-specialist**: Phaser/Cocos Creator web game development
- **technical-programmer**: Web game architecture and optimization
- **performance-analyst**: Web game performance analysis and optimization
- **qa-lead**: Web game testing and quality assurance

## 🏛️ **Phaser Core Architecture**

### **Game Engine Structure**
```
Phaser Game
├── Game Loop
├── Scene Manager
├── Renderer (Canvas/WebGL)
├── Physics Engine
├── Input Manager
├── Audio Manager
├── Animation Manager
├── Particle Manager
└── Texture Manager
```

### **Game Flow Architecture**
```javascript
// Game Initialization Flow
Game Constructor
├── Create Renderer
├── Initialize Systems
├── Load Configuration
├── Setup Event Listeners
└── Start Game Loop

// Game Loop Flow
Game Loop
├── Update Input
├── Update Physics
├── Update Animations
├── Update Particles
├── Update Audio
├── Render Frame
└── Handle Events
```

## 🎭 **Scene System Architecture**

### **Scene Management**
```javascript
// Scene Manager Architecture
SceneManager
├── Active Scene Stack
├── Scene Transitions
├── Scene Data Sharing
└── Scene Lifecycle Management

// Scene Lifecycle
Scene Lifecycle
├── init() - Initialize scene data
├── preload() - Load assets
├── create() - Create game objects
├── update() - Game loop updates
├── pause() - Pause scene
├── resume() - Resume scene
├── shutdown() - Clean up scene
└── destroy() - Destroy scene
```

### **Scene Architecture Pattern**
```javascript
// Base Scene Class
export class BaseScene extends Scene {
    constructor(key) {
        super({ key });
        this.systems = new Map();
        this.entities = new Map();
        this.ui = new Map();
    }

    create() {
        this.createSystems();
        this.createEntities();
        this.createUI();
        this.setupEventListeners();
    }

    createSystems() {
        // Create game systems
        this.systems.set('physics', this.physics);
        this.systems.set('audio', this.sound);
        this.systems.set('input', this.input);
        this.systems.set('camera', this.cameras.main);
    }

    createEntities() {
        // Create game entities
        this.entities.set('player', new Player(this));
        this.entities.set('enemies', new EnemyManager(this));
        this.entities.set('bullets', new BulletManager(this));
    }

    createUI() {
        // Create UI elements
        this.ui.set('score', new ScoreUI(this));
        this.ui.set('health', new HealthUI(this));
        this.ui.set('menu', new MenuUI(this));
    }

    update(time, delta) {
        // Update systems
        this.updateSystems(time, delta);
        
        // Update entities
        this.updateEntities(time, delta);
        
        // Update UI
        this.updateUI(time, delta);
    }
}
```

### **Scene Communication**
```javascript
// Scene Data Sharing
class SceneData {
    constructor() {
        this.sharedData = new Map();
        this.eventBus = new EventBus();
    }

    setData(key, value) {
        this.sharedData.set(key, value);
        this.eventBus.emit('dataChanged', { key, value });
    }

    getData(key) {
        return this.sharedData.get(key);
    }

    on(event, callback) {
        this.eventBus.on(event, callback);
    }

    emit(event, data) {
        this.eventBus.emit(event, data);
    }
}

// Scene Communication Example
export class GameScene extends BaseScene {
    constructor() {
        super('GameScene');
        this.sceneData = new SceneData();
    }

    create() {
        super.create();
        
        // Listen for events from other scenes
        this.sceneData.on('playerDeath', this.handlePlayerDeath, this);
        this.sceneData.on('levelComplete', this.handleLevelComplete, this);
    }

    handlePlayerDeath(data) {
        // Handle player death
        this.sceneData.setData('score', data.score);
        this.scene.start('GameOverScene');
    }

    handleLevelComplete(data) {
        // Handle level completion
        this.sceneData.setData('nextLevel', data.level + 1);
        this.scene.start('LevelCompleteScene');
    }
}
```

## 🎮 **Entity System Architecture**

### **Entity Component System**
```javascript
// Base Entity Class
export class Entity extends Phaser.GameObjects.Sprite {
    constructor(scene, x, y, texture) {
        super(scene, x, y, texture);
        
        this.components = new Map();
        this.active = true;
        this.visible = true;
        
        this.init();
    }

    init() {
        // Initialize entity
        this.addComponent(new TransformComponent(this));
        this.addComponent(new HealthComponent(this));
        this.addComponent(new MovementComponent(this));
    }

    addComponent(component) {
        component.setEntity(this);
        this.components.set(component.constructor.name, component);
        return component;
    }

    getComponent(ComponentClass) {
        return this.components.get(ComponentClass.name);
    }

    hasComponent(ComponentClass) {
        return this.components.has(ComponentClass.name);
    }

    removeComponent(ComponentClass) {
        const component = this.components.get(ComponentClass.name);
        if (component) {
            component.destroy();
            this.components.delete(ComponentClass.name);
        }
        return component;
    }

    update(time, delta) {
        if (!this.active) return;
        
        // Update all components
        this.components.forEach(component => {
            if (component.update) {
                component.update(time, delta);
            }
        });
    }
}
```

### **Component System**
```javascript
// Base Component Class
export class Component {
    constructor() {
        this.entity = null;
        this.active = true;
    }

    setEntity(entity) {
        this.entity = entity;
        this.init();
    }

    init() {
        // Initialize component
    }

    update(time, delta) {
        // Update component
    }

    destroy() {
        // Clean up component
        this.entity = null;
        this.active = false;
    }
}

// Movement Component
export class MovementComponent extends Component {
    constructor() {
        super();
        this.velocity = { x: 0, y: 0 };
        this.speed = 5;
        this.acceleration = 0.1;
        this.friction = 0.95;
    }

    init() {
        // Initialize movement
    }

    update(time, delta) {
        // Update position
        this.entity.x += this.velocity.x * delta * 0.001;
        this.entity.y += this.velocity.y * delta * 0.001;
        
        // Apply friction
        this.velocity.x *= this.friction;
        this.velocity.y *= this.friction;
    }

    move(direction, speed = this.speed) {
        this.velocity.x = direction.x * speed;
        this.velocity.y = direction.y * speed;
    }

    stop() {
        this.velocity.x = 0;
        this.velocity.y = 0;
    }
}

// Health Component
export class HealthComponent extends Component {
    constructor() {
        super();
        this.health = 100;
        this.maxHealth = 100;
        this.invulnerable = false;
        this.invulnerableTime = 0;
    }

    init() {
        // Initialize health
    }

    update(time, delta) {
        // Update invulnerability
        if (this.invulnerable) {
            this.invulnerableTime -= delta;
            if (this.invulnerableTime <= 0) {
                this.invulnerable = false;
            }
        }
    }

    takeDamage(amount) {
        if (this.invulnerable) return;
        
        this.health -= amount;
        this.health = Math.max(0, this.health);
        
        // Set invulnerability
        this.invulnerable = true;
        this.invulnerableTime = 1000;
        
        // Emit damage event
        this.entity.emit('damage', { amount, health: this.health });
        
        if (this.health <= 0) {
            this.entity.emit('death');
        }
    }

    heal(amount) {
        this.health += amount;
        this.health = Math.min(this.health, this.maxHealth);
        
        // Emit heal event
        this.entity.emit('heal', { amount, health: this.health });
    }
}
```

### **Entity Factory**
```javascript
// Entity Factory
export class EntityFactory {
    constructor(scene) {
        this.scene = scene;
        this.templates = new Map();
        this.pools = new Map();
    }

    registerTemplate(name, template) {
        this.templates.set(name, template);
    }

    create(type, x, y, config = {}) {
        const template = this.templates.get(type);
        if (!template) {
            throw new Error(`Entity template not found: ${type}`);
        }

        // Get from pool or create new
        const entity = this.getFromPool(type) || this.createNew(type, x, y, template);
        
        // Configure entity
        this.configureEntity(entity, config);
        
        return entity;
    }

    createNew(type, x, y, template) {
        const entity = new template.class(this.scene, x, y, template.texture);
        
        // Add components
        template.components.forEach(componentConfig => {
            const component = new componentConfig.class();
            entity.addComponent(component);
        });
        
        return entity;
    }

    configureEntity(entity, config) {
        Object.keys(config).forEach(key => {
            if (entity.hasComponent(key)) {
                const component = entity.getComponent(key);
                Object.assign(component, config[key]);
            }
        });
    }

    getFromPool(type) {
        const pool = this.pools.get(type);
        if (pool && pool.length > 0) {
            return pool.pop();
        }
        return null;
    }

    returnToPool(type, entity) {
        let pool = this.pools.get(type);
        if (!pool) {
            pool = [];
            this.pools.set(type, pool);
        }
        
        entity.active = false;
        entity.visible = false;
        pool.push(entity);
    }
}
```

## 🔧 **System Architecture**

### **System Manager**
```javascript
// System Manager
export class SystemManager {
    constructor(scene) {
        this.scene = scene;
        this.systems = new Map();
        this.updateOrder = [];
    }

    addSystem(name, system, priority = 0) {
        this.systems.set(name, system);
        this.updateOrder.push({ name, priority });
        this.updateOrder.sort((a, b) => a.priority - b.priority);
    }

    getSystem(name) {
        return this.systems.get(name);
    }

    update(time, delta) {
        this.updateOrder.forEach(({ name }) => {
            const system = this.systems.get(name);
            if (system && system.active) {
                system.update(time, delta);
            }
        });
    }

    destroy() {
        this.systems.forEach(system => {
            if (system.destroy) {
                system.destroy();
            }
        });
        this.systems.clear();
        this.updateOrder.length = 0;
    }
}
```

### **Base System Class**
```javascript
// Base System Class
export class System {
    constructor(scene) {
        this.scene = scene;
        this.active = true;
        this.entities = new Set();
        this.components = new Set();
    }

    addEntity(entity) {
        this.entities.add(entity);
        this.onEntityAdded(entity);
    }

    removeEntity(entity) {
        this.entities.delete(entity);
        this.onEntityRemoved(entity);
    }

    requireComponent(ComponentClass) {
        this.components.add(ComponentClass.name);
    }

    onEntityAdded(entity) {
        // Called when entity is added
    }

    onEntityRemoved(entity) {
        // Called when entity is removed
    }

    update(time, delta) {
        // Update system
        this.entities.forEach(entity => {
            if (this.matchesEntity(entity)) {
                this.updateEntity(entity, time, delta);
            }
        });
    }

    matchesEntity(entity) {
        for (const componentName of this.components) {
            if (!entity.hasComponent(componentName)) {
                return false;
            }
        }
        return true;
    }

    updateEntity(entity, time, delta) {
        // Update individual entity
    }

    destroy() {
        this.entities.clear();
        this.components.clear();
        this.active = false;
    }
}
```

### **Movement System**
```javascript
// Movement System
export class MovementSystem extends System {
    constructor(scene) {
        super(scene);
        this.requireComponent(MovementComponent);
        this.requireComponent(TransformComponent);
    }

    updateEntity(entity, time, delta) {
        const movement = entity.getComponent(MovementComponent);
        const transform = entity.getComponent(TransformComponent);
        
        if (movement && transform) {
            // Update position
            transform.position.x += movement.velocity.x * delta * 0.001;
            transform.position.y += movement.velocity.y * delta * 0.001;
            
            // Apply friction
            movement.velocity.x *= movement.friction;
            movement.velocity.y *= movement.friction;
            
            // Update entity position
            entity.x = transform.position.x;
            entity.y = transform.position.y;
        }
    }
}
```

### **Collision System**
```javascript
// Collision System
export class CollisionSystem extends System {
    constructor(scene) {
        super(scene);
        this.requireComponent(ColliderComponent);
        this.collisionPairs = new Map();
    }

    update(time, delta) {
        this.checkCollisions();
        this.handleCollisions();
    }

    checkCollisions() {
        const entities = Array.from(this.entities);
        
        for (let i = 0; i < entities.length; i++) {
            for (let j = i + 1; j < entities.length; j++) {
                const entityA = entities[i];
                const entityB = entities[j];
                
                if (this.checkCollision(entityA, entityB)) {
                    const pair = `${entityA.id}-${entityB.id}`;
                    this.collisionPairs.set(pair, { entityA, entityB });
                }
            }
        }
    }

    checkCollision(entityA, entityB) {
        const colliderA = entityA.getComponent(ColliderComponent);
        const colliderB = entityB.getComponent(ColliderComponent);
        
        if (!colliderA || !colliderB) return false;
        
        // Simple AABB collision
        const boundsA = colliderA.getBounds();
        const boundsB = colliderB.getBounds();
        
        return boundsA.overlaps(boundsB);
    }

    handleCollisions() {
        this.collisionPairs.forEach(({ entityA, entityB }) => {
            this.handleCollision(entityA, entityB);
        });
        
        this.collisionPairs.clear();
    }

    handleCollision(entityA, entityB) {
        // Emit collision events
        entityA.emit('collision', { other: entityB });
        entityB.emit('collision', { other: entityA });
        
        // Handle specific collision types
        this.handleSpecificCollision(entityA, entityB);
        this.handleSpecificCollision(entityB, entityA);
    }

    handleSpecificCollision(entityA, entityB) {
        // Handle specific collision logic
        const healthA = entityA.getComponent(HealthComponent);
        const healthB = entityB.getComponent(HealthComponent);
        
        if (healthA) {
            healthA.takeDamage(10);
        }
    }
}
```

## 🎨 **Rendering Architecture**

### **Rendering Pipeline**
```javascript
// Rendering Pipeline
export class RenderingPipeline {
    constructor(scene) {
        this.scene = scene;
        this.layers = new Map();
        this.camera = scene.cameras.main;
    }

    addLayer(name, zIndex = 0) {
        const layer = new Phaser.GameObjects.Container(scene);
        layer.setDepth(zIndex);
        this.layers.set(name, layer);
        scene.add.existing(layer);
        return layer;
    }

    addToLayer(layerName, gameObject) {
        const layer = this.layers.get(layerName);
        if (layer) {
            layer.add(gameObject);
        }
    }

    render() {
        // Render layers in order
        this.layers.forEach(layer => {
            if (layer.visible) {
                this.camera.render(layer);
            }
        });
    }
}
```

### **Sprite Management**
```javascript
// Sprite Manager
export class SpriteManager {
    constructor(scene) {
        this.scene = scene;
        this.sprites = new Map();
        this.atlases = new Map();
        this.animations = new Map();
    }

    loadAtlas(key, atlasUrl, imageUrl) {
        return this.scene.load.atlas(key, atlasUrl, imageUrl);
    }

    createSprite(key, x, y, frame) {
        const sprite = this.scene.add.sprite(x, y, key, frame);
        this.sprites.set(sprite.name || sprite.id, sprite);
        return sprite;
    }

    createAnimation(key, config) {
        const anim = this.scene.anims.create(config);
        this.animations.set(key, anim);
        return anim;
    }

    playAnimation(sprite, animationKey) {
        const anim = this.animations.get(animationKey);
        if (anim) {
            sprite.play(animationKey);
        }
    }
}
```

## 🎵 **Audio Architecture**

### **Audio Manager**
```javascript
// Audio Manager
export class AudioManager {
    constructor(scene) {
        this.scene = scene;
        this.sounds = new Map();
        this.music = new Map();
        this.volume = {
            master: 1,
            music: 0.3,
            sfx: 0.5
        };
        this.muted = false;
    }

    loadSound(key, config) {
        const sound = this.scene.sound.add(key, config);
        this.sounds.set(key, sound);
        return sound;
    }

    loadMusic(key, config) {
        const music = this.scene.sound.add(key, config);
        this.music.set(key, music);
        return music;
    }

    playSound(key, config = {}) {
        const sound = this.sounds.get(key);
        if (sound && !this.muted) {
            sound.play(config);
            sound.setVolume(this.volume.sfx * this.volume.master);
        }
        return sound;
    }

    playMusic(key, config = {}) {
        const music = this.music.get(key);
        if (music && !this.muted) {
            music.play(config);
            music.setVolume(this.volume.music * this.volume.master);
        }
        return music;
    }

    setVolume(type, volume) {
        this.volume[type] = Math.max(0, Math.min(1, volume));
        this.updateVolumes();
    }

    updateVolumes() {
        this.sounds.forEach(sound => {
            sound.setVolume(this.volume.sfx * this.volume.master);
        });
        
        this.music.forEach(music => {
            music.setVolume(this.volume.music * this.volume.master);
        });
    }

    mute() {
        this.muted = true;
        this.scene.sound.pauseAll();
    }

    unmute() {
        this.muted = false;
        this.scene.sound.resumeAll();
    }
}
```

## 📊 **Performance Architecture**

### **Performance Monitor**
```javascript
// Performance Monitor
export class PerformanceMonitor {
    constructor(scene) {
        this.scene = scene;
        this.metrics = {
            fps: 60,
            frameTime: 16.67,
            memory: 0,
            entities: 0,
            drawCalls: 0
        };
        this.history = {
            fps: [],
            frameTime: [],
            memory: []
        };
        this.maxHistorySize = 60;
    }

    update(time, delta) {
        this.updateMetrics(time, delta);
        this.updateHistory();
        this.checkPerformance();
    }

    updateMetrics(time, delta) {
        // Update FPS
        this.metrics.fps = this.scene.game.loop.actualFps;
        this.metrics.frameTime = delta;
        
        // Update memory (if available)
        if (performance.memory) {
            this.metrics.memory = performance.memory.usedJSHeapSize / 1024 / 1024;
        }
        
        // Update entity count
        this.metrics.entities = this.scene.children.length;
        
        // Update draw calls (approximate)
        this.metrics.drawCalls = this.scene.renderer.drawCount;
    }

    updateHistory() {
        this.history.fps.push(this.metrics.fps);
        this.history.frameTime.push(this.metrics.frameTime);
        this.history.memory.push(this.metrics.memory);
        
        // Limit history size
        if (this.history.fps.length > this.maxHistorySize) {
            this.history.fps.shift();
            this.history.frameTime.shift();
            this.history.memory.shift();
        }
    }

    checkPerformance() {
        // Check for performance issues
        if (this.metrics.fps < 30) {
            console.warn('Low FPS detected:', this.metrics.fps);
        }
        
        if (this.metrics.memory > 100) {
            console.warn('High memory usage detected:', this.metrics.memory, 'MB');
        }
        
        if (this.metrics.frameTime > 33) {
            console.warn('High frame time detected:', this.metrics.frameTime, 'ms');
        }
    }

    getMetrics() {
        return { ...this.metrics };
    }

    getAverageMetrics() {
        return {
            avgFps: this.calculateAverage(this.history.fps),
            avgFrameTime: this.calculateAverage(this.history.frameTime),
            avgMemory: this.calculateAverage(this.history.memory)
        };
    }

    calculateAverage(array) {
        if (array.length === 0) return 0;
        return array.reduce((sum, value) => sum + value, 0) / array.length;
    }
}
```

## 🎯 **Best Practices**

### **Code Organization**
- **Modular Design**: Separate concerns into modules
- **Component Architecture**: Use component-based design
- **System Separation**: Separate systems for different concerns
- **Event-Driven**: Use event-driven architecture

### **Performance Guidelines**
- **Object Pooling**: Use object pools for frequently created objects
- **Batch Operations**: Batch similar operations
- **Memory Management**: Clean up unused resources
- **Rendering Optimization**: Optimize rendering pipeline

### **Scalability**
- **Scene Management**: Use scenes for different game states
- **Entity Management**: Use entity-component system
- **System Architecture**: Use system-based architecture
- **Data Management**: Use data-driven design

### **Maintainability**
- **Documentation**: Document code and architecture
- **Testing**: Write tests for critical components
- **Code Review**: Review code regularly
- **Refactoring**: Refactor code regularly

---

## 📚 **Architecture Patterns**

### **MVC Pattern**
```javascript
// Model-View-Controller Pattern
class GameModel {
    constructor() {
        this.score = 0;
        this.health = 100;
        this.level = 1;
    }
}

class GameView {
    constructor(scene) {
        this.scene = scene;
        this.scoreText = scene.add.text(10, 10, 'Score: 0');
        this.healthBar = scene.add.graphics();
    }
}

class GameController {
    constructor(model, view) {
        this.model = model;
        this.view = view;
    }
    
    updateScore(points) {
        this.model.score += points;
        this.view.scoreText.setText(`Score: ${this.model.score}`);
    }
}
```

### **Observer Pattern**
```javascript
// Observer Pattern
class EventManager {
    constructor() {
        this.listeners = new Map();
    }
    
    on(event, callback) {
        if (!this.listeners.has(event)) {
            this.listeners.set(event, []);
        }
        this.listeners.get(event).push(callback);
    }
    
    emit(event, data) {
        const callbacks = this.listeners.get(event);
        if (callbacks) {
            callbacks.forEach(callback => callback(data));
        }
    }
}
```

### **Factory Pattern**
```javascript
// Factory Pattern
class EntityFactory {
    static createEnemy(type, scene, x, y) {
        switch (type) {
            case 'basic':
                return new BasicEnemy(scene, x, y);
            case 'fast':
                return new FastEnemy(scene, x, y);
            case 'heavy':
                return new HeavyEnemy(scene, x, y);
            default:
                throw new Error(`Unknown enemy type: ${type}`);
        }
    }
}
```

---

## 🎯 **Getting Help**

### **Architecture Resources**
- **Phaser Documentation**: https://phaser.io/docs/
- **Architecture Guide**: https://phaser.io/learn/architecture/
- **Examples**: https://phaser.io/examples/
- **Community**: https://phaser.io/community/

### **Learning Resources**
- **Books**: Game Architecture Patterns
- **Courses**: Game Development Courses
- **Tutorials**: Architecture Tutorials
- **Articles**: Architecture Articles

---

*Phaser Architecture Guide*
*Version: 3.60+*
*Last Updated: 2026-03-10*
*Team: Programming Team*
*Specialist: cocos-creator-specialist*
*Platform: Web*
