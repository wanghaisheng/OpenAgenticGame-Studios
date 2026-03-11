# Phaser Performance Optimization Guide

## 🎯 Overview

This guide covers performance optimization techniques for Phaser JS games within the OpenAgenticGame architecture. Performance optimization is crucial for delivering smooth, responsive web games that run well across different devices and browsers.

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

## 📊 **Performance Metrics**

### **Key Performance Indicators**
- **Frame Rate (FPS)**: Target 60 FPS, minimum 30 FPS
- **Frame Time**: Target < 16.67ms, maximum < 33ms
- **Memory Usage**: Target < 100MB, maximum < 200MB
- **Draw Calls**: Target < 100, maximum < 500
- **Texture Memory**: Target < 50MB, maximum < 100MB

### **Performance Monitoring**
```javascript
// Performance Monitor
export class PerformanceMonitor {
    constructor(scene) {
        this.scene = scene;
        this.metrics = {
            fps: 60,
            frameTime: 16.67,
            memory: 0,
            drawCalls: 0,
            entities: 0
        };
        this.history = {
            fps: [],
            frameTime: [],
            memory: []
        };
        this.maxHistorySize = 60;
        this.warningThreshold = {
            fps: 30,
            frameTime: 33,
            memory: 100
        };
    }

    update(time, delta) {
        this.updateMetrics(time, delta);
        this.updateHistory();
        this.checkPerformance();
        this.displayMetrics();
    }

    updateMetrics(time, delta) {
        this.metrics.fps = this.scene.game.loop.actualFps;
        this.metrics.frameTime = delta;
        
        if (performance.memory) {
            this.metrics.memory = performance.memory.usedJSHeapSize / 1024 / 1024;
        }
        
        this.metrics.entities = this.scene.children.length;
        this.metrics.drawCalls = this.scene.renderer.drawCount;
    }

    checkPerformance() {
        if (this.metrics.fps < this.warningThreshold.fps) {
            console.warn(`Low FPS: ${this.metrics.fps}`);
            this.suggestOptimizations('fps');
        }
        
        if (this.metrics.frameTime > this.warningThreshold.frameTime) {
            console.warn(`High frame time: ${this.metrics.frameTime}ms`);
            this.suggestOptimizations('frameTime');
        }
        
        if (this.metrics.memory > this.warningThreshold.memory) {
            console.warn(`High memory usage: ${this.metrics.memory}MB`);
            this.suggestOptimizations('memory');
        }
    }

    suggestOptimizations(issue) {
        const suggestions = {
            fps: [
                'Reduce particle effects',
                'Optimize sprite rendering',
                'Use object pooling',
                'Reduce physics calculations'
            ],
            frameTime: [
                'Optimize update loops',
                'Reduce expensive calculations',
                'Use spatial partitioning',
                'Batch rendering operations'
            ],
            memory: [
                'Clean up unused objects',
                'Use texture atlases',
                'Optimize audio buffers',
                'Reduce asset size'
            ]
        };
        
        const tips = suggestions[issue] || [];
        tips.forEach(tip => console.log(`  - ${tip}`));
    }
}
```

## 🎮 **Rendering Optimization**

### **Canvas vs WebGL**
```javascript
// WebGL Configuration
const config = {
    type: Phaser.WEBGL, // Use WebGL for better performance
    render: {
        pixelArt: true,  // Pixel art rendering
        antialias: false, // Disable antialiasing for pixel art
        roundPixels: true // Round pixel values
    },
    backgroundColor: '#000000'
};

// Canvas Fallback
if (!this.renderer.type === Phaser.WEBGL) {
    console.warn('WebGL not supported, falling back to Canvas');
    this.config.type = Phaser.CANVAS;
}
```

### **Sprite Optimization**
```javascript
// Sprite Pooling
class SpritePool {
    constructor(scene, texture, maxSize = 100) {
        this.scene = scene;
        this.texture = texture;
        this.maxSize = maxSize;
        this.pool = [];
        this.active = new Set();
    }

    get(x, y) {
        let sprite;
        if (this.pool.length > 0) {
            sprite = this.pool.pop();
            sprite.setPosition(x, y);
        } else {
            sprite = this.scene.add.sprite(x, y, this.texture);
        }
        
        sprite.setActive(true);
        sprite.setVisible(true);
        this.active.add(sprite);
        return sprite;
    }

    release(sprite) {
        if (this.active.has(sprite)) {
            sprite.setActive(false);
            sprite.setVisible(false);
            this.active.delete(sprite);
            
            if (this.pool.length < this.maxSize) {
                this.pool.push(sprite);
            } else {
                sprite.destroy();
            }
        }
    }

    releaseAll() {
        this.active.forEach(sprite => this.release(sprite));
    }
}
```

### **Texture Optimization**
```javascript
// Texture Atlas Usage
class TextureManager {
    constructor(scene) {
        this.scene = scene;
        this.atlases = new Map();
        this.textures = new Map();
    }

    loadAtlas(key, atlasUrl, imageUrl) {
        return this.scene.load.atlas(key, atlasUrl, imageUrl);
    }

    createSpriteFromAtlas(atlasKey, frameName, x, y) {
        return this.scene.add.sprite(x, y, atlasKey, frameName);
    }

    optimizeTextures() {
        // Use texture atlases to reduce draw calls
        this.scene.textures.list.forEach(texture => {
            if (texture.source.length > 1) {
                console.log(`Texture atlas: ${texture.key} has ${texture.source.length} frames`);
            }
        });
    }
}
```

### **Batch Rendering**
```javascript
// Batch Rendering System
class BatchRenderer {
    constructor(scene) {
        this.scene = scene;
        this.batches = new Map();
    }

    createBatch(key, texture) {
        const batch = this.scene.add.graphics();
        this.batches.set(key, batch);
        return batch;
    }

    addToBatch(batchKey, drawFunction) {
        const batch = this.batches.get(batchKey);
        if (batch) {
            batch.clear();
            drawFunction(batch);
        }
    }

    renderBatches() {
        this.batches.forEach(batch => {
            batch.setDepth(0);
        });
    }
}
```

## 🧮 **Physics Optimization**

### **Physics World Optimization**
```javascript
// Physics Configuration
const physicsConfig = {
    default: 'arcade',
    arcade: {
        gravity: { y: 0 },
        debug: false, // Disable debug in production
        fps: 60,     // Physics FPS
        timeStep: 1 / 60,
        maxSubSteps: 4,
        overlapBias: 4,
        tileBias: 16
    }
};

// Spatial Partitioning
class SpatialGrid {
    constructor(width, height, cellSize) {
        this.width = width;
        this.height = height;
        this.cellSize = cellSize;
        this.cells = new Map();
    }

    getCellKey(x, y) {
        const cellX = Math.floor(x / this.cellSize);
        const cellY = Math.floor(y / this.cellSize);
        return `${cellX},${cellY}`;
    }

    addEntity(entity) {
        const key = this.getCellKey(entity.x, entity.y);
        if (!this.cells.has(key)) {
            this.cells.set(key, new Set());
        }
        this.cells.get(key).add(entity);
    }

    removeEntity(entity) {
        const key = this.getCellKey(entity.x, entity.y);
        const cell = this.cells.get(key);
        if (cell) {
            cell.delete(entity);
            if (cell.size === 0) {
                this.cells.delete(key);
            }
        }
    }

    getNearbyEntities(x, y, radius) {
        const nearby = new Set();
        const cellRadius = Math.ceil(radius / this.cellSize);
        
        for (let dx = -cellRadius; dx <= cellRadius; dx++) {
            for (let dy = -cellRadius; dy <= cellRadius; dy++) {
                const key = this.getCellKey(x + dx * this.cellSize, y + dy * this.cellSize);
                const cell = this.cells.get(key);
                if (cell) {
                    cell.forEach(entity => nearby.add(entity));
                }
            }
        }
        
        return nearby;
    }
}
```

### **Collision Optimization**
```javascript
// Optimized Collision System
class CollisionSystem {
    constructor(scene) {
        this.scene = scene;
        this.spatialGrid = new SpatialGrid(800, 600, 50);
        this.collisionPairs = new Set();
        this.collisionTypes = new Map();
    }

    update() {
        this.updateSpatialGrid();
        this.checkCollisions();
        this.handleCollisions();
    }

    updateSpatialGrid() {
        // Clear grid
        this.spatialGrid.cells.clear();
        
        // Add entities to grid
        this.scene.children.list.forEach(entity => {
            if (entity.active && entity.body) {
                this.spatialGrid.addEntity(entity);
            }
        });
    }

    checkCollisions() {
        this.collisionPairs.clear();
        
        this.scene.children.list.forEach(entityA => {
            if (!entityA.active || !entityA.body) return;
            
            const nearby = this.spatialGrid.getNearbyEntities(
                entityA.x, entityA.y, 100
            );
            
            nearby.forEach(entityB => {
                if (entityA !== entityB && entityB.active && entityB.body) {
                    const pairKey = `${entityA.id}-${entityB.id}`;
                    const reverseKey = `${entityB.id}-${entityA.id}`;
                    
                    if (!this.collisionPairs.has(reverseKey)) {
                        if (this.checkCollision(entityA, entityB)) {
                            this.collisionPairs.add(pairKey);
                        }
                    }
                }
            });
        });
    }

    checkCollision(entityA, entityB) {
        // Simple AABB collision
        const boundsA = entityA.getBounds();
        const boundsB = entityB.getBounds();
        return boundsA.intersects(boundsB);
    }

    handleCollisions() {
        this.collisionPairs.forEach(pairKey => {
            const [idA, idB] = pairKey.split('-');
            const entityA = this.scene.children.list.find(e => e.id === parseInt(idA));
            const entityB = this.scene.children.list.find(e => e.id === parseInt(idB));
            
            if (entityA && entityB) {
                this.handleCollision(entityA, entityB);
            }
        });
    }

    handleCollision(entityA, entityB) {
        // Emit collision events
        entityA.emit('collision', { other: entityB });
        entityB.emit('collision', { other: entityA });
    }
}
```

## 🎵 **Audio Optimization**

### **Audio Pooling**
```javascript
// Audio Pool Manager
class AudioPool {
    constructor(scene) {
        this.scene = scene;
        this.pools = new Map();
        this.maxPoolSize = 10;
    }

    createPool(soundKey, config = {}) {
        const pool = {
            sounds: [],
            available: [],
            config: config
        };
        
        for (let i = 0; i < this.maxPoolSize; i++) {
            const sound = this.scene.sound.add(soundKey, config);
            pool.sounds.push(sound);
            pool.available.push(sound);
        }
        
        this.pools.set(soundKey, pool);
    }

    play(soundKey, config = {}) {
        const pool = this.pools.get(soundKey);
        if (!pool) {
            console.warn(`Audio pool not found: ${soundKey}`);
            return null;
        }
        
        let sound;
        if (pool.available.length > 0) {
            sound = pool.available.pop();
        } else {
            sound = pool.sounds[0]; // Reuse oldest sound
            sound.stop();
        }
        
        sound.play(config);
        
        sound.on('complete', () => {
            pool.available.push(sound);
        });
        
        return sound;
    }

    stopAll(soundKey) {
        const pool = this.pools.get(soundKey);
        if (pool) {
            pool.sounds.forEach(sound => sound.stop());
        }
    }
}
```

### **Audio Compression**
```javascript
// Audio Optimization
class AudioOptimizer {
    constructor() {
        this.compressionSettings = {
            mp3: { bitrate: 128, sampleRate: 22050 },
            ogg: { quality: 6 },
            wav: { bitDepth: 16, sampleRate: 22050 }
        };
    }

    compressAudio(audioBuffer, format = 'mp3') {
        const settings = this.compressionSettings[format];
        
        // Implement audio compression logic
        // This would typically use Web Audio API or external libraries
        return audioBuffer;
    }

    preloadOptimizedAudio(scene, audioFiles) {
        audioFiles.forEach(file => {
            const optimizedFile = this.getOptimizedFile(file);
            scene.load.audio(file.key, optimizedFile.url);
        });
    }

    getOptimizedFile(file) {
        // Return optimized audio file based on device capabilities
        if (this.supportsWebAudio()) {
            return { url: file.url + '.webm', format: 'webm' };
        }
        return { url: file.url + '.mp3', format: 'mp3' };
    }

    supportsWebAudio() {
        return !!(window.AudioContext || window.webkitAudioContext);
    }
}
```

## 🧠 **Memory Management**

### **Object Pooling**
```javascript
// Universal Object Pool
class ObjectPool {
    constructor(createFn, resetFn, maxSize = 100) {
        this.createFn = createFn;
        this.resetFn = resetFn;
        this.maxSize = maxSize;
        this.pool = [];
        this.active = new Set();
    }

    get() {
        let obj;
        if (this.pool.length > 0) {
            obj = this.pool.pop();
        } else {
            obj = this.createFn();
        }
        
        this.active.add(obj);
        return obj;
    }

    release(obj) {
        if (this.active.has(obj)) {
            this.resetFn(obj);
            this.active.delete(obj);
            
            if (this.pool.length < this.maxSize) {
                this.pool.push(obj);
            } else {
                this.destroyObject(obj);
            }
        }
    }

    releaseAll() {
        this.active.forEach(obj => this.release(obj));
    }

    destroyObject(obj) {
        if (obj.destroy) {
            obj.destroy();
        }
    }

    getStats() {
        return {
            poolSize: this.pool.length,
            activeCount: this.active.size,
            totalCreated: this.pool.length + this.active.size
        };
    }
}
```

### **Memory Monitoring**
```javascript
// Memory Monitor
class MemoryMonitor {
    constructor() {
        this.thresholds = {
            warning: 100,  // MB
            critical: 150  // MB
        };
        this.history = [];
        this.maxHistorySize = 60;
    }

    checkMemory() {
        if (performance.memory) {
            const used = performance.memory.usedJSHeapSize / 1024 / 1024;
            const total = performance.memory.totalJSHeapSize / 1024 / 1024;
            
            this.updateHistory(used, total);
            this.checkThresholds(used, total);
            
            return { used, total };
        }
        return null;
    }

    updateHistory(used, total) {
        this.history.push({ used, total, timestamp: Date.now() });
        
        if (this.history.length > this.maxHistorySize) {
            this.history.shift();
        }
    }

    checkThresholds(used, total) {
        if (used > this.thresholds.critical) {
            console.error(`Critical memory usage: ${used.toFixed(2)}MB`);
            this.suggestCleanup();
        } else if (used > this.thresholds.warning) {
            console.warn(`High memory usage: ${used.toFixed(2)}MB`);
        }
    }

    suggestCleanup() {
        const suggestions = [
            'Clear unused textures',
            'Release object pools',
            'Stop audio playback',
            'Clear particle systems',
            'Destroy inactive entities'
        ];
        
        suggestions.forEach(suggestion => console.log(`  - ${suggestion}`));
    }

    getAverageUsage() {
        if (this.history.length === 0) return 0;
        
        const total = this.history.reduce((sum, entry) => sum + entry.used, 0);
        return total / this.history.length;
    }
}
```

### **Garbage Collection Optimization**
```javascript
// Garbage Collection Helper
class GCHelper {
    constructor() {
        this.cleanupTasks = [];
        this.cleanupInterval = 5000; // 5 seconds
        this.lastCleanup = 0;
    }

    addCleanupTask(task) {
        this.cleanupTasks.push(task);
    }

    performCleanup() {
        const now = Date.now();
        if (now - this.lastCleanup < this.cleanupInterval) {
            return;
        }
        
        this.cleanupTasks.forEach(task => {
            try {
                task();
            } catch (error) {
                console.error('Cleanup task failed:', error);
            }
        });
        
        this.lastCleanup = now;
        
        // Suggest garbage collection if available
        if (window.gc) {
            window.gc();
        }
    }

    createCleanupTask(pool) {
        return () => {
            pool.releaseAll();
        };
    }
}
```

## 🎨 **Asset Optimization**

### **Image Optimization**
```javascript
// Asset Optimizer
class AssetOptimizer {
    constructor() {
        this.optimizationStrategies = {
            images: {
                compression: 0.8,
                maxWidth: 2048,
                maxHeight: 2048,
                format: 'webp'
            },
            audio: {
                bitrate: 128,
                sampleRate: 22050,
                format: 'mp3'
            },
            spritesheets: {
                padding: 2,
                maxSheetSize: 4096,
                powerOfTwo: true
            }
        };
    }

    optimizeImages(images) {
        return images.map(image => {
            return this.optimizeImage(image);
        });
    }

    optimizeImage(image) {
        const strategy = this.optimizationStrategies.images;
        
        // Implement image optimization
        // This would typically use canvas API or external libraries
        return {
            key: image.key,
            url: this.getOptimizedImageUrl(image.url),
            width: Math.min(image.width, strategy.maxWidth),
            height: Math.min(image.height, strategy.maxHeight)
        };
    }

    getOptimizedImageUrl(originalUrl) {
        // Return optimized image URL based on device capabilities
        if (this.supportsWebP()) {
            return originalUrl.replace(/\.(png|jpg|jpeg)$/, '.webp');
        }
        return originalUrl;
    }

    supportsWebP() {
        const canvas = document.createElement('canvas');
        canvas.width = 1;
        canvas.height = 1;
        return canvas.toDataURL('image/webp').indexOf('data:image/webp') === 0;
    }
}
```

### **Sprite Sheet Optimization**
```javascript
// Sprite Sheet Manager
class SpriteSheetManager {
    constructor(scene) {
        this.scene = scene;
        this.sheets = new Map();
        this.maxSheetSize = 4096;
    }

    createSpriteSheet(key, frames, config = {}) {
        const sheet = this.optimizeSpriteSheet(frames, config);
        this.sheets.set(key, sheet);
        return sheet;
    }

    optimizeSpriteSheet(frames, config) {
        const maxWidth = config.maxWidth || this.maxSheetSize;
        const maxHeight = config.maxHeight || this.maxSheetSize;
        
        // Implement sprite sheet optimization
        // This would typically use texture packing algorithms
        return {
            key: config.key,
            frames: frames,
            width: maxWidth,
            height: maxHeight,
            optimized: true
        };
    }

    getFrame(sheetKey, frameName) {
        const sheet = this.sheets.get(sheetKey);
        if (sheet) {
            return sheet.frames.find(frame => frame.name === frameName);
        }
        return null;
    }
}
```

## 📱 **Mobile Optimization**

### **Mobile Performance**
```javascript
// Mobile Optimizer
class MobileOptimizer {
    constructor() {
        this.isMobile = this.detectMobile();
        this.performanceLevel = this.assessPerformance();
    }

    detectMobile() {
        return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
    }

    assessPerformance() {
        if (!this.isMobile) return 'high';
        
        const memory = navigator.deviceMemory || 4;
        const cores = navigator.hardwareConcurrency || 4;
        
        if (memory >= 8 && cores >= 8) return 'high';
        if (memory >= 4 && cores >= 4) return 'medium';
        return 'low';
    }

    getOptimizedConfig(baseConfig) {
        const config = { ...baseConfig };
        
        switch (this.performanceLevel) {
            case 'low':
                config.pixelArt = true;
                config.antialias = false;
                config.render.fps = 30;
                config.physics.arcade.fps = 30;
                break;
            case 'medium':
                config.pixelArt = true;
                config.antialias = false;
                config.render.fps = 45;
                config.physics.arcade.fps = 45;
                break;
            case 'high':
                // Use default high-quality settings
                break;
        }
        
        return config;
    }
}
```

### **Touch Optimization**
```javascript
// Touch Input Optimizer
class TouchOptimizer {
    constructor(scene) {
        this.scene = scene;
        this.touchThreshold = 10;
        this.multiTouch = false;
        this.setupTouchOptimizations();
    }

    setupTouchOptimizations() {
        // Enable multi-touch if supported
        if (this.scene.input.pointer1) {
            this.multiTouch = true;
        }
        
        // Optimize touch events
        this.scene.input.on('pointerdown', this.handleTouchStart, this);
        this.scene.input.on('pointerup', this.handleTouchEnd, this);
        this.scene.input.on('pointermove', this.handleTouchMove, this);
    }

    handleTouchStart(pointer) {
        // Handle touch start with optimization
        this.lastTouchTime = Date.now();
        this.touchStartPos = { x: pointer.x, y: pointer.y };
    }

    handleTouchEnd(pointer) {
        // Handle touch end with optimization
        const touchDuration = Date.now() - this.lastTouchTime;
        
        if (touchDuration < 200) {
            // Quick tap
            this.handleQuickTap(pointer);
        } else {
            // Long press
            this.handleLongPress(pointer);
        }
    }

    handleTouchMove(pointer) {
        // Handle touch move with threshold
        const distance = this.calculateDistance(
            this.touchStartPos, { x: pointer.x, y: pointer.y }
        );
        
        if (distance > this.touchThreshold) {
            this.handleSwipe(pointer);
        }
    }

    calculateDistance(pos1, pos2) {
        const dx = pos2.x - pos1.x;
        const dy = pos2.y - pos1.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

## 🔄 **Update Loop Optimization**

### **Update Loop Management**
```javascript
// Update Loop Optimizer
class UpdateLoopOptimizer {
    constructor(scene) {
        this.scene = scene;
        this.updateGroups = new Map();
        this.updateInterval = 1000 / 60; // 60 FPS
        this.lastUpdate = 0;
    }

    addUpdateGroup(name, objects, interval = this.updateInterval) {
        this.updateGroups.set(name, {
            objects: new Set(objects),
            interval: interval,
            lastUpdate: 0
        });
    }

    update(time, delta) {
        this.updateGroups.forEach((group, name) => {
            if (time - group.lastUpdate >= group.interval) {
                this.updateGroup(group, time, delta);
                group.lastUpdate = time;
            }
        });
    }

    updateGroup(group, time, delta) {
        group.objects.forEach(obj => {
            if (obj.active && obj.update) {
                obj.update(time, delta);
            }
        });
    }

    addToGroup(groupName, object) {
        const group = this.updateGroups.get(groupName);
        if (group) {
            group.objects.add(object);
        }
    }

    removeFromGroup(groupName, object) {
        const group = this.updateGroups.get(groupName);
        if (group) {
            group.objects.delete(object);
        }
    }
}
```

### **Time-based Updates**
```javascript
// Time-based Update System
class TimeBasedUpdate {
    constructor() {
        this.accumulator = 0;
        this.fixedTimeStep = 1000 / 60; // 60 FPS
        this.maxAccumulator = 1000 / 30; // 30 FPS minimum
    }

    update(delta, updateCallback) {
        this.accumulator += delta;
        
        // Clamp accumulator to prevent spiral of death
        this.accumulator = Math.min(this.accumulator, this.maxAccumulator);
        
        while (this.accumulator >= this.fixedTimeStep) {
            updateCallback(this.fixedTimeStep);
            this.accumulator -= this.fixedTimeStep;
        }
    }
}
```

## 📊 **Performance Profiling**

### **Profiler Tool**
```javascript
// Performance Profiler
class PerformanceProfiler {
    constructor() {
        this.profiles = new Map();
        this.currentProfile = null;
        this.startTime = 0;
    }

    startProfile(name) {
        this.currentProfile = name;
        this.startTime = performance.now();
        
        if (!this.profiles.has(name)) {
            this.profiles.set(name, {
                totalTime: 0,
                callCount: 0,
                averageTime: 0,
                minTime: Infinity,
                maxTime: 0
            });
        }
    }

    endProfile() {
        if (!this.currentProfile) return;
        
        const endTime = performance.now();
        const duration = endTime - this.startTime;
        
        const profile = this.profiles.get(this.currentProfile);
        profile.totalTime += duration;
        profile.callCount++;
        profile.averageTime = profile.totalTime / profile.callCount;
        profile.minTime = Math.min(profile.minTime, duration);
        profile.maxTime = Math.max(profile.maxTime, duration);
        
        this.currentProfile = null;
        return duration;
    }

    getProfile(name) {
        return this.profiles.get(name);
    }

    getAllProfiles() {
        return Object.fromEntries(this.profiles);
    }

    resetProfiles() {
        this.profiles.clear();
        this.currentProfile = null;
    }

    printProfiles() {
        console.log('Performance Profiles:');
        this.profiles.forEach((profile, name) => {
            console.log(`${name}:`);
            console.log(`  Total Time: ${profile.totalTime.toFixed(2)}ms`);
            console.log(`  Call Count: ${profile.callCount}`);
            console.log(`  Average Time: ${profile.averageTime.toFixed(2)}ms`);
            console.log(`  Min Time: ${profile.minTime.toFixed(2)}ms`);
            console.log(`  Max Time: ${profile.maxTime.toFixed(2)}ms`);
        });
    }
}
```

### **Profile Decorator**
```javascript
// Profile Decorator
function profile(name) {
    return function(target, propertyKey, descriptor) {
        const originalMethod = descriptor.value;
        
        descriptor.value = function(...args) {
            if (this.profiler) {
                this.profiler.startProfile(name);
                const result = originalMethod.apply(this, args);
                this.profiler.endProfile();
                return result;
            }
            
            return originalMethod.apply(this, args);
        };
        
        return descriptor;
    };
}

// Usage
class GameSystem {
    constructor() {
        this.profiler = new PerformanceProfiler();
    }

    @profile('update')
    update(time, delta) {
        // Update logic
    }

    @profile('render')
    render() {
        // Render logic
    }
}
```

## 🎯 **Best Practices**

### **General Optimization**
- **Profile First**: Always profile before optimizing
- **Measure Impact**: Measure the impact of optimizations
- **Target Bottlenecks**: Focus on actual bottlenecks
- **Test on Target Devices**: Test on actual target devices

### **Rendering Optimization**
- **Use WebGL**: Prefer WebGL over Canvas
- **Batch Operations**: Batch similar operations
- **Reduce Draw Calls**: Minimize draw calls
- **Use Texture Atlases**: Use sprite sheets

### **Memory Optimization**
- **Object Pooling**: Use object pools
- **Clean Up Resources**: Clean up unused resources
- **Monitor Memory**: Monitor memory usage
- **Avoid Leaks**: Avoid memory leaks

### **Performance Monitoring**
- **Use Profiler**: Use performance profiler
- **Monitor FPS**: Monitor frame rate
- **Track Memory**: Track memory usage
- **Set Thresholds**: Set performance thresholds

---

## 📚 **Tools and Resources**

### **Performance Tools**
- **Chrome DevTools**: Performance profiling
- **Firefox Profiler**: Performance analysis
- **Lighthouse**: Performance audit
- **WebPageTest**: Performance testing

### **Optimization Libraries**
- **Three.js**: 3D graphics optimization
- **Pixi.js**: 2D rendering optimization
- **Howler.js**: Audio optimization
- **Tween.js**: Animation optimization

### **Learning Resources**
- **Performance Guide**: https://web.dev/performance/
- **Phaser Performance**: https://phaser.io/tutorials/advanced-performance
- **Web Performance**: https://developers.google.com/web/performance/

---

## 🎯 **Getting Help**

### **Performance Resources**
- **Phaser Documentation**: https://phaser.io/docs/
- **Performance Guide**: https://phaser.io/tutorials/advanced-performance
- **Community Forum**: https://phaser.io/community/
- **Stack Overflow**: https://stackoverflow.com/questions/tagged/phaser

### **Professional Support**
- **Performance Consulting**: Performance optimization services
- **Code Review**: Performance code review
- **Training**: Performance optimization training
- **Support**: Technical support services

---

*Phaser Performance Optimization Guide*
*Version: 3.60+*
*Last Updated: 2026-03-10*
*Team: Programming Team*
*Specialist: cocos-creator-specialist*
*Platform: Web*
