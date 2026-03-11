# Phaser Installation Guide

## 🎯 Overview

This guide covers the installation and setup of Phaser JS for web game development within the OpenAgenticGame architecture. Phaser is a fast, free, and fun open source HTML5 game framework for Canvas and WebGL.

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

## 📦 Requirements

### **System Requirements**
- **Node.js**: Version 14.0 or higher
- **npm**: Version 6.0 or higher
- **Web Browser**: Modern browser with WebGL support
- **Text Editor**: Code editor with JavaScript support

### **Recommended Browsers**
- **Chrome**: Version 60+
- **Firefox**: Version 55+
- **Safari**: Version 12+
- **Edge**: Version 79+
- **Opera**: Version 47+

### **Optional Tools**
- **Phaser Editor**: Visual game editor (optional)
- **Local Server**: For development testing
- **Git**: Version control (recommended)

## 🚀 **Installation Methods**

### **Method 1: npm (Recommended)**
```bash
# Create new project directory
mkdir my-phaser-game
cd my-phaser-game

# Initialize npm project
npm init -y

# Install Phaser
npm install phaser@latest

# Install additional dependencies
npm install @types/phaser --save-dev
```

### **Method 2: CDN**
```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdn.jsdelivr.net/npm/phaser@3.60.0/dist/phaser.min.js"></script>
</head>
<body>
    <script src="src/game.js"></script>
</body>
</html>
```

### **Method 3: Download**
```bash
# Download Phaser
curl -O phaser.zip https://github.com/photonstorm/phaser/releases/download/v3.60.0/phaser.zip

# Extract
unzip phaser.zip
```

## 🔧 **Project Setup**

### **Basic Project Structure**
```
my-phaser-game/
├── src/
│   ├── scenes/
│   │   ├── PreloadScene.js
│   │   ├── MenuScene.js
│   │   └── GameScene.js
│   ├── entities/
│   │   ├── Player.js
│   │   ├── Enemy.js
│   │   └── Bullet.js
│   ├── systems/
│   │   ├── SpawnSystem.js
│   │   ├── CollisionSystem.js
│   │   └── ScoreSystem.js
│   └── utils/
│       ├── ObjectPool.js
│       └── PerformanceMonitor.js
├── assets/
│   ├── images/
│   │   ├── player.png
│   │   ├── enemy.png
│   │   └── bullet.png
│   ├── audio/
│   │   ├── shoot.mp3
│   │   ├── explosion.mp3
│   │   └── background-music.mp3
│   └── fonts/
│       └── arcade-font.png
├── index.html
├── package.json
└── README.md
```

### **package.json Configuration**
```json
{
  "name": "my-phaser-game",
  "version": "1.0.0",
  "description": "A Phaser web game",
  "main": "src/main.js",
  "scripts": {
    "dev": "webpack serve --mode development",
    "build": "webpack --mode production",
    "start": "node server.js",
    "test": "jest"
  },
  "dependencies": {
    "phaser": "^3.60.0"
  },
  "devDependencies": {
    "@types/phaser": "^3.60.0",
    "webpack": "^5.75.0",
    "webpack-cli": "^5.1.4",
    "typescript": "^4.9.5",
    "jest": "^29.7.0"
  }
}
```

### **Webpack Configuration (webpack.config.js)**
```javascript
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
          }
        }
      },
      {
        test: /\.(png|jpg|gif|svg|mp3|wav)$/,
        type: 'asset/resource'
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.json']
  },
  devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    port: 3000
  },
  devtool: 'source-map'
};
```

## 🔧 **Development Setup**

### **Local Development Server**
```javascript
// server.js
const express = require('express');
const path = require('path');

const app = express();
const port = process.env.PORT || 3000;

// Serve static files
app.use(express.static(path.join(__dirname, 'dist')));

// SPA fallback
app.get('*', (req, res) => {
    res.sendFile(path.join(__dirname, 'dist', 'index.html'));
});

app.listen(port, () => {
    console.log(`Development server running on port ${port}`);
});
```

### **Development Scripts**
```json
"scripts": {
    "dev": "webpack serve --mode development --watch",
    "build": "webpack --mode production",
    "start": "node server.js",
    "clean": "rm -rf dist",
    "test": "jest",
    "lint": "eslint src/**/*.js"
}
```

## 🌐 **IDE Setup**

### **VS Code**
```json
{
  "recommendations": [
    "ms-vscode.typescript-javascript",
    "phaser-vscode",
    "es6-string-html"
  ],
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

### **WebStorm**
```xml
<component name="JavaScript">
  <option name="ES6 JavaScript">
    <option name="JSX">
      <option name="JSX Harmony">
        <option name="ECMAScript 6">
          <option name="ECMAScript 2015+">
            <option name="Node.js">
              <option name="React JSX">
                <option name="Vue Template">
                  <option name="Angular Template">
        </option>
      </option>
```

### **Sublime Text**
```json
{
  "prefered": {
    "syntaxes": [
      "javascript",
      "typescript"
    ]
  }
}
```

## 📱 **Asset Management**

### **Asset Organization**
```
assets/
├── images/
│   ├── sprites/
│   │   ├── player/
│   │   │   ├── idle.png
│   │   │   ├── walk/
│   │   │   └── attack/
│   │   └── ui/
│   │       ├── button.png
│   │       ├── panel.png
│   │       └── icon.png
│   ├── backgrounds/
│   │   ├── space-bg.png
│   │   ├── stars-bg.png
│   │   └── nebula-bg.png
│   └── audio/
│       ├── sfx/
│       │   ├── shoot.mp3
│       │   ├── explosion.mp3
│       │   └── powerup.mp3
│       └── music/
│           ├── background-music.mp3
│           ├── menu-music.mp3
│           └── game-over-music.mp3
```

### **Asset Loading**
```javascript
// Preload Scene
export class PreloadScene extends Scene {
    constructor() {
        super({ key: 'PreloadScene' });
    }

    preload() {
        // Load images
        this.load.image('player', 'assets/images/sprites/player/idle.png');
        this.load.spritesheet('player-walk', 'assets/images/sprites/player/walk.png', {
            frameWidth: 64,
            frameHeight: 64
        });
        
        // Load audio
        this.load.audio('shoot', 'assets/audio/sfx/shoot.mp3');
        this.load.audio('background-music', 'assets/audio/music/background-music.mp3');
        
        // Load JSON data
        this.load.json('game-config', 'assets/data/game-config.json');
        
        // Create loading screen
        this.createLoadingScreen();
    }
    
    create() {
        // Start game when loading is complete
        this.scene.start('MenuScene');
    }
}
```

## 🔧 **Configuration**

### **Game Configuration**
```javascript
// config.js
export const gameConfig = {
    // Game settings
    playerSpeed: 5,
    enemySpeed: 2,
    bulletSpeed: 10,
    maxEnemies: 10,
    spawnRate: 2000,
    
    // Display settings
    gameWidth: 800,
    gameHeight: 600,
    pixelArt: true,
    antialias: false,
    
    // Physics settings
    gravity: { y: 0 },
    bounce: 0.1,
    debug: false,
    
    // Audio settings
    musicVolume: 0.3,
    sfxVolume: 0.5,
    mute: false
};
```

### **Environment Variables**
```bash
# Development
export NODE_ENV=development
export API_URL=http://localhost:3000

# Production
export NODE_ENV=production
export API_URL=https://api.example.com
```

## 🧪 **Testing Setup**

### **Jest Configuration**
```javascript
// jest.config.js
module.exports = {
    testEnvironment: 'node',
    testMatch: [
        '/tests/.*\\.test\\.js$'
    ],
    collectCoverageFrom: 'coverage',
    coverageDirectory: 'coverage',
    coverageReporters: ['text', 'html', 'lcov'],
    coverageThreshold: {
        global: {
            branches: 80,
            functions: 80,
            lines: 80
        }
    }
};
```

### **Test Example**
```javascript
// tests/Player.test.js
import { Player } from '../src/entities/Player';

describe('Player', () => {
    let player;
    
    beforeEach(() => {
        const scene = new TestScene();
        player = new Player(scene, 100, 100);
    });
    
    test('should initialize with correct health', () => {
        expect(player.health).toBe(100);
    });
    
    test('should move at correct speed', () => {
        player.speed = 5;
        player.update(1, 16);
        expect(player.y).toBe(116); // 100 + 5 * 16
    });
    
    test('should take damage correctly', () => {
        player.takeDamage(25);
        expect(player.health).toBe(75);
    });
});
```

## 🔧 **Build Process**

### **Development Build**
```bash
# Start development server
npm run dev

# Watch for changes
npm run dev --watch
```

### **Production Build**
```bash
# Build for production
npm run build

# Optimize build
npm run build --optimize
```

### **Deployment**
```bash
# Deploy to GitHub Pages
npm run deploy:gh-pages

# Deploy to Netlify
npm run deploy:netlify

# Deploy to Vercel
npm run deploy:vercel
```

## 🛠️ **Troubleshooting**

### **Common Installation Issues**

#### **Module Not Found**
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules
rm -rf node_modules

# Reinstall dependencies
npm install
```

#### **Permission Denied**
```bash
# Use sudo (Linux/MacOS)
sudo npm install

# Or use npx
npx phaser create my-game
```

#### **Network Issues**
```bash
# Use different registry
npm config set registry https://registry.npmjs.org

# Use proxy if needed
npm config set proxy http://proxy.example.com
```

### **Development Issues**

#### **Game Won't Load**
```javascript
// Check console for errors
console.log('Game initialization error:', error);

// Verify Phaser version
console.log('Phaser version:', Phaser.VERSION);
```

#### **Assets Not Loading**
```javascript
// Check asset paths
console.log('Asset path:', this.load.path);

// Verify file exists
if (!this.textures.exists('player')) {
    console.error('Player asset not found');
}
```

#### **Performance Issues**
```javascript
// Monitor performance
const fps = this.game.loop.actualFps;
console.log('FPS:', fps);

// Monitor memory
const memory = this.performance.memory.used;
console.log('Memory usage:', memory);
```

### **Browser Compatibility**

#### **WebGL Not Supported**
```javascript
// Check WebGL support
const canvas = document.createElement('canvas');
const gl = canvas.getContext('webgl') || canvas.getContext('experimental-webgl');
const webGLSupported = !!gl;

if (!webGLSupported) {
    console.warn('WebGL not supported, falling back to Canvas');
    this.config.type = Phaser.CANVAS;
}
```

#### **Audio Not Playing**
```javascript
// Check audio context
const AudioContext = window.AudioContext || window.webkitAudioContext;
const audioSupported = !!AudioContext;

if (!audioSupported) {
    console.warn('Web Audio API not supported');
    this.sound.setMute(true);
}
```

## 📚 **Version Management**

### **Update Phaser**
```bash
# Update to latest version
npm update phaser@latest

# Update specific version
npm install phaser@3.60.1
```

### **Version Compatibility**
- **Phaser 3.60+**: Latest features and improvements
- **Phaser 3.55**: Stable version with full feature set
- **Phaser 3.50**: Long-term support version
- **Phaser 2.x**: Legacy version (not recommended)

### **Breaking Changes**
- **Phaser 3.60**: New animation system
- **Phaser 3.55**: Improved TypeScript support
- **Phaser 3.50**: Enhanced input system
- **Phaser 3.0**: Complete rewrite from Phaser 2

## 📊 **Performance Tips**

### **Rendering Optimization**
```javascript
// Use WebGL for better performance
const config = {
    type: Phaser.WEBGL,
    render: {
        pixelArt: true,
        antialias: false
    }
};

// Batch rendering
const batch = this.add.graphics();
batch.beginFill(0, 0, 100, 100);
batch.endFill();
```

### **Memory Management**
```javascript
// Object pooling
class BulletPool extends Phaser.GameObjects.Group {
    constructor(scene) {
        super(scene);
        this.pool = [];
        this.maxSize = 100;
    }
    
    get(x, y) {
        if (this.pool.length > 0) {
            const bullet = this.pool.pop();
            bullet.reset(x, y);
            return bullet;
        }
        
        return this.create(x, y);
    }
    
    release(bullet) {
        if (this.pool.length < this.maxSize) {
            this.pool.push(bullet);
        } else {
            bullet.destroy();
        }
    }
}
```

### **Asset Optimization**
```javascript
// Use sprite sheets
this.load.spritesheet('player', 'assets/images/player.png', {
    frameWidth: 64,
    frameHeight: 64
});

// Compress images
// Use tools like TinyPNG or Squoosh
```

---

## 🎯 **Getting Help**

### **Official Resources**
- **Website**: https://phaser.io/
- **Documentation**: https://phaser.io/learn/
- **Examples**: https://phaser.io/examples/
- **API Reference**: https://phaser.io/docs/

### **Community Support**
- **Forum**: https://phaser.io/community/
- **Discord**: https://discord.gg/phaser
- **GitHub**: https://github.com/photonstorm/phaser

### **Learning Resources**
- **Tutorials**: https://phaser.io/tutorials/
- **Videos**: https://phaser.io/learn/
- **Books**: Available on Amazon and other platforms
- **Courses**: Various online courses available

---

*Phaser Installation Guide*
*Version: 3.60+*
*Last Updated: 2026-03-10*
*Team: Programming Team*
*Specialist: cocos-creator-specialist*
*Platform: Web*
