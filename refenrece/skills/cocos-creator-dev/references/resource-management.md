# Resource Management

Loading, releasing, and managing assets in Cocos Creator 3.x.

## Resource Manager Overview

Cocos Creator 3.x uses `assetManager` for all resource operations. It provides:
- Resource loading (local and remote)
- Dependency management
- Memory management
- Asset bundles
- Caching

## Loading Resources

### resources Directory

Resources in `assets/resources/` can be loaded with `resources.load()`:

```
assets/
└── resources/
    ├── textures/
    │   └── player.png
    ├── prefabs/
    │   └── enemy.prefab
    └── audio/
        └── jump.mp3
```

### Basic Loading

```typescript
import { resources, SpriteFrame, Prefab } from 'cc';

// Load single resource
resources.load('textures/player', SpriteFrame, (err, asset) => {
    if (err) {
        console.error('Failed to load:', err);
        return;
    }

    // Use asset
    const sprite = this.node.getComponent(Sprite);
    sprite.spriteFrame = asset;
});

// Load with path
resources.load('prefabs/enemy', Prefab, (err, prefab) => {
    const enemy = instantiate(prefab);
    this.node.addChild(enemy);
});
```

### Loading Arrays

```typescript
// Load all sprites in directory
resources.loadDir('textures/monsters', SpriteFrame, (err, assets) => {
    if (err) {
        console.error('Failed to load:', err);
        return;
    }

    // assets is array of SpriteFrame
    assets.forEach((spriteFrame: SpriteFrame) => {
        console.log('Loaded:', spriteFrame.name);
    });
});
```

### Loading with Promises

```typescript
// Wrap in promise
function loadAsset<T>(path: string, type: typeof Asset): Promise<T> {
    return new Promise((resolve, reject) => {
        resources.load(path, type, (err, asset) => {
            if (err) {
                reject(err);
            } else {
                resolve(asset as T);
            }
        });
    });
}

// Usage with async/await
async loadPlayerSprite() {
    try {
        const spriteFrame = await loadAsset<SpriteFrame>(
            'textures/player',
            SpriteFrame
        );
        this.getComponent(Sprite).spriteFrame = spriteFrame;
    } catch (err) {
        console.error('Load failed:', err);
    }
}
```

## Remote Resources

### Loading Remote URLs

```typescript
import { assetManager } from 'cc';

// Load remote image
assetManager.loadRemote('https://example.com/image.png', (err, imageAsset) => {
    if (err) {
        console.error('Failed to load remote:', err);
        return;
    }

    const spriteFrame = new SpriteFrame();
    spriteFrame.texture = imageAsset;
    this.getComponent(Sprite).spriteFrame = spriteFrame;
});

// Load remote JSON
assetManager.loadRemote('https://api.example.com/data.json', (err, jsonAsset) => {
    if (err) return;

    const data = jsonAsset.json;
    console.log('Loaded data:', data);
});
```

### Download & Cache

```typescript
// Download to cache
assetManager.downloader.downloadFile(
    'https://example.com/bundle.zip',
    { timeout: 30 },
    (err, path) => {
        if (err) {
            console.error('Download failed:', err);
            return;
        }

        console.log('Downloaded to:', path);
    }
);
```

## Asset Bundles

### What are Asset Bundles?

Asset Bundles are packaged groups of assets that can be:
- Loaded dynamically
- Updated separately
- Reduced initial download size
- Organized by feature/level

### Creating Asset Bundles

1. Select folder in **Assets Manager**
2. In **Properties**, check **Bundle**
3. Set bundle name

```
assets/
├── resources/
└── levels/
    └── level1/  (configured as bundle "level1")
        ├── scenes/
        ├── textures/
        └── prefabs/
```

### Loading Asset Bundles

```typescript
@ccclass('BundleLoader')
export class BundleLoader extends Component {
    loadLevelBundle(bundleName: string) {
        // Load bundle
        assetManager.loadBundle(bundleName, (err, bundle) => {
            if (err) {
                console.error('Failed to load bundle:', err);
                return;
            }

            // Load scene from bundle
            bundle.loadScene('game', (err) => {
                if (err) {
                    console.error('Failed to load scene:', err);
                    return;
                }

                director.runScene(bundle.getScene('game'));
            });
        });
    }

    loadAssetFromBundle(bundleName: string, assetPath: string) {
        assetManager.loadBundle(bundleName, (err, bundle) => {
            if (err) {
                console.error('Bundle load failed:', err);
                return;
            }

            // Load specific asset
            bundle.load(assetPath, SpriteFrame, (err, asset) => {
                if (err) {
                    console.error('Asset load failed:', err);
                    return;
                }

                this.getComponent(Sprite).spriteFrame = asset;
            });
        });
    }
}
```

### Preloading Bundles

```typescript
// Preload bundle (don't load into memory yet)
assetManager.loadBundle('level2', (err, bundle) => {
    if (err) {
        console.error('Bundle preload failed:', err);
        return;
    }

    // Now can load assets from bundle
    bundle.preload('textures/background', SpriteFrame);
});
```

### Releasing Bundles

```typescript
// Get loaded bundle
const bundle = assetManager.getBundle('level1');

// Release specific asset
bundle.release('textures/player', SpriteFrame);

// Release entire bundle
assetManager.releaseBundle('level1');
```

## Memory Management

### Asset Dependencies

When you load an asset, its dependencies are also loaded:

```typescript
// Loading prefab also loads:
// - Textures referenced by sprites
// - Materials referenced by models
// - Other prefabs referenced
resources.load('prefabs/player', Prefab, (err, prefab) => {
    // All dependencies loaded
});
```

### Releasing Resources

```typescript
// Release single asset
const asset = this.getComponent(Sprite).spriteFrame;
assetManager.releaseAsset(asset);

// Release by path
resources.release('textures/player');

// Release directory
resources.releaseDir('textures/monsters');

// Release asset bundle
assetManager.releaseBundle('level1');
```

### Reference Counting

Assets are automatically managed with reference counting:

```typescript
// Load asset
resources.load('textures/player', SpriteFrame, (err, spriteFrame) => {
    // Reference count = 1

    // Assign to component
    this.getComponent(Sprite).spriteFrame = spriteFrame;
    // Reference count = 2

    // Remove component
    this.node.removeComponent(Sprite);
    // Reference count = 1

    // Release asset
    assetManager.releaseAsset(spriteFrame);
    // Reference count = 0, asset freed
});
```

### Manual Memory Management

```typescript
@ccclass('ResourceManager')
export class ResourceManager extends Component {
    private loadedAssets: Set<Asset> = new Set();

    loadAsset(path: string, type: typeof Asset) {
        resources.load(path, type, (err, asset) => {
            if (err) {
                console.error('Load failed:', err);
                return;
            }

            // Track asset
            this.loadedAssets.add(asset);
        });
    }

    releaseAll() {
        this.loadedAssets.forEach(asset => {
            assetManager.releaseAsset(asset);
        });
        this.loadedAssets.clear();
    }

    onDestroy() {
        this.releaseAll();
    }
}
```

## Caching

### Asset Cache

```typescript
// Cache is automatic for loaded assets

// Check if asset in cache
const cached = assetManager.assets.get('textures/player');

// Clear all caches
assetManager.assets.clear();

// Release and remove from cache
resources.release('textures/player');
```

### Preventing Caching

```typescript
// Load remote without cache
assetManager.loadRemote(
    'https://example.com/data.json',
    { cacheEnabled: false },
    (err, asset) => {
        // Asset not cached
    }
);
```

## Preloading Strategy

### Sequential Preloading

```typescript
@ccclass('PreloadManager')
export class PreloadManager extends Component {
    async preloadGameAssets() {
        try {
            // Preload textures
            await this.preloadDir('textures/enemies', SpriteFrame);
            await this.preloadDir('textures/ui', SpriteFrame);

            // Preload audio
            await this.preloadDir('audio/sfx', AudioClip);

            // Preload prefabs
            await this.preloadDir('prefabs/enemies', Prefab);

            console.log('All assets preloaded');
        } catch (err) {
            console.error('Preload failed:', err);
        }
    }

    preloadDir<T>(path: string, type: typeof Asset): Promise<void> {
        return new Promise((resolve, reject) => {
            resources.preloadDir(path, type, (err) => {
                if (err) {
                    reject(err);
                } else {
                    resolve();
                }
            });
        });
    }
}
```

### Progressive Preloading

```typescript
@ccclass('ProgressiveLoader')
export class ProgressiveLoader extends Component {
    loadWithProgress() {
        const assets = [
            { path: 'textures/bg1', type: SpriteFrame },
            { path: 'textures/bg2', type: SpriteFrame },
            { path: 'textures/bg3', type: SpriteFrame },
        ];

        let loaded = 0;
        const total = assets.length;

        assets.forEach(asset => {
            resources.load(asset.path, asset.type, (err) => {
                if (err) {
                    console.error('Load failed:', asset.path, err);
                }

                loaded++;
                const progress = (loaded / total) * 100;
                this.updateProgress(progress);

                if (loaded === total) {
                    console.log('All loaded');
                }
            });
        });
    }

    updateProgress(percent: number) {
        // Update UI progress bar
    }
}
```

## Best Practices

1. **Release unused assets** to prevent memory leaks
2. **Use Asset Bundles** for large games to reduce initial load time
3. **Preload critical assets** before they're needed
4. **Cache remote assets** locally when possible
5. **Pool frequently used assets** instead of reloading
6. **Monitor memory usage** with profiler tools
7. **Use object pooling** for frequently created/destroyed objects
8. **Release bundle** when switching levels/game modes

## Memory Profiling

```typescript
@ccclass('MemoryMonitor')
export class MemoryMonitor extends Component {
    update() {
        if (DEBUG_MODE) {
            // Log memory usage (if supported)
            const info = assetManager.assets.get('memory_info');
            if (info) {
                console.log('Asset count:', assetManager.assets.count);
            }
        }
    }
}
```

## Common Patterns

### Asset Pool

```typescript
@ccclass('AssetPool')
export class AssetPool extends Component {
    private pool: Map<string, Asset[]> = new Map();

    getAsset(path: string, type: typeof Asset): Promise<Asset> {
        return new Promise((resolve, reject) => {
            const key = `${path}_${type.name}`;

            // Check pool
            if (this.pool.has(key) && this.pool.get(key).length > 0) {
                const asset = this.pool.get(key).pop();
                resolve(asset);
                return;
            }

            // Load new
            resources.load(path, type, (err, asset) => {
                if (err) {
                    reject(err);
                } else {
                    resolve(asset);
                }
            });
        });
    }

    returnAsset(path: string, type: typeof Asset, asset: Asset) {
        const key = `${path}_${type.name}`;
        if (!this.pool.has(key)) {
            this.pool.set(key, []);
        }
        this.pool.get(key).push(asset);
    }
}
```

### Lazy Loading

```typescript
@ccclass('LazyLoader')
export class LazyLoader extends Component {
    private loaded: boolean = false;

    async ensureLoaded() {
        if (this.loaded) return;

        try {
            await this.loadAsset('textures/heavy', SpriteFrame);
            this.loaded = true;
        } catch (err) {
            console.error('Load failed:', err);
        }
    }

    onEnable() {
        this.ensureLoaded();
    }
}
```

## Troubleshooting

### Asset Not Releasing

```typescript
// PROBLEM: Asset still in memory after release
assetManager.releaseAsset(asset);

// SOLUTION: Check for dependencies
const deps = assetManager.dependUtil.getDeps(asset.id);
deps.forEach(dep => {
    assetManager.releaseAsset(dep);
});
```

### Memory Leak

```typescript
// PROBLEM: Memory keeps increasing
resources.load('texture', SpriteFrame, (err, asset) => {
    this.getComponent(Sprite).spriteFrame = asset;
    // Asset reference held by component
});

// SOLUTION: Release when done
onDestroy() {
    const sprite = this.getComponent(Sprite);
    if (sprite && sprite.spriteFrame) {
        assetManager.releaseAsset(sprite.spriteFrame);
        sprite.spriteFrame = null;
    }
}
```

### Bundle Load Fails

```typescript
// PROBLEM: Bundle not found
assetManager.loadBundle('my-bundle', callback);

// SOLUTION: Verify bundle name and path
// Check bundle is configured in Project Settings
console.log('Available bundles:', assetManager.bundles.keys);
```
