# RestoreInitialValues Timing Issue

## Summary

`RestoreInitialValues()` restores to values captured at `Initialization()` execution time, not the original Inspector/Scene values.

## Prevention

- Cache initial values manually in Awake()
- Or ensure Initialization() is called before any RestoreInitialValues()

## Symptoms

- Transform values reset to (0,0,0) instead of Inspector values
- Works in Editor but fails on Android/iOS builds
- First instance behaves differently than others
- Only specific slots/instances affected

## Root Cause

**Common Expectation:**
```
RestoreInitialValues() → Restores to original Inspector/Scene values
```

**Actual Behavior:**
```
RestoreInitialValues() → Restores to values captured at Initialization() time
```

**Sequence of events:**
1. Unity starts → Inspector value (e.g., `(0, 0.447, 0)`) applied
2. Event fires (e.g., SOAP event) → Your method called
3. `RestoreInitialValues()` called → MMF_Player not yet initialized
4. Transform captured/overwritten to `(0, 0, 0)`

**Why it works in Editor but not on device:**
- Editor has more predictable script execution order
- Android IL2CPP builds may have different timing

## Solution

### Option 1: Manual Caching (Recommended)

```csharp
private Vector3 _initialPosition;

private void Awake()
{
    // Cache the value set in the scene directly
    _initialPosition = targetTransform.localPosition;
}

private void ResetToInitial()
{
    feedbackPlayer.StopFeedbacks();
    // Restore directly instead of using RestoreInitialValues()
    targetTransform.localPosition = _initialPosition;
}
```

### Option 2: Explicit Initialization

```csharp
private void Start()
{
    // Explicitly initialize in Start
    feedbackPlayer.Initialization();
}

private void ResetToInitial()
{
    // Now safe to use
    feedbackPlayer.RestoreInitialValues();
}
```

### Option 3: State Verification

```csharp
private void ResetFeedback()
{
    if (feedbackPlayer == null) return;

    feedbackPlayer.StopFeedbacks();

    if (feedbackPlayer.IsPlaying)
    {
        feedbackPlayer.StopFeedbacks();
    }
}
```

## Script Execution Order

If timing issues persist, consider Script Execution Order settings:

1. Edit → Project Settings → Script Execution Order
2. Set MMF_Player to earlier order (negative value)

**Note:** Even with `Awake` InitializationMode, MMF_Player may execute later than other scripts' Awake.

## Testing

1. Test on actual Android/iOS device, not just Editor
2. Test with multiple instances of the same prefab
3. Verify first instance behavior specifically

## Discovery

- Date: 2026-01-30
- Context: Android build에서 첫 번째 슬롯 위치 버그
- Related: KennelSlotView.cs
