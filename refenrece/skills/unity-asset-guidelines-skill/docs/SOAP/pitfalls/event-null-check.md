# Event Null Check Required

## Summary

ScriptableEvent references may be null if not assigned in Inspector, causing NullReferenceException.

## Prevention

- Always add null check before subscribing/unsubscribing
- Verify Inspector assignments before play mode

## Symptoms

- NullReferenceException in OnEnable or OnDisable
- Works in some scenes but not others
- Works for some prefab instances but not others

## Root Cause

1. SerializeField declared but not assigned in Inspector
2. OnEnable runs and tries to access null reference
3. NullReferenceException thrown

## Solution

### Always Use Null Check

```csharp
private void OnEnable()
{
    if (_onDamageEvent != null)
        _onDamageEvent.OnRaised += OnDamaged;
}

private void OnDisable()
{
    if (_onDamageEvent != null)
        _onDamageEvent.OnRaised -= OnDamaged;
}
```

### Alternative: Required Field Validation

```csharp
private void Awake()
{
    if (_onDamageEvent == null)
    {
        Debug.LogError($"[{gameObject.name}] _onDamageEvent is not assigned!", this);
    }
}
```

## Testing

1. Leave SerializeField unassigned intentionally
2. Enter play mode
3. Verify no NullReferenceException (with null check)
4. Verify warning logged (with validation)

## Discovery

- Standard Unity SerializeField pattern issue
- Particularly important for prefabs used across multiple scenes
