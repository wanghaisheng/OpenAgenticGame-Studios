# FEEL (MMFeedbacks) Common Pitfalls and Troubleshooting

## Overview
This document covers common pitfalls, issues, and troubleshooting strategies when using FEEL (MMFeedbacks) in Unity projects.

## Common Pitfalls

### 1. Performance Issues

#### Problem: Excessive Feedback Instances
**Symptoms**: Frame rate drops, stuttering during intense gameplay
**Cause**: Too many feedback instances playing simultaneously
**Solution**:
```csharp
public class FeedbackLimiter : MonoBehaviour
{
    public MMFeedbacks feedback;
    public float cooldownTime = 0.1f;
    private float lastPlayTime;
    
    public void PlayFeedbackLimited()
    {
        if (Time.time - lastPlayTime >= cooldownTime)
        {
            feedback.PlayFeedbacks();
            lastPlayTime = Time.time;
        }
    }
}
```

#### Problem: Memory Leaks
**Symptoms**: Memory usage increases over time
**Cause**: Feedback objects not being properly cleaned up
**Solution**:
```csharp
public class FeedbackCleaner : MonoBehaviour
{
    private void OnDestroy()
    {
        // Clean up all feedbacks
        var feedbacks = GetComponentsInChildren<MMFeedbacks>();
        foreach (var feedback in feedbacks)
        {
            feedback.StopFeedbacks();
            feedback.DestroyFeedbacks();
        }
    }
}
```

### 2. Timing and Synchronization Issues

#### Problem: Feedback Not Playing
**Symptoms**: Feedback doesn't play when expected
**Causes**:
- Feedback disabled in inspector
- Wrong timing settings
- GameObject not active
**Troubleshooting Checklist**:
- [ ] Feedback GameObject is active
- [ ] Feedback component is enabled
- [ ] InitialDelay is set correctly
- [ ] PlayOnEnable is set appropriately
- [ ] No conflicting scripts disabling the feedback

#### Problem: Feedback Playing Too Late/Early
**Symptoms**: Feedback timing doesn't match action
**Causes**:
- Incorrect InitialDelay settings
- Animation timing mismatches
- Script execution order issues
**Solution**:
```csharp
public class TimedFeedback : MonoBehaviour
{
    public MMFeedbacks feedback;
    public float delay = 0.1f;
    
    public void PlayDelayedFeedback()
    {
        StartCoroutine(PlayFeedbackAfterDelay());
    }
    
    private IEnumerator PlayFeedbackAfterDelay()
    {
        yield return new WaitForSeconds(delay);
        feedback.PlayFeedbacks();
    }
}
```

### 3. Audio Feedback Issues

#### Problem: Audio Not Playing
**Symptoms**: Visual feedback works but no audio
**Causes**:
- Audio source not configured
- Audio clip missing
- Audio settings incorrect
**Troubleshooting**:
```csharp
public class AudioFeedbackChecker : MonoBehaviour
{
    public MMF_Sound soundFeedback;
    
    private void Start()
    {
        // Check audio source
        if (soundFeedback.SoundAudioSource == null)
        {
            Debug.LogWarning("Audio source not assigned!");
            soundFeedback.SoundAudioSource = GetComponent<AudioSource>();
        }
        
        // Check audio clip
        if (soundFeedback.SoundAudioClip == null)
        {
            Debug.LogWarning("Audio clip not assigned!");
        }
    }
}
```

#### Problem: Audio Volume Issues
**Symptoms**: Audio too loud/quiet or inconsistent
**Causes**:
- Volume settings incorrect
- Audio mixer issues
- Distance attenuation problems
**Solution**:
```csharp
public class AudioVolumeController : MonoBehaviour
{
    public MMF_Sound soundFeedback;
    public float masterVolume = 1.0f;
    
    private void Start()
    {
        // Set consistent volume
        soundFeedback.Volume = masterVolume;
        
        // Use audio mixer if available
        if (soundFeedback.SoundAudioMixerGroup != null)
        {
            // Configure mixer group settings
        }
    }
}
```

### 4. Visual Feedback Issues

#### Problem: Particle Effects Not Showing
**Symptoms**: Particle feedback doesn't appear
**Causes**:
- Particle system not configured
- Renderer issues
- Material problems
**Troubleshooting**:
```csharp
public class ParticleFeedbackChecker : MonoBehaviour
{
    public MMF_ParticleSystem particleFeedback;
    
    private void Start()
    {
        // Check particle system
        if (particleFeedback.ParticleSystem == null)
        {
            Debug.LogWarning("Particle system not assigned!");
        }
        
        // Check renderer
        var renderer = particleFeedback.ParticleSystem.GetComponent<ParticleSystemRenderer>();
        if (renderer == null)
        {
            Debug.LogWarning("Particle system renderer missing!");
        }
    }
}
```

#### Problem: Screen Shake Issues
**Symptoms**: Camera shake not working or too intense
**Causes**:
- Camera not assigned
- Shake parameters incorrect
- Cinemachine conflicts
**Solution**:
```csharp
public class CameraShakeController : MonoBehaviour
{
    public MMF_CameraShake cameraShake;
    public float maxShakeIntensity = 2.0f;
    
    private void Start()
    {
        // Clamp shake intensity
        cameraShake.RemapCameraShakeIntensityOne = Mathf.Min(
            cameraShake.RemapCameraShakeIntensityOne, 
            maxShakeIntensity
        );
        
        // Ensure camera is assigned
        if (cameraShake.ShakeCamera == null)
        {
            cameraShake.ShakeCamera = Camera.main;
        }
    }
}
```

### 5. Platform-Specific Issues

#### Problem: Mobile Performance Issues
**Symptoms**: Poor performance on mobile devices
**Causes**:
- Too many particle effects
- Complex audio processing
- High-frequency feedback loops
**Solution**:
```csharp
public class MobileFeedbackOptimizer : MonoBehaviour
{
    public MMFeedbacks[] feedbacks;
    public bool isMobile;
    
    private void Start()
    {
        isMobile = Application.platform == RuntimePlatform.Android || 
                   Application.platform == RuntimePlatform.IPhonePlayer;
        
        if (isMobile)
        {
            OptimizeForMobile();
        }
    }
    
    private void OptimizeForMobile()
    {
        foreach (var feedback in feedbacks)
        {
            // Reduce particle count
            var particleFeedbacks = feedback.GetComponentsInChildren<MMF_ParticleSystem>();
            foreach (var particle in particleFeedbacks)
            {
                // Reduce particle emission for mobile
            }
            
            // Disable expensive feedbacks
            var expensiveFeedbacks = feedback.GetComponentsInChildren<MMF_ScreenShake>();
            foreach (var shake in expensiveFeedbacks)
            {
                shake.enabled = false;
            }
        }
    }
}
```

#### Problem: Console Controller Vibration
**Symptoms**: Controller vibration not working
**Causes**:
- Input system not configured
- Platform-specific vibration issues
- Controller compatibility problems
**Solution**:
```csharp
public class ControllerVibrationFix : MonoBehaviour
{
    public MMF_ControllerVibration vibrationFeedback;
    
    private void Start()
    {
        // Check if vibration is supported
        if (!Gamepad.current.supportsVibration)
        {
            Debug.LogWarning("Controller vibration not supported!");
            vibrationFeedback.enabled = false;
        }
    }
}
```

## Debugging Tools

### 1. Feedback Debugger
```csharp
public class FeedbackDebugger : MonoBehaviour
{
    public MMFeedbacks targetFeedback;
    public bool enableDebug = true;
    
    private void OnEnable()
    {
        if (enableDebug)
        {
            targetFeedback.FeedbackStarted += OnFeedbackStarted;
            targetFeedback.FeedbackEnded += OnFeedbackEnded;
        }
    }
    
    private void OnDisable()
    {
        if (enableDebug)
        {
            targetFeedback.FeedbackStarted -= OnFeedbackStarted;
            targetFeedback.FeedbackEnded -= OnFeedbackEnded;
        }
    }
    
    private void OnFeedbackStarted()
    {
        Debug.Log($"Feedback started: {targetFeedback.name}");
    }
    
    private void OnFeedbackEnded()
    {
        Debug.Log($"Feedback ended: {targetFeedback.name}");
    }
}
```

### 2. Performance Profiler
```csharp
public class FeedbackProfiler : MonoBehaviour
{
    public MMFeedbacks[] feedbacksToProfile;
    public bool enableProfiling = true;
    
    private Dictionary<string, float> feedbackTimes = new Dictionary<string, float>();
    
    private void Update()
    {
        if (enableProfiling && Input.GetKeyDown(KeyCode.P))
        {
            ProfileAllFeedbacks();
        }
    }
    
    private void ProfileAllFeedbacks()
    {
        foreach (var feedback in feedbacksToProfile)
        {
            var stopwatch = System.Diagnostics.Stopwatch.StartNew();
            feedback.PlayFeedbacks();
            stopwatch.Stop();
            
            feedbackTimes[feedback.name] = stopwatch.ElapsedMilliseconds;
        }
        
        foreach (var kvp in feedbackTimes)
        {
            Debug.Log($"{kvp.Key}: {kvp.Value}ms");
        }
    }
}
```

## Best Practices Checklist

### Before Implementation
- [ ] Define feedback requirements clearly
- [ ] Test feedback on target platform
- [ ] Consider performance implications
- [ ] Plan for accessibility needs

### During Implementation
- [ ] Use appropriate feedback types
- [ ] Set correct timing parameters
- [ ] Configure audio sources properly
- [ ] Test with different input methods

### After Implementation
- [ ] Profile performance on target devices
- [ ] Test with various gameplay scenarios
- [ ] Verify accessibility compliance
- [ ] Document feedback behavior

### Maintenance
- [ ] Regular performance monitoring
- [ ] Update feedback for new platforms
- [ ] Gather user feedback
- [ ] Keep documentation current

## Troubleshooting Flowchart

1. **Feedback not playing?**
   - Check GameObject active state
   - Verify component enabled
   - Check timing settings
   - Verify script execution order

2. **Performance issues?**
   - Profile feedback instances
   - Check for memory leaks
   - Optimize particle effects
   - Reduce feedback frequency

3. **Audio problems?**
   - Verify audio source setup
   - Check audio clip assignment
   - Test audio mixer settings
   - Verify volume levels

4. **Visual issues?**
   - Check particle system setup
   - Verify renderer configuration
   - Test material assignments
   - Check camera shake settings

---

*FEEL Pitfalls and Troubleshooting*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
