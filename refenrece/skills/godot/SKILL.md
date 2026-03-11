---
name: godot
version: 1.2.0
description: Develop, test, build, and deploy Godot 4.x games. Includes GdUnit4 for GDScript unit tests and PlayGodot for game automation and E2E testing. Supports web/desktop exports, CI/CD pipelines, and deployment to Vercel/GitHub Pages/itch.io.
---

# Godot Skill

Develop, test, build, and deploy Godot 4.x games.

## Quick Reference

```bash
# GdUnit4 - Unit testing framework (GDScript, runs inside Godot)
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests

# PlayGodot - Game automation framework (Python, like Playwright for games)
export GODOT_PATH=/path/to/godot-automation-fork
pytest tests/ -v

# Export web build
godot --headless --export-release "Web" ./build/index.html

# Deploy to Vercel
vercel deploy ./build --prod
```

---

## Testing Overview

| | GdUnit4 | PlayGodot |
|---|---------|-----------|
| Type | Unit testing | Game automation |
| Language | GDScript | Python |
| Runs | Inside Godot | External (like Playwright) |
| Requires | Addon | Custom Godot fork |
| Best for | Unit/component tests | E2E/integration tests |

---

## GdUnit4 (GDScript Tests)

GdUnit4 runs tests written in GDScript directly inside Godot.

### Project Structure

```
project/
├── addons/gdUnit4/          # GdUnit4 addon
├── test/                     # Test directory
│   ├── suites/               # Test suites
│   │   └── MyTestSuite.gd    # Test suite file
│   └── test_resources/       # Test resources
└── src/                      # Source code
```

### Test Example

```gdscript
# test/suites/MyTestSuite.gd
extends GdUnitTestSuite

func test_example():
    var result = 2 + 2
    assert_int(result).is_equal(4)

func test_node_creation():
    var node = Node.new()
    assert_node(node).is_not_null()
    node.queue_free()
```

### Running Tests

```bash
# Run all tests
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests

# Run specific test suite
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests --suite MyTestSuite

# Run with verbose output
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests --verbose
```

---

## PlayGodot (Python Tests)

PlayGodot provides Python-based game automation, similar to Playwright for web applications.

### Setup

```bash
# Install dependencies
pip install -r requirements.txt

# Set Godot path
export GODOT_PATH=/path/to/godot-automation-fork
```

### Test Example

```python
# tests/test_game.py
from playgodot import Game, GameTest

class TestGame(GameTest):
    async def test_player_movement(self):
        game = await Game.launch("res://scenes/main.tscn")
        
        # Test player movement
        player = game.get_node("Player")
        initial_pos = player.position
        
        # Simulate key press
        await game.press_key(KEY_RIGHT)
        await game.wait(0.5)
        
        # Assert player moved
        assert player.position.x > initial_pos.x
        
        await game.close()
```

### Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run specific test
pytest tests/test_game.py::TestGame::test_player_movement -v

# Run with coverage
pytest tests/ --cov=src --cov-report=html
```

---

## Export and Deployment

### Web Export

```bash
# Export web build
godot --headless --export-release "Web" ./build/index.html

# Export with custom template
godot --headless --export-release "Web" ./build/index.html --custom-template path/to/template
```

### Desktop Export

```bash
# Export Windows
godot --headless --export-release "Windows Desktop" ./build/game.exe

# Export macOS
godot --headless --export-release "Mac OSX" ./build/game.app

# Export Linux
godot --headless --export-release "Linux/X11" ./build/game.x86_64
```

### Deployment to Vercel

```bash
# Deploy to Vercel
vercel deploy ./build --prod

# Deploy with custom domain
vercel deploy ./build --prod --domain my-game.vercel.app
```

### Deployment to GitHub Pages

```bash
# Deploy to GitHub Pages
gh-pages -d ./build

# Deploy with custom domain
gh-pages -d ./build --cname my-game.github.io
```

---

## CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/test.yml
name: Test and Deploy
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      - name: Run GdUnit4 tests
        run: godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests
      - name: Run PlayGodot tests
        run: pytest tests/ -v
      - name: Export web build
        run: godot --headless --export-release "Web" ./build/index.html
      - name: Deploy to Vercel
        run: vercel deploy ./build --prod
```

---

## Best Practices

### Testing
- Write unit tests for core game logic
- Use PlayGodot for integration and E2E tests
- Keep tests fast and focused
- Mock external dependencies

### Export
- Optimize assets for target platform
- Test exports on all target platforms
- Use custom export templates when needed
- Include proper error handling

### Deployment
- Use automated CI/CD pipelines
- Test deployments in staging first
- Monitor deployed applications
- Keep deployment configurations versioned

---

## Integration with Claude Code Game Studios

This skill integrates with the following agents:
- **Godot Specialist [37]** - Core Godot development
- **Godot GDScript Specialist [38]** - GDScript programming
- **Godot GDExtension Specialist [39]** - Native extensions
- **Godot Shader Specialist [40]** - Shader development
- **Godot Full-Stack Specialist** - Testing, deployment, and CI/CD

---

*Version: 1.2.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
