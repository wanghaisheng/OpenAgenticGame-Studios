# Phaser Deployment Guide

## 🎯 Overview

This guide covers the deployment strategies and best practices for Phaser JS games within the OpenAgenticGame architecture. Proper deployment ensures your game runs smoothly across different platforms and reaches the widest possible audience.

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

## 🌐 **Deployment Platforms**

### **Static Site Hosting**
- **GitHub Pages**: Free static hosting
- **Netlify**: Automated deployment
- **Vercel**: High-performance hosting
- **Firebase Hosting**: Google platform
- **Surge.sh**: Simple static hosting

### **Game Distribution**
- **itch.io**: Indie game platform
- **Newgrounds**: Flash game community
- **Kongregate**: Web game platform
- **Armor Games**: Game portal
- **CrazyGames**: Browser games

### **Mobile Web**
- **Progressive Web App**: PWA deployment
- **Mobile Browsers**: Mobile optimization
- **App Stores**: Web-to-app conversion
- **Social Platforms**: Facebook Instant Games

## 📦 **Build Process**

### **Development Build**
```javascript
// Development Configuration
const devConfig = {
    mode: 'development',
    devtool: 'source-map',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist'),
        publicPath: '/'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: 'babel-loader'
            },
            {
                test: /\.(png|jpg|gif|svg)$/,
                type: 'asset/resource'
            }
        ]
    },
    devServer: {
        contentBase: path.join(__dirname, 'dist'),
        compress: true,
        port: 3000,
        hot: true
    }
};
```

### **Production Build**
```javascript
// Production Configuration
const prodConfig = {
    mode: 'production',
    output: {
        filename: 'bundle.[contenthash].js',
        path: path.resolve(__dirname, 'dist'),
        publicPath: '/'
    },
    optimization: {
        minimizer: [
            new TerserPlugin({
                terserOptions: {
                    compress: {
                        drop_console: true
                    }
                }
            })
        ],
        splitChunks: {
            chunks: 'all',
            cacheGroups: {
                vendor: {
                    test: /[\\/]node_modules[\\/]/,
                    name: 'vendors',
                    chunks: 'all'
                }
            }
        }
    },
    plugins: [
        new CleanWebpackPlugin(),
        new HtmlWebpackPlugin({
            template: './src/index.html',
            minify: {
                removeComments: true,
                collapseWhitespace: true,
                removeRedundantAttributes: true,
                useShortDoctype: true,
                removeEmptyAttributes: true,
                removeStyleLinkTypeAttributes: true,
                keepClosingSlash: true,
                minifyJS: true,
                minifyCSS: true,
                minifyURLs: true
            }
        })
    ]
};
```

### **Asset Optimization**
```javascript
// Asset Pipeline
const AssetPipeline = {
    optimizeImages: (imageFiles) => {
        return imageFiles.map(file => {
            return {
                input: file,
                output: file.replace(/\.(png|jpg|jpeg)$/, '.webp'),
                plugins: [
                    imageminWebp({ quality: 80 })
                ]
            };
        });
    },
    
    optimizeAudio: (audioFiles) => {
        return audioFiles.map(file => {
            return {
                input: file,
                output: file.replace(/\.(mp3|wav)$/, '.ogg'),
                plugins: [
                    imageminGifsicle({ optimizationLevel: 3 })
                ]
            };
        });
    },
    
    createSpriteSheets: (imageFiles) => {
        // Create optimized sprite sheets
        return TexturePacker.create({
            files: imageFiles,
            output: 'assets/spritesheets',
            format: 'json',
            padding: 2,
            maxSheetSize: 4096
        });
    }
};
```

## 🚀 **Deployment Scripts**

### **Package.json Scripts**
```json
{
  "scripts": {
    "dev": "webpack serve --mode development",
    "build": "webpack --mode production",
    "build:analyze": "webpack-bundle-analyzer dist/bundle.js",
    "deploy:gh-pages": "gh-pages -d dist",
    "deploy:netlify": "netlify deploy --prod --dir dist",
    "deploy:vercel": "vercel --prod",
    "deploy:firebase": "firebase deploy",
    "test": "jest",
    "test:e2e": "cypress run",
    "lint": "eslint src/**/*.js",
    "format": "prettier --write src/**/*.js"
  }
}
```

### **GitHub Actions CI/CD**
```yaml
# .github/workflows/deploy.yml
name: Deploy Game

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '16'
    - name: Install dependencies
      run: npm ci
    - name: Run tests
      run: npm test
    - name: Run E2E tests
      run: npm run test:e2e

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '16'
    - name: Install dependencies
      run: npm ci
    - name: Build game
      run: npm run build
    - name: Upload build artifacts
      uses: actions/upload-artifact@v2
      with:
        name: dist
        path: dist/

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
    - name: Download build artifacts
      uses: actions/download-artifact@v2
      with:
        name: dist
        path: dist/
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

### **Netlify Deployment**
```toml
# netlify.toml
[build]
  publish = "dist"
  command = "npm run build"

[build.environment]
  NODE_VERSION = "16"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"

[[headers]]
  for = "*.js"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "*.css"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "*.png"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "*.webp"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "*.mp3"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/:splat"
  status = 200
```

## 📱 **Progressive Web App (PWA)**

### **Service Worker**
```javascript
// sw.js
const CACHE_NAME = 'phaser-game-v1';
const urlsToCache = [
    '/',
    '/index.html',
    '/bundle.js',
    '/assets/',
    '/manifest.json'
];

self.addEventListener('install', event => {
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then(cache => cache.addAll(urlsToCache))
    );
});

self.addEventListener('fetch', event => {
    event.respondWith(
        caches.match(event.request)
            .then(response => {
                // Cache hit - return response
                if (response) {
                    return response;
                }

                // Network request
                return fetch(event.request).then(response => {
                    // Check if valid response
                    if (!response || response.status !== 200 || response.type !== 'basic') {
                        return response;
                    }

                    // Clone response
                    const responseToCache = response.clone();

                    caches.open(CACHE_NAME)
                        .then(cache => {
                            cache.put(event.request, responseToCache);
                        });

                    return response;
                });
            })
    );
});

self.addEventListener('activate', event => {
    event.waitUntil(
        caches.keys().then(cacheNames => {
            return Promise.all(
                cacheNames.map(cacheName => {
                    if (cacheName !== CACHE_NAME) {
                        return caches.delete(cacheName);
                    }
                })
            );
        })
    );
});
```

### **Web App Manifest**
```json
{
  "name": "Space Shooter Game",
  "short_name": "SpaceShooter",
  "description": "Exciting space shooter arcade game",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#00ff00",
  "orientation": "landscape",
  "scope": "/",
  "icons": [
    {
      "src": "icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "icons/icon-96x96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "icons/icon-128x128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "icons/icon-144x144.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "icons/icon-152x152.png",
      "sizes": "152x152",
      "type": "image/png"
    },
    {
      "src": "icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icons/icon-384x384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      "src": "icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ],
  "splash_pages": null
}
```

### **PWA Integration**
```javascript
// PWA Manager
class PWAManager {
    constructor() {
        this.deferredPrompt = null;
        this.installButton = null;
        this.setupEventListeners();
    }

    setupEventListeners() {
        // Before install prompt
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            this.deferredPrompt = e;
            this.showInstallButton();
        });

        // App installed
        window.addEventListener('appinstalled', () => {
            this.deferredPrompt = null;
            this.hideInstallButton();
        });

        // Service worker registration
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/sw.js')
                .then(registration => {
                    console.log('SW registered: ', registration);
                })
                .catch(registrationError => {
                    console.log('SW registration failed: ', registrationError);
                });
        }
    }

    showInstallButton() {
        if (!this.installButton) {
            this.installButton = document.createElement('button');
            this.installButton.textContent = 'Install App';
            this.installButton.className = 'install-button';
            this.installButton.addEventListener('click', () => {
                this.installApp();
            });
            document.body.appendChild(this.installButton);
        }
    }

    hideInstallButton() {
        if (this.installButton) {
            this.installButton.remove();
            this.installButton = null;
        }
    }

    installApp() {
        if (this.deferredPrompt) {
            this.deferredPrompt.prompt();
            this.deferredPrompt.userChoice.then((choiceResult) => {
                if (choiceResult.outcome === 'accepted') {
                    console.log('User accepted the install prompt');
                } else {
                    console.log('User dismissed the install prompt');
                }
                this.deferredPrompt = null;
            });
        }
    }
}
```

## 🎮 **Game Platform Deployment**

### **itch.io Deployment**
```javascript
// itch.io Exporter
class ItchExporter {
    constructor() {
        this.platform = 'itch.io';
        this.config = {
            name: 'Space Shooter',
            author: 'OpenAgenticGame',
            description: 'Exciting space shooter game',
            tags: ['shooter', 'space', 'arcade'],
            genre: 'Shooter',
            platform: 'HTML5'
        };
    }

    export() {
        return {
            files: this.getGameFiles(),
            metadata: this.config,
            butler: this.generateButlerConfig()
        };
    }

    getGameFiles() {
        return [
            'index.html',
            'bundle.js',
            'assets/',
            'manifest.json',
            'sw.js'
        ];
    }

    generateButlerConfig() {
        return {
            'itchio': {
                'game': {
                    'name': this.config.name,
                    'description': this.config.description,
                    'genre': this.config.genre,
                    'tags': this.config.tags,
                    'platforms': ['HTML5']
                }
            }
        };
    }
}
```

### **Kongregate Deployment**
```javascript
// Kongregate Integration
class KongregateIntegration {
    constructor() {
        this.api = null;
        this.userId = null;
        this.gameAuthToken = null;
    }

    init() {
        if (typeof kongregateAPI !== 'undefined') {
            kongregateAPI.loadAPI(() => {
                this.api = kongregateAPI.getAPI();
                this.userId = this.api.services.getUserId();
                this.gameAuthToken = this.api.services.getGameAuthToken();
                
                console.log('Kongregate API loaded');
                this.setupEventHandlers();
            });
        }
    }

    setupEventHandlers() {
        // Submit score
        this.api.stats.submit('high_score', this.getHighScore());
        
        // Submit achievements
        this.api.stats.submit('games_played', 1);
        
        // Handle ads
        this.api.ads.displayAd();
    }

    submitScore(score) {
        if (this.api) {
            this.api.stats.submit('high_score', score);
        }
    }

    submitAchievement(achievement) {
        if (this.api) {
            this.api.stats.submit(achievement, 1);
        }
    }

    showAd() {
        if (this.api) {
            this.api.ads.displayAd();
        }
    }
}
```

## 📊 **Analytics Integration**

### **Google Analytics**
```javascript
// Analytics Manager
class AnalyticsManager {
    constructor() {
        this.trackingId = 'GA_MEASUREMENT_ID';
        this.config = {
            send_page_view: false,
            debug_mode: false
        };
        this.init();
    }

    init() {
        // Load Google Analytics
        const script = document.createElement('script');
        script.src = `https://www.googletagmanager.com/gtag/js?id=${this.trackingId}`;
        script.async = true;
        document.head.appendChild(script);

        // Initialize gtag
        window.dataLayer = window.dataLayer || [];
        window.gtag = function() {
            dataLayer.push(arguments);
        };
        
        gtag('js', new Date());
        gtag('config', this.trackingId, this.config);
        
        this.trackGameStart();
    }

    trackGameStart() {
        gtag('event', 'game_start', {
            event_category: 'engagement',
            event_label: 'game_session'
        });
    }

    trackGameEnd(score, timePlayed) {
        gtag('event', 'game_end', {
            event_category: 'engagement',
            event_label: 'game_session',
            value: score,
            custom_parameter: timePlayed
        });
    }

    trackLevelComplete(level, time) {
        gtag('event', 'level_complete', {
            event_category: 'engagement',
            event_label: `level_${level}`,
            custom_parameter: time
        });
    }

    trackPurchase(item, price) {
        gtag('event', 'purchase', {
            event_category: 'monetization',
            event_label: item,
            value: price
        });
    }

    trackError(error, context) {
        gtag('event', 'error', {
            event_category: 'error',
            event_label: context,
            custom_parameter: error.message
        });
    }
}
```

### **Custom Analytics**
```javascript
// Custom Analytics
class CustomAnalytics {
    constructor() {
        this.events = [];
        this.sessionStart = Date.now();
        this.sessionData = {
            userAgent: navigator.userAgent,
            platform: navigator.platform,
            language: navigator.language,
            screenResolution: `${screen.width}x${screen.height}`,
            viewportSize: `${window.innerWidth}x${window.innerHeight}`
        };
    }

    trackEvent(eventName, data) {
        const event = {
            name: eventName,
            data: data,
            timestamp: Date.now(),
            sessionTime: Date.now() - this.sessionStart,
            sessionId: this.getSessionId()
        };
        
        this.events.push(event);
        this.sendEvent(event);
    }

    getSessionId() {
        let sessionId = localStorage.getItem('game_session_id');
        if (!sessionId) {
            sessionId = this.generateSessionId();
            localStorage.setItem('game_session_id', sessionId);
        }
        return sessionId;
    }

    generateSessionId() {
        return 'session_' + Math.random().toString(36).substr(2, 9);
    }

    sendEvent(event) {
        // Send to analytics endpoint
        fetch('/api/analytics', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                event: event,
                session: this.sessionData
            })
        }).catch(error => {
            console.error('Analytics error:', error);
        });
    }

    getAnalyticsData() {
        return {
            events: this.events,
            session: this.sessionData,
            sessionDuration: Date.now() - this.sessionStart
        };
    }
}
```

## 🔧 **Environment Configuration**

### **Environment Variables**
```javascript
// Environment Config
class EnvironmentConfig {
    constructor() {
        this.config = this.loadConfig();
    }

    loadConfig() {
        const env = process.env.NODE_ENV || 'development';
        
        const configs = {
            development: {
                apiUrl: 'http://localhost:3000/api',
                analyticsEnabled: false,
                debugMode: true,
                logLevel: 'debug'
            },
            staging: {
                apiUrl: 'https://staging.example.com/api',
                analyticsEnabled: true,
                debugMode: true,
                logLevel: 'info'
            },
            production: {
                apiUrl: 'https://api.example.com',
                analyticsEnabled: true,
                debugMode: false,
                logLevel: 'error'
            }
        };
        
        return configs[env] || configs.development;
    }

    get(key) {
        return this.config[key];
    }

    isDevelopment() {
        return process.env.NODE_ENV === 'development';
    }

    isProduction() {
        return process.env.NODE_ENV === 'production';
    }
}
```

### **Feature Flags**
```javascript
// Feature Flags Manager
class FeatureFlags {
    constructor() {
        this.flags = this.loadFlags();
    }

    loadFlags() {
        return {
            enableAnalytics: true,
            enableAds: false,
            enablePWA: true,
            enableMultiplayer: false,
            enableLeaderboards: true,
            enableAchievements: true,
            enableInAppPurchases: false,
            enableSocialSharing: true
        };
    }

    isEnabled(flag) {
        return this.flags[flag] || false;
    }

    enable(flag) {
        this.flags[flag] = true;
    }

    disable(flag) {
        this.flags[flag] = false;
    }

    updateFlags(newFlags) {
        Object.assign(this.flags, newFlags);
    }
}
```

## 📱 **Mobile Optimization**

### **Mobile Detection**
```javascript
// Mobile Detector
class MobileDetector {
    constructor() {
        this.isMobile = this.detectMobile();
        this.isTablet = this.detectTablet();
        this.isDesktop = !this.isMobile && !this.isTablet;
        this.deviceInfo = this.getDeviceInfo();
    }

    detectMobile() {
        return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
    }

    detectTablet() {
        return /iPad|Android(?!.*Mobile)/i.test(navigator.userAgent);
    }

    getDeviceInfo() {
        return {
            userAgent: navigator.userAgent,
            platform: navigator.platform,
            vendor: navigator.vendor,
            language: navigator.language,
            cookieEnabled: navigator.cookieEnabled,
            onLine: navigator.onLine,
            screen: {
                width: screen.width,
                height: screen.height,
                colorDepth: screen.colorDepth,
                pixelDepth: screen.pixelDepth
            },
            viewport: {
                width: window.innerWidth,
                height: window.innerHeight
            },
            deviceMemory: navigator.deviceMemory || 4,
            hardwareConcurrency: navigator.hardwareConcurrency || 4,
            connection: navigator.connection || {
                effectiveType: '4g',
                downlink: 10,
                rtt: 50
            }
        };
    }

    getOptimizedConfig() {
        const config = {
            pixelArt: true,
            antialias: false,
            fps: 60,
            physicsFps: 60
        };

        if (this.isMobile) {
            config.fps = 30;
            config.physicsFps = 30;
            config.pixelArt = true;
            config.antialias = false;
        }

        if (this.deviceInfo.deviceMemory < 4) {
            config.fps = 30;
            config.physicsFps = 30;
        }

        return config;
    }
}
```

### **Touch Controls**
```javascript
// Touch Controls Manager
class TouchControlsManager {
    constructor(scene) {
        this.scene = scene;
        this.touchArea = null;
        this.controls = {
            left: false,
            right: false,
            up: false,
            down: false,
            action: false
        };
        this.setupTouchControls();
    }

    setupTouchControls() {
        // Create touch area
        this.touchArea = this.scene.add.rectangle(0, 0, this.scene.cameras.main.width, this.scene.cameras.main.height);
        this.touchArea.setInteractive();
        this.touchArea.setAlpha(0);
        
        // Touch events
        this.touchArea.on('pointerdown', this.handleTouchStart, this);
        this.touchArea.on('pointerup', this.handleTouchEnd, this);
        this.touchArea.on('pointermove', this.handleTouchMove, this);
        
        // Create visual controls
        this.createVisualControls();
    }

    createVisualControls() {
        const { width, height } = this.scene.cameras.main;
        
        // D-pad
        this.dPad = this.scene.add.container(width * 0.15, height * 0.7);
        
        const dpadBg = this.scene.add.circle(0, 0, 60, 0x333366, 0.5);
        this.dPad.add(dpadBg);
        
        // D-pad buttons
        this.dPadButtons = {
            up: this.scene.add.rectangle(0, -40, 30, 30, 0x555577),
            down: this.scene.add.rectangle(0, 40, 30, 30, 0x555577),
            left: this.scene.add.rectangle(-40, 0, 30, 30, 0x555577),
            right: this.scene.add.rectangle(40, 0, 30, 30, 0x555577)
        };
        
        Object.values(this.dPadButtons).forEach(button => {
            button.setInteractive();
            this.dPad.add(button);
        });
        
        // Action button
        this.actionButton = this.scene.add.circle(width * 0.85, height * 0.7, 40, 0x555577, 0.5);
        this.actionButton.setInteractive();
        this.scene.add.existing(this.actionButton);
    }

    handleTouchStart(pointer) {
        const { width, height } = this.scene.cameras.main;
        const x = pointer.x;
        const y = pointer.y;
        
        // Check D-pad
        if (x < width * 0.3 && y > height * 0.5) {
            this.handleDPadTouch(x, y, true);
        }
        
        // Check action button
        if (x > width * 0.7 && y > height * 0.5) {
            this.controls.action = true;
            this.actionButton.setTint(0x7777aa);
        }
    }

    handleTouchEnd(pointer) {
        this.resetControls();
    }

    handleTouchMove(pointer) {
        const { width, height } = this.scene.cameras.main;
        const x = pointer.x;
        const y = pointer.y;
        
        if (x < width * 0.3 && y > height * 0.5) {
            this.handleDPadTouch(x, y, true);
        }
    }

    handleDPadTouch(x, y, active) {
        const { width, height } = this.scene.cameras.main;
        const centerX = width * 0.15;
        const centerY = height * 0.7;
        
        const dx = x - centerX;
        const dy = y - centerY;
        
        // Reset controls
        this.controls.left = false;
        this.controls.right = false;
        this.controls.up = false;
        this.controls.down = false;
        
        // Determine direction
        if (Math.abs(dx) > Math.abs(dy)) {
            if (dx > 20) {
                this.controls.right = true;
                this.dPadButtons.right.setTint(0x7777aa);
            } else if (dx < -20) {
                this.controls.left = true;
                this.dPadButtons.left.setTint(0x7777aa);
            }
        } else {
            if (dy > 20) {
                this.controls.down = true;
                this.dPadButtons.down.setTint(0x7777aa);
            } else if (dy < -20) {
                this.controls.up = true;
                this.dPadButtons.up.setTint(0x7777aa);
            }
        }
    }

    resetControls() {
        Object.keys(this.controls).forEach(key => {
            this.controls[key] = false;
        });
        
        // Reset visual states
        Object.values(this.dPadButtons).forEach(button => {
            button.clearTint();
        });
        
        this.actionButton.clearTint();
    }

    getControls() {
        return this.controls;
    }
}
```

## 🔧 **Testing and QA**

### **E2E Testing**
```javascript
// Cypress E2E Tests
describe('Game Deployment', () => {
    beforeEach(() => {
        cy.visit('/');
    });

    it('should load the game', () => {
        cy.get('#game-canvas').should('be.visible');
        cy.get('.loading-screen').should('not.exist');
    });

    it('should have responsive design', () => {
        cy.viewport(375, 667); // Mobile
        cy.get('#game-canvas').should('be.visible');
        
        cy.viewport(1920, 1080); // Desktop
        cy.get('#game-canvas').should('be.visible');
    });

    it('should handle touch controls', () => {
        cy.viewport(375, 667);
        cy.get('.touch-controls').should('be.visible');
        
        cy.get('.action-button').click();
        cy.get('.player').should('have.class', 'shooting');
    });

    it('should track analytics', () => {
        cy.window().then((win) => {
            cy.spy(win, 'gtag').as('gtag');
        });
        
        cy.get('.start-button').click();
        cy.get('@gtag').should('have.been.calledWith', 'event', 'game_start');
    });
});
```

### **Performance Testing**
```javascript
// Performance Tests
describe('Performance Tests', () => {
    it('should maintain 60 FPS', () => {
        cy.visit('/');
        
        cy.window().then((win) => {
            const fps = win.game.loop.actualFps;
            expect(fps).to.be.greaterThan(55);
        });
    });

    it('should load within 3 seconds', () => {
        cy.visit('/');
        cy.get('.loading-screen', { timeout: 3000 }).should('not.exist');
    });

    it('should use less than 100MB memory', () => {
        cy.window().then((win) => {
            if (win.performance && win.performance.memory) {
                const memory = win.performance.memory.usedJSHeapSize / 1024 / 1024;
                expect(memory).to.be.lessThan(100);
            }
        });
    });
});
```

## 📊 **Monitoring and Maintenance**

### **Error Tracking**
```javascript
// Error Tracking
class ErrorTracker {
    constructor() {
        this.errors = [];
        this.setupErrorHandlers();
    }

    setupErrorHandlers() {
        // Global error handler
        window.addEventListener('error', (event) => {
            this.logError({
                type: 'javascript',
                message: event.message,
                filename: event.filename,
                lineno: event.lineno,
                colno: event.colno,
                stack: event.error ? event.error.stack : null
            });
        });

        // Unhandled promise rejection
        window.addEventListener('unhandledrejection', (event) => {
            this.logError({
                type: 'promise',
                message: event.reason,
                stack: event.reason ? event.reason.stack : null
            });
        });
    }

    logError(error) {
        error.timestamp = Date.now();
        error.userAgent = navigator.userAgent;
        error.url = window.location.href;
        
        this.errors.push(error);
        this.sendError(error);
    }

    sendError(error) {
        fetch('/api/errors', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(error)
        }).catch(console.error);
    }

    getErrors() {
        return this.errors;
    }
}
```

### **Performance Monitoring**
```javascript
// Performance Monitor
class PerformanceMonitor {
    constructor() {
        this.metrics = {
            fps: 60,
            frameTime: 16.67,
            memory: 0,
            loadTime: 0
        };
        this.startTime = Date.now();
        this.setupMonitoring();
    }

    setupMonitoring() {
        // Monitor FPS
        this.monitorFPS();
        
        // Monitor memory
        this.monitorMemory();
        
        // Monitor load time
        this.monitorLoadTime();
    }

    monitorFPS() {
        let lastTime = performance.now();
        let frames = 0;
        
        const measureFPS = () => {
            frames++;
            const currentTime = performance.now();
            
            if (currentTime >= lastTime + 1000) {
                this.metrics.fps = Math.round((frames * 1000) / (currentTime - lastTime));
                frames = 0;
                lastTime = currentTime;
                
                this.sendMetrics();
            }
            
            requestAnimationFrame(measureFPS);
        };
        
        requestAnimationFrame(measureFPS);
    }

    monitorMemory() {
        setInterval(() => {
            if (performance.memory) {
                this.metrics.memory = performance.memory.usedJSHeapSize / 1024 / 1024;
            }
        }, 5000);
    }

    monitorLoadTime() {
        window.addEventListener('load', () => {
            this.metrics.loadTime = Date.now() - this.startTime;
        });
    }

    sendMetrics() {
        fetch('/api/metrics', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.metrics)
        }).catch(console.error);
    }

    getMetrics() {
        return this.metrics;
    }
}
```

## 🎯 **Best Practices**

### **Deployment Checklist**
- **Build Optimization**: Minify and compress assets
- **Performance Testing**: Test on target devices
- **Cross-Browser Testing**: Test on all supported browsers
- **Mobile Testing**: Test on mobile devices
- **Analytics Setup**: Configure analytics tracking
- **Error Tracking**: Set up error monitoring
- **Performance Monitoring**: Set up performance monitoring

### **Security Considerations**
- **HTTPS**: Use HTTPS for all connections
- **CSP**: Implement Content Security Policy
- **XSS Protection**: Prevent XSS attacks
- **CSRF Protection**: Prevent CSRF attacks
- **Input Validation**: Validate all user input
- **Secure Assets**: Use secure asset delivery

### **Performance Optimization**
- **Asset Optimization**: Optimize images and audio
- **Code Splitting**: Split code into chunks
- **Lazy Loading**: Load assets on demand
- **Caching**: Implement proper caching
- **CDN**: Use CDN for asset delivery
- **Compression**: Use compression for assets

---

## 📚 **Resources and Tools**

### **Deployment Platforms**
- **GitHub Pages**: https://pages.github.com/
- **Netlify**: https://www.netlify.com/
- **Vercel**: https://vercel.com/
- **Firebase Hosting**: https://firebase.google.com/docs/hosting

### **Game Distribution**
- **itch.io**: https://itch.io/
- **Kongregate**: https://www.kongregate.com/
- **Newgrounds**: https://www.newgrounds.com/
- **Armor Games**: https://www.armorgames.com/

### **Analytics Tools**
- **Google Analytics**: https://analytics.google.com/
- **Hotjar**: https://www.hotjar.com/
- **Mixpanel**: https://mixpanel.com/
- **Amplitude**: https://amplitude.com/

### **Testing Tools**
- **Cypress**: https://www.cypress.io/
- **Playwright**: https://playwright.dev/
- **Jest**: https://jestjs.io/
- **Mocha**: https://mochajs.org/

---

## 🎯 **Getting Help**

### **Documentation**
- **Phaser Docs**: https://phaser.io/docs/
- **Web.dev**: https://web.dev/
- **MDN Web Docs**: https://developer.mozilla.org/
- **PWA Builder**: https://www.pwabuilder.com/

### **Community**
- **Phaser Forum**: https://phaser.io/community/
- **Stack Overflow**: https://stackoverflow.com/questions/tagged/phaser
- **Reddit**: https://www.reddit.com/r/phaser/
- **Discord**: https://discord.gg/phaser

### **Professional Support**
- **Consulting**: Game deployment consulting
- **Code Review**: Deployment code review
- **Training**: Deployment training
- **Support**: Technical support services

---

*Phaser Deployment Guide*
*Version: 3.60+*
*Last Updated: 2026-03-10*
*Team: Programming Team*
*Specialist: cocos-creator-specialist*
*Platform: Web*
