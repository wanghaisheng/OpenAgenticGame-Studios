# Variable Listener Memory Leak

## Summary

Subscribing to Variable changes without unsubscribing causes memory leaks and unexpected behavior.

## Prevention

- Always pair `AddListener` in OnEnable with `RemoveListener` in OnDisable
- Never subscribe in Start() or Awake() without corresponding unsubscribe

## Symptoms

- Memory usage grows over time
- Destroyed objects still receiving callbacks
- Multiple callback invocations for single value change
- Console errors referencing destroyed objects

## Root Cause

When a MonoBehaviour subscribes to a ScriptableObject's event but doesn't unsubscribe:
1. ScriptableObject holds reference to the listener
2. GameObject is destroyed but listener reference remains
3. ScriptableObject tries to invoke destroyed listener
4. Memory cannot be freed (leak)

## Solution

### Correct Pattern

```csharp
private void OnEnable()
{
    _healthVariable.AddListener(OnHealthChanged);
}

private void OnDisable()
{
    _healthVariable.RemoveListener(OnHealthChanged);
}
```

### Incorrect Pattern

```csharp
// ❌ Bad - Subscribe only, no unsubscribe
private void Start()
{
    _healthVariable.AddListener(OnHealthChanged);
    // No unsubscribe in OnDisable!
}
```

## Testing

To verify no leaks:
1. Subscribe to variable
2. Destroy the subscribing GameObject
3. Change the variable value
4. Check console for errors

## Discovery

- Common Unity/SOAP pattern issue
- Applies to all ScriptableObject-based event systems
