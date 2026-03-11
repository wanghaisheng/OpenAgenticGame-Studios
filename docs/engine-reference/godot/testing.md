# Godot Testing Reference

## Overview

This document provides comprehensive testing guidelines for Godot 4.x projects, covering both unit testing with GdUnit4 and game automation with PlayGodot.

## Testing Frameworks

### GdUnit4 - Unit Testing Framework

GdUnit4 is a unit testing framework for GDScript that runs tests directly inside Godot.

#### Setup

```bash
# Install GdUnit4 addon
# Download from: https://github.com/godotengine/gdUnit4
# Extract to: addons/gdUnit4/
```

#### Test Structure

```
project/
├── addons/gdUnit4/
├── test/
│   ├── suites/
│   │   ├── TestPlayer.gd
│   │   ├── TestHealthSystem.gd
│   │   └── TestUIComponents.gd
│   └── test_resources/
└── src/
```

#### Running Tests

```bash
# Run all tests
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests

# Run specific test suite
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests --suite TestPlayer

# Run with coverage
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests --coverage
```

### PlayGodot - Game Automation Framework

PlayGodot provides Python-based game automation, similar to Playwright for web applications.

#### Setup

```bash
# Install dependencies
pip install playgodot

# Set Godot path
export GODOT_PATH=/path/to/godot-automation-fork
```

#### Test Structure

```
project/
├── tests/
│   ├── test_game_logic.py
│   ├── test_ui_automation.py
│   └── test_integration.py
├── requirements.txt
└── pytest.ini
```

#### Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run specific test
pytest tests/test_game_logic.py::TestPlayerMovement -v

# Run with coverage
pytest tests/ --cov=src --cov-report=html
```

## Testing Best Practices

### Unit Testing with GdUnit4

#### Test Naming Conventions

```gdscript
# Good: Descriptive and clear
func test_player_should_move_right_when_right_key_pressed():
func test_health_should_decrease_when_taking_damage():
func test_ui_button_should_be_disabled_when_game_is_paused():

# Avoid: Generic names
func test_movement():
func test_health():
func test_button():
```

#### Test Organization

```gdscript
extends GdUnitTestSuite

# Test setup
func before_test():
    # Runs before each test
    pass

func after_test():
    # Runs after each test
    pass

# Test cases
func test_player_initialization():
    var player = create_test_player()
    assert_int(player.health).is_equal(100)
    assert_int(player.position.x).is_equal(0)
    assert_int(player.position.y).is_equal(0)

func test_player_movement():
    var player = create_test_player()
    var initial_pos = player.position
    
    player.move_right()
    await get_tree().create_timer(0.1).timeout
    
    assert_float(player.position.x).is_greater(initial_pos.x)
```

#### Assertion Examples

```gdscript
# Integer assertions
assert_int(player.health).is_equal(100)
assert_int(player.health).is_greater(0)
assert_int(player.health).is_between(0, 100)

# String assertions
assert_string(player.name).is_equal("Player")
assert_string(player.state).contains("active")
assert_string(player.state).does_not_contain("dead")

# Node assertions
assert_node(player).is_not_null()
assert_node(player).is_instanceof(Player)
assert_node(player).is_inside_tree()

# Signal assertions
await assert_signal(player).wait_for_signal("health_changed", 1.0)
assert_signal(player).has_signal_emission_count("moved", 3)
```

### Game Automation with PlayGodot

#### Test Structure

```python
from playgodot import Game, GameTest
import pytest

class TestPlayerMovement(GameTest):
    async def test_player_can_move_right(self):
        game = await Game.launch("res://scenes/main.tscn")
        
        # Get player
        player = game.get_node("Player")
        initial_pos = player.position
        
        # Simulate key press
        await game.press_key(KEY_RIGHT)
        await game.wait(0.5)
        
        # Assert movement
        assert player.position.x > initial_pos.x
        
        await game.close()

class TestUIInteraction(GameTest):
    async def test_button_click_triggers_action(self):
        game = await Game.launch("res://scenes/main.tscn")
        
        # Get button
        button = game.get_node("UI/ActionButton")
        
        # Click button
        await game.click_node(button)
        await game.wait(0.1)
        
        # Assert action triggered
        assert game.has_signal("action_triggered")
        
        await game.close()
```

#### Advanced Automation

```python
class TestComplexScenarios(GameTest):
    async def test_complete_game_flow(self):
        game = await Game.launch("res://scenes/main.tscn")
        
        # Start game
        await game.click_node("UI/StartButton")
        await game.wait(1.0)
        
        # Play through level
        await self.play_through_level(game)
        
        # Check win condition
        assert game.get_node("UI/WinScreen").visible
        
        await game.close()
    
    async def play_through_level(self, game):
        # Navigate through level
        await game.press_key(KEY_RIGHT, duration=2.0)
        await game.press_key(KEY_SPACE)
        await game.wait(0.5)
        await game.press_key(KEY_RIGHT, duration=1.0)
```

## Integration Testing

### Component Integration

```gdscript
func test_player_weapon_integration():
    var player = create_test_player()
    var weapon = preload("res://weapons/Sword.tscn").instantiate()
    
    # Equip weapon
    player.equip_weapon(weapon)
    
    # Test interaction
    player.attack()
    assert_signal(weapon).wait_for_signal("weapon_used", 1.0)
    assert_bool(player.is_attacking).is_true()
```

### System Integration

```python
async def test_save_load_system():
    game = await Game.launch("res://scenes/main.tscn")
    
    # Get initial state
    player = game.get_node("Player")
    initial_health = player.health
    initial_position = player.position
    
    # Save game
    await game.click_node("UI/SaveButton")
    await game.wait(0.5)
    
    # Change state
    player.health = 50
    player.position = Vector2(100, 100)
    
    # Load game
    await game.click_node("UI/LoadButton")
    await game.wait(0.5)
    
    # Verify state restored
    assert player.health == initial_health
    assert player.position == initial_position
    
    await game.close()
```

## Performance Testing

### Frame Rate Testing

```python
async def test_performance_under_load():
    game = await Game.launch("res://scenes/main.tscn")
    
    # Add load
    for i in range(100):
        enemy = preload("res://enemies/Enemy.tscn").instantiate()
        game.get_node("Enemies").add_child(enemy)
    
    # Measure frame rate
    initial_fps = Engine.get_frames_per_second()
    await game.wait(5.0)
    final_fps = Engine.get_frames_per_second()
    
    # Assert performance
    assert final_fps >= 30  # Minimum acceptable FPS
    
    await game.close()
```

### Memory Testing

```gdscript
func test_memory_usage():
    var initial_memory = OS.get_static_memory_usage_by_type()
    
    # Create many objects
    var objects = []
    for i in range(1000):
        objects.append(Node.new())
    
    var peak_memory = OS.get_static_memory_usage_by_type()
    
    # Clean up
    for obj in objects:
        obj.queue_free()
    
    var final_memory = OS.get_static_memory_usage_by_type()
    
    # Assert memory management
    assert_int(peak_memory[OS.MEMORY_TYPE_STATIC]).is_less_than(initial_memory[OS.MEMORY_TYPE_STATIC] * 2)
```

## CI/CD Integration

### GitHub Actions

```yaml
name: Godot Tests
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Godot
        uses: godotengine/godot-ci@v3
        with:
          godot-version: 4.2
      
      - name: Run GdUnit4 Tests
        run: |
          godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --run-tests --coverage
      
      - name: Setup Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'
      
      - name: Install PlayGodot
        run: pip install playgodot
      
      - name: Run PlayGodot Tests
        run: pytest tests/ -v
      
      - name: Upload Coverage
        uses: codecov/codecov-action@v1
        with:
          file: ./coverage.xml
```

## Debugging Tests

### Common Issues

1. **Test Isolation**: Ensure tests don't share state
2. **Async Testing**: Use proper await patterns
3. **Node Cleanup**: Always queue_free nodes
4. **Signal Timing**: Use proper timeouts for signals

### Debugging Techniques

```gdscript
func test_with_debugging():
    var player = create_test_player()
    
    # Debug output
    print("Player created with health: ", player.health)
    
    # Step through
    player.take_damage(10)
    print("After damage, health: ", player.health)
    
    # Breakpoints (in Godot editor)
    breakpoint
    
    assert_int(player.health).is_equal(90)
```

## Best Practices Summary

1. **Write descriptive test names**
2. **Keep tests focused and small**
3. **Use proper setup and teardown**
4. **Test both positive and negative cases**
5. **Mock external dependencies**
6. **Maintain high test coverage**
7. **Automate testing in CI/CD**
8. **Regularly review and refactor tests**

---

*Godot Testing Reference*
*Version: 1.2.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
