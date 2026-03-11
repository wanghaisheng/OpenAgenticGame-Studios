# GdUnit4 Assertions Reference

This document provides a comprehensive reference for GdUnit4 assertions and testing utilities.

## Core Assertions

### Integer Assertions

```gdscript
# Equality
assert_int(value).is_equal(expected)
assert_int(value).is_not_equal(expected)

# Comparison
assert_int(value).is_greater(expected)
assert_int(value).is_greater_or_equal(expected)
assert_int(value).is_less(expected)
assert_int(value).is_less_or_equal(expected)

# Range
assert_int(value).is_between(min, max)
assert_int(value).is_not_between(min, max)
```

### Float Assertions

```gdscript
# Equality (with tolerance)
assert_float(value).is_equal(expected, tolerance)
assert_float(value).is_not_equal(expected, tolerance)

# Comparison
assert_float(value).is_greater(expected)
assert_float(value).is_greater_or_equal(expected)
assert_float(value).is_less(expected)
assert_float(value).is_less_or_equal(expected)
```

### String Assertions

```gdscript
# Equality
assert_string(value).is_equal(expected)
assert_string(value).is_not_equal(expected)

# Contains
assert_string(value).contains(substring)
assert_string(value).does_not_contain(substring)

# Start/End
assert_string(value).starts_with(prefix)
assert_string(value).ends_with(suffix)

# Empty
assert_string(value).is_empty()
assert_string(value).is_not_empty()
```

### Boolean Assertions

```gdscript
assert_bool(value).is_true()
assert_bool(value).is_false()
```

### Node Assertions

```gdscript
# Null checks
assert_node(node).is_null()
assert_node(node).is_not_null()

# Type checks
assert_node(node).is_instanceof(expected_type)
assert_node(node).is_not_instanceof(expected_type)

# Tree checks
assert_node(node).is_inside_tree()
assert_node(node).is_not_inside_tree()

# Child checks
assert_node(parent).has_child(child)
assert_node(parent).does_not_have_child(child)
```

### Array Assertions

```gdscript
# Size
assert_array(array).has_size(expected)
assert_array(array).is_empty()
assert_array(array).is_not_empty()

# Contains
assert_array(array).contains(item)
assert_array(array).does_not_contain(item)

# All/Any
assert_array(array).contains_all(items)
assert_array(array).contains_any(items)
```

### Dictionary Assertions

```gdscript
# Size
assert_dict(dictionary).has_size(expected)
assert_dict(dictionary).is_empty()
assert_dict(dictionary).is_not_empty()

# Keys
assert_dict(dictionary).has_key(key)
assert_dict(dictionary).does_not_have_key(key)

# Values
assert_dict(dictionary).has_value(value)
assert_dict(dictionary).does_not_have_value(value)
```

## Advanced Assertions

### Signal Assertions

```gdscript
# Wait for signal
await assert_signal(emitter).wait_for_signal("signal_name", timeout)

# Signal emission count
assert_signal(emitter).has_signal_emission_count("signal_name", expected_count)
```

### File Assertions

```gdscript
# File existence
assert_file("path/to/file").exists()
assert_file("path/to/file").does_not_exist()

# File content
assert_file("path/to/file").has_content(expected_content)
```

### Custom Assertions

```gdscript
# Custom assertion function
func assert_custom_condition(value, condition_func):
    assert_bool(condition_func.call(value)).is_true()

# Usage
assert_custom_condition(my_value, func(x): return x > 0)
```

## Test Utilities

### Test Setup and Teardown

```gdscript
extends GdUnitTestSuite

func before_test():
    # Runs before each test
    pass

func after_test():
    # Runs after each test
    pass

func before():
    # Runs before all tests in suite
    pass

func after():
    # Runs after all tests in suite
    pass
```

### Test Doubles

```gdscript
# Mocking
var mock_node = mock(Node)
mock_node.set_method("get_position", Vector2.ZERO)

# Stubbing
stub(node).to_return("get_position", Vector2.ZERO)

# Spying
var spy_node = spy(Node)
# Verify calls
verify(spy_node).was_called("get_position")
```

### Parameterized Tests

```gdscript
func test_with_parameters():
    var test_cases = [
        [1, 2, 3],  # a, b, expected_sum
        [2, 3, 5],
        [0, 0, 0]
    ]
    
    for case in test_cases:
        var a = case[0]
        var b = case[1]
        var expected = case[2]
        
        var result = add(a, b)
        assert_int(result).is_equal(expected)
```

## Best Practices

### Test Organization

```gdscript
# Group related tests
func test_player_movement_right():
    # Test right movement
    pass

func test_player_movement_left():
    # Test left movement
    pass

func test_player_movement_jump():
    # Test jumping
    pass
```

### Test Naming

```gdscript
# Use descriptive names
func test_player_should_move_right_when_right_key_pressed():
    # Clear and descriptive
    pass

# Avoid generic names
func test_movement():
    # Not descriptive enough
    pass
```

### Assertion Messages

```gdscript
# Add custom messages
assert_int(result).is_equal(expected, "Expected %d but got %d" % [expected, result])

# Use meaningful messages
assert_bool(is_valid).is_true("Validation should pass for valid input")
```

### Test Data Management

```gdscript
# Use test resources
var test_data = load("res://test/resources/test_data.json")

# Create test fixtures
func create_test_player():
    var player = preload("res://src/Player.tscn").instantiate()
    player.position = Vector2(100, 100)
    return player
```

## Integration Examples

### Testing Game Logic

```gdscript
func test_health_system():
    var player = create_test_player()
    player.health = 100
    
    # Test damage
    player.take_damage(20)
    assert_int(player.health).is_equal(80)
    
    # Test healing
    player.heal(10)
    assert_int(player.health).is_equal(90)
    
    # Test death
    player.take_damage(100)
    assert_bool(player.is_dead()).is_true()
```

### Testing UI Components

```gdscript
func test_button_interaction():
    var button = preload("res://ui/ActionButton.tscn").instantiate()
    add_child(button)
    
    # Test initial state
    assert_bool(button.is_disabled()).is_false()
    
    # Test click
    button.pressed.emit()
    assert_signal(button).wait_for_signal("action_triggered", 1.0)
    
    button.queue_free()
```

### Testing Network Components

```gdscript
func test_network_connection():
    var network = preload("res://network/NetworkManager.tscn").instantiate()
    add_child(network)
    
    # Mock network
    stub(network).to_return("is_connected", true)
    
    # Test connection
    assert_bool(network.connect_to_server()).is_true()
    assert_bool(network.is_connected()).is_true()
    
    network.queue_free()
```

---

*Reference for GdUnit4 assertions*
*Version: 1.2.0*
*Last updated: 2026-03-10*
