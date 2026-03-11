# PrimeTween API Reference

## Core API Methods

### Transform Animation

```csharp
// Position
Tween.Position(Transform target, Vector3 endValue, float duration, Ease ease = Ease.Default, int cycles = 1, CycleMode cycleMode = CycleMode.Restart, float startDelay = 0, bool useUnscaledTime = false, UpdateType updateType = UpdateType.Update)
Tween.PositionX(Transform target, float endValue, float duration, ...)
Tween.PositionY(Transform target, float endValue, float duration, ...)
Tween.PositionZ(Transform target, float endValue, float duration, ...)
Tween.PositionAtSpeed(Transform target, Vector3 endValue, float speed, ...)

// Local Position
Tween.LocalPosition(Transform target, Vector3 endValue, float duration, ...)
Tween.LocalPositionX/Y/Z(Transform target, float endValue, float duration, ...)
Tween.LocalPositionAtSpeed(Transform target, Vector3 endValue, float speed, ...)

// Rotation
Tween.Rotation(Transform target, Quaternion endValue, float duration, ...)
Tween.RotationAtSpeed(Transform target, Vector3 endValue, float speed, ...)
Tween.EulerAngles(Transform target, Vector3 endValue, float duration, ...)
Tween.LocalEulerAngles(Transform target, Vector3 endValue, float duration, ...)
Tween.LocalRotation(Transform target, Quaternion endValue, float duration, ...)

// Scale
Tween.Scale(Transform target, float endValue, float duration, ...)
Tween.Scale(Transform target, Vector3 endValue, float duration, ...)
```

### UI Animation

```csharp
// RectTransform
Tween.UIAnchoredPosition(RectTransform target, Vector2 endValue, float duration, ...)
Tween.UIAnchoredPositionX/Y(RectTransform target, float endValue, float duration, ...)
Tween.UISizeDelta(RectTransform target, Vector2 endValue, float duration, ...)
Tween.UISizeDeltaWidth/Height(RectTransform target, float endValue, float duration, ...)

// UI Color & Alpha
Tween.Color(Graphic target, Color endValue, float duration, ...)
Tween.Alpha(Graphic target, float endValue, float duration, ...)

// Canvas Group
Tween.Alpha(CanvasGroup target, float endValue, float duration, ...)
```

### Material & Color

```csharp
Tween.Color(Material target, Color endValue, float duration, ...)
Tween.Alpha(Material target, float endValue, float duration, ...)
Tween.Color(Material target, int propertyId, Color endValue, float duration, ...)
Tween.Color(Material target, string propertyName, Color endValue, float duration, ...)
```

### Camera Animation

```csharp
Tween.OrthoSize(Camera target, float endValue, float duration, ...)
Tween.FieldOfView(Camera target, float endValue, float duration, ...)
Tween.AspectRatio(Camera target, float endValue, float duration, ...)
Tween.BackgroundColor(Camera target, Color endValue, float duration, ...)
Tween.ShakeCamera(Camera target, float strengthFactor, float duration, float frequency)
```

### Audio & Text

```csharp
// Audio
Tween.Volume(AudioSource target, float endValue, float duration, ...)
Tween.Pitch(AudioSource target, float endValue, float duration, ...)

// TextMeshPro
Tween.Color(TMP_Text target, Color endValue, float duration, ...)
Tween.Alpha(TMP_Text target, float endValue, float duration, ...)
Tween.FontSize(TMP_Text target, float endValue, float duration, ...)
Tween.MaxVisibleCharacters(TMP_Text target, int endValue, float duration, ...)

// UI Toolkit
Tween.VisualElementColor(VisualElement target, Color endValue, float duration, ...)
Tween.VisualElementBackgroundColor(VisualElement target, Color endValue, float duration, ...)
Tween.VisualElementOpacity(VisualElement target, float endValue, float duration, ...)
```

### Shake & Punch

```csharp
Tween.ShakeLocalPosition(Transform target, Vector3 strength, float duration, int frequency, float easeBetweenShakes = Ease.OutQuad)
Tween.ShakeLocalRotation(Transform target, Vector3 strength, float duration, int frequency)
Tween.ShakeLocalScale(Transform target, Vector3 strength, float duration, int frequency)
Tween.PunchLocalPosition(Transform target, Vector3 strength, float duration, int frequency)
Tween.PunchLocalRotation(Transform target, Vector3 strength, float duration, int frequency)
Tween.PunchLocalScale(Transform target, Vector3 strength, float duration, int frequency)
Tween.ShakeCustom<T>(T startValue, ShakeSettings settings, Action<T, T> onValueChange)
```

### Custom Tweens

```csharp
Tween.Custom<T>(T startValue, T endValue, float duration, Action<T> onValueChange, ...)
Tween.Custom<T>(object target, T startValue, T endValue, float duration, Action<object, T> onValueChange, ...)
```

Supported types: `float`, `Color`, `Vector2`, `Vector3`, `Vector4`, `Quaternion`, `Rect`

### Delay & Callback

```csharp
Tween.Delay(float duration, Action onComplete = null, bool useUnscaledTime = false)
Tween.Delay(object target, float duration, Action<object> onComplete, ...)
```

## Sequence API

```csharp
// Create Sequence
Sequence.Create(int cycles = 1, CycleMode cycleMode = CycleMode.Restart, Ease sequenceEase = Ease.Default, bool useUnscaledTime = false, UpdateType updateType = UpdateType.Update)

// Chain methods
Sequence.Chain(Tween tween)
Sequence.Chain(Sequence sequence)
Sequence.ChainDelay(float duration)
Sequence.ChainCallback(Action callback)

// Group methods
Sequence.Group(Tween tween)
Sequence.Group(Sequence sequence)
Sequence.GroupCallback(Action callback)

// Insert methods
Sequence.Insert(float atTime, Tween tween)
Sequence.Insert(float atTime, Sequence sequence)
Sequence.InsertCallback(float atTime, Action callback)

// Control
sequence.Stop()
sequence.Complete()
sequence.isPaused
sequence.timeScale
sequence.elapsedTime / elapsedTimeTotal
sequence.progress / progressTotal
```

## Tween Control

```csharp
// Instance methods
tween.Stop()
tween.Complete()
tween.isAlive
tween.isPaused
tween.timeScale
tween.elapsedTime / elapsedTimeTotal
tween.progress / progressTotal
tween.interpolationFactor
tween.duration

// Static methods
Tween.StopAll(object target = null)
Tween.CompleteAll(object target = null)
Tween.SetPausedAll(bool isPaused, object target = null)

// Cycles
tween.SetRemainingCycles(int cycles)
tween.SetRemainingCycles(bool stopAtEndValue)
```

## Callbacks

```csharp
// OnComplete
Tween.OnComplete(Action callback)
Tween.OnComplete(object target, Action<object> callback)

// OnUpdate
Tween.OnUpdate(Action<Tween> callback)
Tween.OnUpdate(object target, Action<object, Tween> callback)

// Warning: closures allocate memory!
// BAD:  .OnComplete(() => MyMethod())
// GOOD: .OnComplete(target: this, target => target.MyMethod())
```

## TweenSettings Struct

```csharp
// For generic animations
TweenSettings<T>(T endValue, float duration, Ease ease = Ease.Default, int cycles = 1, CycleMode cycleMode = CycleMode.Restart, float startDelay = 0, float endDelay = 0, bool useUnscaledTime = false, UpdateType updateType = UpdateType.Update)

// With start value
TweenSettings<T>(T startValue, T endValue, float duration, ...)

// Helper methods
settings.WithDirection(bool toEndValue) // Flips startValue and endValue
```

## ShakeSettings Struct

```csharp
ShakeSettings(Vector3 strength, float duration, int frequency, Ease easeBetweenShakes = Ease.OutQuad)
```

## Easing Functions

```csharp
// Standard Eases
enum Ease {
    Linear, InSine, OutSine, InOutSine,
    InQuad, OutQuad, InOutQuad,
    InCubic, OutCubic, InOutCubic,
    InQuart, OutQuart, InOutQuart,
    InQuint, OutQuint, InOutQuint,
    InExpo, OutExpo, InOutExpo,
    InCirc, OutCirc, InOutCirc,
    InElastic, OutElastic, InOutElastic,
    InBack, OutBack, InOutBack,
    InBounce, OutBounce, InOutBounce,
    Default = OutQuad
}

// Parametric Easing
Easing.Overshoot(float strength)
Easing.Bounce(float strength)
Easing.BounceExact(float amplitude)
Easing.Elastic(float strength, float period = 0.3f)

// Manual evaluation
Easing.Evaluate(float t, Ease ease)
```

## CycleMode

```csharp
enum CycleMode {
    Restart,     // Restart from beginning
    Yoyo,        // Animate forth and back
    Incremental, // Increment endValue each cycle
    Rewind       // Reverse time
}

enum SequenceCycleMode {
    Restart,
    Yoyo,
    Rewind
}
```

## UpdateType

```csharp
enum UpdateType {
    Update,       // Update in MonoBehaviour.Update()
    LateUpdate,   // Update in MonoBehaviour.LateUpdate()
    FixedUpdate   // Update in MonoBehaviour.FixedUpdate()
}
```

## Configuration

```csharp
// Set tweens capacity for zero allocations
PrimeTweenConfig.SetTweensCapacity(int capacity)

// Warn if endValue equals current value
PrimeTweenConfig.warnEndValueEqualsCurrent = true;

// Safety checks (adds validation)
#define PRIME_TWEEN_SAFETY_CHECKS

// DOTween adapter
#define PRIME_TWEEN_DOTWEEN_ADAPTER

// Experimental features
#define PRIME_TWEEN_EXPERIMENTAL
```

## Utility Methods

```csharp
// Global time scale
Tween.GlobalTimeScale(float endValue, float duration)
Tween.GlobalTimeScale(float endValue, float duration, Ease ease)

// Tween time scale
Tween.TweenTimeScale(Tween tween, float endValue, float duration)
Tween.TweenTimeScale(Sequence sequence, float endValue, float duration)

// Get tween count
Tween.GetTweensCount(object target)
```

## Complete All Patterns

```csharp
// Stop all tweens on a target
Tween.StopAll(transform);

// Complete all tweens on a target
Tween.CompleteAll(transform);

// Pause/Resume all tweens on a target
Tween.SetPausedAll(true, transform);
Tween.SetPausedAll(false, transform);
```
