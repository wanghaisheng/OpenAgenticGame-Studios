# SOAP Usage Patterns

## Overview

SOAP is a Scriptable Object-based architecture package. It separates data (Variable) from view (Component) and promotes loose coupling between components.

**Core Principles:**
- Complete separation of data and view
- No direct references (Singleton Managers, etc.)
- Pub/Sub communication through ScriptableEvents

## Quick Reference

| Type | Use Case |
|------|----------|
| `IntVariable` | Integer values (score, count, etc.) |
| `FloatVariable` | Float values (health, speed, etc.) |
| `StringVariable` | String values |
| `BoolVariable` | Boolean values |
| `Vector3Variable` | 3D vector values |
| `ScriptableEventNoParam` | Events without parameters |
| `ScriptableEvent<T>` | Events with parameters (requires custom class) |

## Common Patterns

### Variable Read-Only Pattern

```csharp
public class HealthDisplay : MonoBehaviour
{
    [SerializeField] private IntVariable _healthVariable;
    [SerializeField] private TextMeshProUGUI _healthText;

    private void OnEnable()
    {
        _healthVariable.AddListener(UpdateDisplay);
        UpdateDisplay();
    }

    private void OnDisable()
    {
        _healthVariable.RemoveListener(UpdateDisplay);
    }

    private void UpdateDisplay()
    {
        _healthText.text = _healthVariable.Value.ToString();
    }
}
```

### Variable Write Pattern

```csharp
public class DamageSystem
{
    public static void ApplyDamage(IntVariable health, int damage)
    {
        health.Value = Mathf.Max(0, health.Value - damage);
    }
}
```

### Parameterless Event Pattern

```csharp
// Publisher
public class BoxOpener : MonoBehaviour
{
    [SerializeField] private ScriptableEventNoParam _onBoxOpenedEvent;

    public void OpenBox()
    {
        _onBoxOpenedEvent.Raise();
    }
}

// Subscriber
public class BoxUI : MonoBehaviour
{
    [SerializeField] private ScriptableEventNoParam _onBoxOpenedEvent;

    private void OnEnable()
    {
        if (_onBoxOpenedEvent != null)
            _onBoxOpenedEvent.OnRaised += OnBoxOpened;
    }

    private void OnDisable()
    {
        if (_onBoxOpenedEvent != null)
            _onBoxOpenedEvent.OnRaised -= OnBoxOpened;
    }

    private void OnBoxOpened()
    {
        Debug.Log("Box opened!");
    }
}
```

### Parameterized Event Pattern

**Step 1: Create Event Class**
```csharp
using Obvious.Soap;
using UnityEngine;

[CreateAssetMenu(fileName = "ScoreChangedEvent", menuName = "Events/ScoreChangedEvent")]
public class ScoreChangedEvent : ScriptableEvent<int>
{
}
```

**Step 2: Raise Event**
```csharp
public class ScoreSystem : MonoBehaviour
{
    [SerializeField] private ScoreChangedEvent _onScoreChangedEvent;

    public void AddScore(int points)
    {
        _onScoreChangedEvent.Raise(points);
    }
}
```

**Step 3: Subscribe to Event**
```csharp
public class ScoreUI : MonoBehaviour
{
    [SerializeField] private ScoreChangedEvent _onScoreChangedEvent;

    private void OnEnable()
    {
        if (_onScoreChangedEvent != null)
            _onScoreChangedEvent.OnRaised += UpdateScore;
    }

    private void OnDisable()
    {
        if (_onScoreChangedEvent != null)
            _onScoreChangedEvent.OnRaised -= UpdateScore;
    }

    private void UpdateScore(int newScore)
    {
        Debug.Log($"Score: {newScore}");
    }
}
```

### No Direct References

```csharp
// ❌ Bad - Direct Singleton Manager reference
BoxManager.Instance.OpenBox();
GameManager.Instance.AddScore(100);

// ✅ Good - Use ScriptableEvent
[SerializeField] private ScriptableEventNoParam _openBoxEvent;
_openBoxEvent.Raise();

// ✅ Good - Use Variable
[SerializeField] private IntVariable _scoreVariable;
_scoreVariable.Value += 100;
```

## Naming Conventions

| Type | Format | Example |
|------|--------|---------|
| Variable | `[Feature][Type]Variable` | `BoxCountVariable`, `PlayerHealthVariable` |
| Event (No Param) | `[Feature][Action]Event` | `BoxOpenedEvent`, `PlayerDeathEvent` |
| Event (With Param) | Custom class name | `ScoreChangedEvent : ScriptableEvent<int>` |
| Data | `[Feature]Data` | `BoxData`, `DogData` |

## References

- [SOAP Asset Store](https://assetstore.unity.com/packages/tools/utilities/soap-scriptable-object-architecture-pattern-232107)
