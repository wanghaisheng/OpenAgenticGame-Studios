# Godot Deployment Reference

## Overview

This document provides comprehensive deployment guidelines for Godot 4.x projects, covering web deployment, desktop builds, mobile deployment, and CI/CD integration.

## Export Presets

### Web Export

#### Setup

```bash
# Export web build
godot --headless --export-release "Web" ./build/index.html

# Export with custom template
godot --headless --export-release "Web" ./build/index.html --custom-template path/to/template
```

#### Export Configuration

```ini
# export_presets.cfg
[preset.0]

name="Web"
platform="Web"
runnable=true
dedicated_server=false
custom_features=""
export_filter="all_resources"
include_filter=""
exclude_filter=""
export_path="build/index.html"

[preset.0.options]

variant/type="Regular"
vram_texture_compression/for_web="true"
html/export_icon="true"
html/custom_html_shell=""
html/head_include=""
html/canvas_resize_policy="2"
html/focus_canvas_on_start="true"
html/emulate_mouse_from_touch="true"
debug/export_console_wrapper="true"
```

#### Web Deployment to Vercel

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy to Vercel
vercel deploy ./build --prod

# Deploy with custom domain
vercel deploy ./build --prod --domain my-game.vercel.app

# Vercel configuration
# vercel.json
{
  "version": 2,
  "builds": [
    {
      "src": "index.html",
      "use": "@vercel/static"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/$1"
    }
  ]
}
```

#### Web Deployment to GitHub Pages

```bash
# Install gh-pages
npm install -g gh-pages

# Deploy to GitHub Pages
gh-pages -d ./build

# Deploy with custom domain
gh-pages -d ./build --cname my-game.github.io

# GitHub Actions for GitHub Pages
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Godot
        uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      
      - name: Export Web Build
        run: |
          mkdir -p build
          godot --headless --export-release "Web" ./build/index.html
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```

### Desktop Export

#### Windows Export

```bash
# Export Windows executable
godot --headless --export-release "Windows Desktop" ./build/game.exe

# Export with installer
godot --headless --export-release "Windows Desktop" ./build/game_installer.exe
```

#### macOS Export

```bash
# Export macOS app
godot --headless --export-release "Mac OSX" ./build/game.app

# Export with DMG
godot --headless --export-release "Mac OSX" ./build/game.dmg
```

#### Linux Export

```bash
# Export Linux executable
godot --headless --export-release "Linux/X11" ./build/game.x86_64

# Export with AppImage
godot --headless --export-release "Linux/X11" ./build/game.AppImage
```

### Mobile Export

#### Android Export

```bash
# Export Android APK
godot --headless --export-release "Android" ./build/game.apk

# Export Android AAB (for Play Store)
godot --headless --export-release "Android" ./build/game.aab
```

#### iOS Export

```bash
# Export iOS project
godot --headless --export-release "iOS" ./build/game.xcodeproj

# Build iOS project (requires Xcode)
cd ./build/game.xcodeproj
xcodebuild -project game.xcodeproj -scheme game -destination 'platform=iOS Simulator,name=iPhone 14'
```

## CI/CD Integration

### GitHub Actions Complete Pipeline

```yaml
name: Build and Deploy
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
      
      - name: Setup Godot
        uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      
      - name: Run Tests
        run: |
          godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests
      
      - name: Setup Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      
      - name: Install PlayGodot
        run: pip install playgodot
      
      - name: Run PlayGodot Tests
        run: pytest tests/ -v

  build-web:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Godot
        uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      
      - name: Export Web Build
        run: |
          mkdir -p build
          godot --headless --export-release "Web" ./build/index.html
      
      - name: Upload Web Build
        uses: actions/upload-artifact@v2
        with:
          name: web-build
          path: build/
      
      - name: Deploy to Vercel
        if: github.ref == 'refs/heads/main'
        run: |
          npm install -g vercel
          vercel deploy ./build --prod --token ${{ secrets.VERCEL_TOKEN }}

  build-desktop:
    needs: test
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Godot
        uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      
      - name: Export Desktop Build
        run: |
          mkdir -p build
          if [ "$RUNNER_OS" == "Linux" ]; then
            godot --headless --export-release "Linux/X11" ./build/game.x86_64
          elif [ "$RUNNER_OS" == "Windows" ]; then
            godot --headless --export-release "Windows Desktop" ./build/game.exe
          elif [ "$RUNNER_OS" == "macOS" ]; then
            godot --headless --export-release "Mac OSX" ./build/game.app
          fi
      
      - name: Upload Desktop Build
        uses: actions/upload-artifact@v2
        with:
          name: desktop-build-${{ matrix.os }}
          path: build/
```

### GitLab CI/CD

```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

variables:
  GODOT_VERSION: "4.2"

test:
  stage: test
  image: godotengine/godot:4.2
  script:
    - godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests
    - pip install playgodot
    - pytest tests/ -v

build-web:
  stage: build
  image: godotengine/godot:4.2
  script:
    - mkdir -p build
    - godot --headless --export-release "Web" ./build/index.html
  artifacts:
    paths:
      - build/
    expire_in: 1 week

deploy-web:
  stage: deploy
  image: node:16
  script:
    - npm install -g vercel
    - vercel deploy ./build --prod --token $VERCEL_TOKEN
  only:
    - main
```

## Platform-Specific Optimizations

### Web Optimization

#### HTML5 Template Customization

```html
<!-- custom_html_shell.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>My Godot Game</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        canvas {
            max-width: 100%;
            max-height: 100vh;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <script src="index.js"></script>
    <script>
        // Custom initialization
        const engine = new Engine();
        engine.startGame().then(() => {
            console.log('Game started successfully');
        });
    </script>
</body>
</html>
```

#### Performance Optimization

```gdscript
# Web-specific optimizations
func _ready():
    # Check if running in web
    if OS.get_name() == "HTML5":
        # Reduce quality settings
        ProjectSettings.set_setting("rendering/quality/filters/anisotropic_filter_level", 0)
        ProjectSettings.set_setting("rendering/quality/shadows/filter_mode", 0)
        
        # Optimize for mobile
        if OS.has_feature("mobile"):
            ProjectSettings.set_setting("rendering/quality/filters/texture_mipmap_bias", 0.5)
```

### Desktop Optimization

#### Windows Configuration

```ini
# export_presets.cfg - Windows specific
[preset.0.options]

application/icon="res://icon.ico"
application/file_version="1.0.0"
application/product_name="My Game"
application/product_version="1.0.0"
application/copyright="Copyright 2024"
application/trademarks="My Game Trademark"

binary/format/embed_pck="true"
codesign/enable="false"
codesign/certificate=""
codesign/certificate_password=""

texture_format/bptc="true"
texture_format/s3tc="true"
texture_format/etc="false"
texture_format/etc2="false"
```

#### macOS Configuration

```ini
# export_presets.cfg - macOS specific
[preset.1.options]

application/icon="res://icon.icns"
application/bundle_identifier="com.mycompany.mygame"
application/signature="MYGM"
application/app_category="Game"
application/short_version="1.0"
application/version="1.0.0"
application/copyright="Copyright 2024"

codesign/certificate=""
codesign/certificate_password=""
codesign/identity=""

privacy/microphone_usage_description="This game needs microphone access for voice chat."
privacy/microphone_usage_description_localized={}
privacy/camera_usage_description="This game needs camera access for AR features."
privacy/camera_usage_description_localized={}

texture_format/bptc="true"
texture_format/s3tc="false"
texture_format/etc="false"
texture_format/etc2="false"
```

### Mobile Optimization

#### Android Configuration

```ini
# export_presets.cfg - Android specific
[preset.2.options]

package/unique_name="com.mycompany.mygame"
package/name="My Game"
package/signed="false"
package/apk_expansion="false"
package/apk_expansion_salt=""
package/apk_expansion_pkey=""
package/debug_keystore=""
package/debug_keystore_user=""
package/debug_keystore_password=""

screen/support_small="true"
screen/support_normal="true"
screen/support_large="true"
screen/support_xlarge="true"
screen/orientation="landscape"

xr_features/oculus="false"
xr_features/openxr="false"

keystore/release=""
keystore/release_user=""
keystore/release_password=""

texture_format/bptc="false"
texture_format/s3tc="false"
texture_format/etc="true"
texture_format/etc2="true"
```

#### iOS Configuration

```ini
# export_presets.cfg - iOS specific
[preset.3.options]

application/bundle_identifier="com.mycompany.mygame"
application/signature="MYGM"
application/app_category="Game"
application/short_version="1.0"
application/version="1.0.0"
application/copyright="Copyright 2024"

capabilities/access_wifi="false"
capabilities/access_network_state="false"
capabilities/bluetooth="false"
capabilities/camera="false"
capabilities/gps="false"
capabilities/microphone="false"

privacy/microphone_usage_description="This game needs microphone access for voice chat."
privacy/microphone_usage_description_localized={}
privacy/camera_usage_description="This game needs camera access for AR features."
privacy/camera_usage_description_localized={}

texture_format/bptc="true"
texture_format/s3tc="false"
texture_format/etc="false"
texture_format/etc2="false"
```

## Deployment Automation

### Scripted Deployment

```bash
#!/bin/bash
# deploy.sh

set -e

echo "Starting deployment..."

# Clean previous builds
rm -rf build/
mkdir -p build/

# Export web build
echo "Exporting web build..."
godot --headless --export-release "Web" ./build/index.html

# Deploy to Vercel
if [ "$VERCEL_TOKEN" ]; then
    echo "Deploying to Vercel..."
    vercel deploy ./build --prod --token $VERCEL_TOKEN
fi

# Deploy to GitHub Pages
if [ "$GITHUB_TOKEN" ]; then
    echo "Deploying to GitHub Pages..."
    gh-pages -d ./build
fi

echo "Deployment completed!"
```

### Python Deployment Script

```python
# deploy.py
import os
import subprocess
import json
from pathlib import Path

def run_command(cmd):
    """Run command and return output"""
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)
    if result.returncode != 0:
        print(f"Error: {result.stderr}")
        exit(1)
    return result.stdout

def export_web():
    """Export web build"""
    print("Exporting web build...")
    os.makedirs("build", exist_ok=True)
    run_command("godot --headless --export-release \"Web\" ./build/index.html")
    print("Web export completed")

def deploy_vercel():
    """Deploy to Vercel"""
    if os.getenv("VERCEL_TOKEN"):
        print("Deploying to Vercel...")
        run_command("vercel deploy ./build --prod")
        print("Vercel deployment completed")
    else:
        print("VERCEL_TOKEN not found, skipping Vercel deployment")

def deploy_github_pages():
    """Deploy to GitHub Pages"""
    if os.getenv("GITHUB_TOKEN"):
        print("Deploying to GitHub Pages...")
        run_command("gh-pages -d ./build")
        print("GitHub Pages deployment completed")
    else:
        print("GITHUB_TOKEN not found, skipping GitHub Pages deployment")

def main():
    """Main deployment function"""
    print("Starting deployment...")
    
    export_web()
    deploy_vercel()
    deploy_github_pages()
    
    print("Deployment completed!")

if __name__ == "__main__":
    main()
```

## Monitoring and Analytics

### Performance Monitoring

```gdscript
# Performance monitoring script
extends Node

func _ready():
    # Start monitoring
    monitor_performance()

func monitor_performance():
    var fps = Engine.get_frames_per_second()
    var memory = OS.get_static_memory_usage_by_type()
    
    print("FPS: ", fps)
    print("Memory usage: ", memory[OS.MEMORY_TYPE_STATIC] / 1024 / 1024, " MB")
    
    # Send to analytics service
    send_analytics({
        "fps": fps,
        "memory_mb": memory[OS.MEMORY_TYPE_STATIC] / 1024 / 1024,
        "platform": OS.get_name(),
        "timestamp": Time.get_unix_time_from_system()
    })

func send_analytics(data):
    # Send data to analytics service
    var json_data = JSON.new().stringify(data)
    # Implementation depends on your analytics service
    pass
```

### Error Tracking

```gdscript
# Error tracking
extends Node

func _ready():
    # Set up error handler
    get_tree().set_auto_accept_quit(false)
    get_tree().quit.connect(_on_quit)

func _on_quit():
    # Send error reports before quitting
    send_error_reports()

func send_error_reports():
    # Collect error logs and send to service
    var errors = []
    
    # Implementation depends on your error tracking service
    pass
```

## Best Practices

### General Deployment

1. **Automate Everything**: Use CI/CD for all deployments
2. **Version Management**: Use semantic versioning
3. **Environment Separation**: Separate staging and production
4. **Rollback Strategy**: Always have a rollback plan
5. **Monitoring**: Deploy with monitoring and alerting

### Platform-Specific

1. **Web**: Optimize for performance and loading times
2. **Desktop**: Include proper installers and uninstallers
3. **Mobile**: Follow platform guidelines and store requirements
4. **Console**: Meet certification requirements and platform standards

### Security

1. **Code Signing**: Sign all builds for security
2. **Encryption**: Encrypt sensitive data and communications
3. **Authentication**: Implement proper user authentication
4. **Privacy**: Follow privacy regulations and best practices

---

*Godot Deployment Reference*
*Version: 1.2.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
