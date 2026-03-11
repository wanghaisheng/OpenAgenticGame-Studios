# FEEL (MMFeedbacks) Usage Patterns

## Overview
FEEL is a powerful feedback system that creates responsive game feel through coordinated visual, audio, and haptic feedback.

## Core Patterns

### 1. Impact Feedback Pattern
```csharp
// Basic impact feedback
public class ImpactFeedback : MonoBehaviour
{
    public MMFeedbacks impactFeedback;
    
    private void OnCollisionEnter(Collision collision)
    {
        // Play impact feedback
        impactFeedback.PlayFeedbacks();
    }
}
```

### 2. UI Button Feedback Pattern
```csharp
// UI button interaction feedback
public class UIButtonFeedback : MonoBehaviour, IPointerDownHandler, IPointerUpHandler
{
    public MMFeedbacks pressFeedback;
    public MMFeedbacks releaseFeedback;
    
    public void OnPointerDown(PointerEventData eventData)
    {
        pressFeedback.PlayFeedbacks();
    }
    
    public void OnPointerUp(PointerEventData eventData)
    {
        releaseFeedback.PlayFeedbacks();
    }
}
```

### 3. Character Movement Feedback Pattern
```csharp
// Character movement and action feedback
public class CharacterFeedback : MonoBehaviour
{
    public MMFeedbacks footstepFeedback;
    public MMFeedbacks jumpFeedback;
    public MMFeedbacks landFeedback;
    
    private void Update()
    {
        // Footstep feedback
        if (IsMoving && IsGrounded)
        {
            if (Time.time - lastFootstepTime > footstepInterval)
            {
                footstepFeedback.PlayFeedbacks();
                lastFootstepTime = Time.time;
            }
        }
    }
    
    public void Jump()
    {
        if (IsGrounded)
        {
            jumpFeedback.PlayFeedbacks();
            // Jump logic here
        }
    }
    
    private void OnCollisionEnter(Collision collision)
    {
        if (!IsGrounded && collision.relativeVelocity.y > landingThreshold)
        {
            landFeedback.PlayFeedbacks();
        }
    }
}
```

### 4. Weapon Feedback Pattern
```csharp
// Weapon firing and impact feedback
public class WeaponFeedback : MonoBehaviour
{
    public MMFeedbacks fireFeedback;
    public MMFeedbacks reloadFeedback;
    public MMFeedbacks emptyClipFeedback;
    
    public void FireWeapon()
    {
        if (HasAmmo)
        {
            fireFeedback.PlayFeedbacks();
            // Fire weapon logic
        }
        else
        {
            emptyClipFeedback.PlayFeedbacks();
        }
    }
    
    public void Reload()
    {
        reloadFeedback.PlayFeedbacks();
        // Reload logic here
    }
}
```

### 5. Environmental Feedback Pattern
```csharp
// Environmental interaction feedback
public class EnvironmentalFeedback : MonoBehaviour
{
    public MMFeedbacks breakFeedback;
    public MMFeedbacks collectFeedback;
    public MMFeedbacks activateFeedback;
    
    public void BreakObject()
    {
        breakFeedback.PlayFeedbacks();
        // Object destruction logic
    }
    
    public void CollectItem()
    {
        collectFeedback.PlayFeedbacks();
        // Item collection logic
    }
    
    public void ActivateObject()
    {
        activateFeedback.PlayFeedbacks();
        // Object activation logic
    }
}
```

## Advanced Patterns

### 1. Dynamic Feedback Intensity
```csharp
public class DynamicFeedback : MonoBehaviour
{
    public MMFeedbacks impactFeedback;
    public float minIntensity = 0.5f;
    public float maxIntensity = 2.0f;
    
    public void PlayDynamicImpact(float force)
    {
        // Calculate intensity based on force
        float intensity = Mathf.Lerp(minIntensity, maxIntensity, force / maxForce);
        
        // Set feedback intensity
        var feedbacks = impactFeedback.FeedbacksList;
        foreach (var feedback in feedbacks)
        {
            if (feedback is MMF_CameraShake cameraShake)
            {
                cameraShake.RemapCameraShakeIntensityZero = intensity;
                cameraShake.RemapCameraShakeIntensityOne = intensity;
            }
        }
        
        impactFeedback.PlayFeedbacks();
    }
}
```

### 2. Sequential Feedback Chains
```csharp
public class SequentialFeedback : MonoBehaviour
{
    public MMFeedbacks[] feedbackSequence;
    private int currentFeedbackIndex = 0;
    
    public void PlaySequence()
    {
        if (currentFeedbackIndex < feedbackSequence.Length)
        {
            feedbackSequence[currentFeedbackIndex].PlayFeedbacks();
            currentFeedbackIndex++;
            
            // Auto-advance sequence
            if (currentFeedbackIndex < feedbackSequence.Length)
            {
                StartCoroutine(PlayNextAfterDelay());
            }
        }
    }
    
    private IEnumerator PlayNextAfterDelay()
    {
        yield return new WaitForSeconds(0.1f);
        PlaySequence();
    }
    
    public void ResetSequence()
    {
        currentFeedbackIndex = 0;
    }
}
```

### 3. Conditional Feedback
```csharp
public class ConditionalFeedback : MonoBehaviour
{
    public MMFeedbacks normalFeedback;
    public MMFeedbacks criticalFeedback;
    public MMFeedbacks missFeedback;
    
    public void ProcessHit(bool isCritical, bool isMiss)
    {
        if (isMiss)
        {
            missFeedback.PlayFeedbacks();
        }
        else if (isCritical)
        {
            criticalFeedback.PlayFeedbacks();
        }
        else
        {
            normalFeedback.PlayFeedbacks();
        }
    }
}
```

## Performance Optimization Patterns

### 1. Object Pooling for Feedback
```csharp
public class PooledFeedback : MonoBehaviour
{
    public GameObject feedbackPrefab;
    public int poolSize = 10;
    
    private Queue<GameObject> feedbackPool = new Queue<GameObject>();
    
    private void Start()
    {
        // Initialize pool
        for (int i = 0; i < poolSize; i++)
        {
            GameObject obj = Instantiate(feedbackPrefab);
            obj.SetActive(false);
            feedbackPool.Enqueue(obj);
        }
    }
    
    public void PlayPooledFeedback(Vector3 position)
    {
        if (feedbackPool.Count > 0)
        {
            GameObject feedback = feedbackPool.Dequeue();
            feedback.transform.position = position;
            feedback.SetActive(true);
            
            // Return to pool after delay
            StartCoroutine(ReturnToPool(feedback, 1.0f));
        }
    }
    
    private IEnumerator ReturnToPool(GameObject obj, float delay)
    {
        yield return new WaitForSeconds(delay);
        obj.SetActive(false);
        feedbackPool.Enqueue(obj);
    }
}
```

### 2. Distance-Based Feedback
```csharp
public class DistanceFeedback : MonoBehaviour
{
    public MMFeedbacks nearFeedback;
    public MMFeedbacks farFeedback;
    public float distanceThreshold = 10.0f;
    
    public void PlayDistanceFeedback(Vector3 targetPosition)
    {
        float distance = Vector3.Distance(transform.position, targetPosition);
        
        if (distance < distanceThreshold)
        {
            nearFeedback.PlayFeedbacks();
        }
        else
        {
            farFeedback.PlayFeedbacks();
        }
    }
}
```

## Platform-Specific Patterns

### 1. Mobile Touch Feedback
```csharp
public class MobileFeedback : MonoBehaviour
{
    public MMFeedbacks touchFeedback;
    public MMFeedbacks swipeFeedback;
    
    private void Update()
    {
        if (Input.touchCount > 0)
        {
            Touch touch = Input.GetTouch(0);
            
            if (touch.phase == TouchPhase.Began)
            {
                touchFeedback.PlayFeedbacks();
            }
            else if (touch.phase == TouchPhase.Moved)
            {
                swipeFeedback.PlayFeedbacks();
            }
        }
    }
}
```

### 2. Console Controller Feedback
```csharp
public class ControllerFeedback : MonoBehaviour
{
    public MMFeedbacks buttonPressFeedback;
    public MMFeedbacks vibrationFeedback;
    
    private void Update()
    {
        // Button press feedback
        if (Input.GetButtonDown("Jump"))
        {
            buttonPressFeedback.PlayFeedbacks();
            
            // Controller vibration
            if (Gamepad.current != null)
            {
                Gamepad.current.SetMotorSpeeds(0.5f, 0.5f);
                StartCoroutine(StopVibration(0.2f));
            }
        }
    }
    
    private IEnumerator StopVibration(float duration)
    {
        yield return new WaitForSeconds(duration);
        if (Gamepad.current != null)
        {
            Gamepad.current.SetMotorSpeeds(0f, 0f);
        }
    }
}
```

## Best Practices

### 1. Feedback Design Principles
- **Immediate**: Feedback should be instantaneous
- **Clear**: Feedback should clearly communicate the action
- **Appropriate**: Feedback intensity should match action importance
- **Consistent**: Similar actions should have similar feedback

### 2. Performance Guidelines
- Limit concurrent feedback instances
- Use object pooling for frequently spawned feedback
- Optimize feedback for target platform
- Profile feedback performance regularly

### 3. Accessibility Considerations
- Provide visual alternatives to audio feedback
- Allow feedback intensity adjustments
- Support different input methods
- Consider colorblind-friendly visual feedback

---

*FEEL Usage Patterns*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
