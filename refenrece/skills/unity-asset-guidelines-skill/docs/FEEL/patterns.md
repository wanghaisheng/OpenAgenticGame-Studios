# FEEL (MMFeedbacks) Usage Patterns

## Overview

FEEL is a powerful feedback system from MoreMountains. It provides easy-to-use feedback effects for game feel and juice.

**Core Components:**
- `MMF_Player` - Main component that plays feedbacks
- `MMF_Feedback` - Individual feedback effects
- Feedbacks can be chained, delayed, and looped

## Quick Reference

| Component | Use Case |
|-----------|----------|
| `MMF_Player` | Container for feedbacks, attach to GameObject |
| `MMF_Position` | Animate position |
| `MMF_Scale` | Animate scale (punch, breathe, etc.) |
| `MMF_Rotation` | Animate rotation |
| `MMF_ImageAlpha` | Fade UI images |
| `MMF_Sound` | Play audio clips |
| `MMF_Particles` | Trigger particle systems |

## Common Patterns

### Basic Feedback Play

```csharp
public class ButtonEffect : MonoBehaviour
{
    [SerializeField] private MMF_Player _feedbackPlayer;

    public void OnClick()
    {
        _feedbackPlayer.PlayFeedbacks();
    }
}
```

### Stop and Reset

```csharp
public void ResetState()
{
    _feedbackPlayer.StopFeedbacks();
    _feedbackPlayer.RestoreInitialValues();
}
```

### Conditional Feedback

```csharp
public void TakeDamage(int damage)
{
    if (damage > 10)
    {
        _heavyHitFeedback.PlayFeedbacks();
    }
    else
    {
        _lightHitFeedback.PlayFeedbacks();
    }
}
```

### Feedback with Position Target

```csharp
public void SpawnEffectAt(Vector3 position)
{
    _feedbackPlayer.transform.position = position;
    _feedbackPlayer.PlayFeedbacks();
}
```

### Checking Feedback State

```csharp
public void SafePlay()
{
    if (!_feedbackPlayer.IsPlaying)
    {
        _feedbackPlayer.PlayFeedbacks();
    }
}
```

## InitializationMode Options

| Mode | When Initialized | Use Case |
|------|------------------|----------|
| `Awake` | In Awake() | Earliest initialization needed |
| `Start` | In Start() | Default, most cases |
| `Script` | Manual call | When timing control needed |

```csharp
// For Script mode
private void Start()
{
    _feedbackPlayer.Initialization();
}
```

## References

- [FEEL Official Documentation](https://feel-docs.moremountains.com/)
