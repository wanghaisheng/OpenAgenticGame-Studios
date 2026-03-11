# DOTween API 快速参考

本文件提供 DOTween 核心API的快速参考信息。

## DOTween 核心类

### DOTween 静态类

全局控制和管理 DOTween 系统。

```csharp
// 初始化
DOTween.Init(bool autoKillOnCompletion = true, bool safeMode = true, LogBehaviour logBehaviour = LogBehaviour.Default)

// 杀死所有 tween
DOTween.KillAll()
DOTween.Kill(object targetOrId)

// 清空所有 tween
DOTween.Clear()
DOTween.Clear(bool destroyTweens)

// 暂停/播放
DOTween.PauseAll()
DOTween.PlayAll()

// 时间控制
DOTween.timeScale = 1f // 全局时间缩放
DOTween.useUnscaledTime = false // 是否使用 unscaled time

// 检查状态
DOTween.IsTweening(object targetOrId)
DOTween.IsTweening()
```

### Tween 和 Tweener

- **Tween**: 所有动画的基类 (struct)
- **Tweener**: 单个值的动画 tween，继承自 Tween

```csharp
// 控制方法
tween.Pause()
tween.Play()
tween.Stop()
tween.Rewind()
tween.Restart()
tween.Flip()
tween.Kill(bool complete = false)
tween.Complete()

// 状态检查
tween.IsActive() // 是否活跃
tween.IsPlaying() // 是否正在播放
twin.IsBackwards() // 是否反向播放

// 获取进度
tween.Elapsed() // 已过去的时间
tween.ElapsedPercentage(bool includeLoops = true) // 已过去百分比 (0-1)
tween.Position() // 当前位置 (0-1)

// 设置选项
tween.SetDelay(float delay)
tween.SetLoops(int loops, LoopType loopType = LoopType.Restart)
tween.SetEase(Ease easeType | AnimationCurve easeCurve)
tween.SetUpdate(UpdateType updateType, bool isIndependentUpdate = false)
tween.SetRecyclable(bool value)
tween.SetAutoKill(bool autoKillOnCompletion = true)
tween.SetRelative(bool isRelative = true)
tween.SetId(object id)
tween.SetTarget(object target)
tween.SetSpeedBased()
```

## Ease 缓动类型

```csharp
public enum Ease {
    // 基础
    Linear,
    InSine, OutSine, InOutSine,
    InQuad, OutQuad, InOutQuad,
    InCubic, OutCubic, InOutCubic,
    InQuart, OutQuart, InOutQuart,
    InQuint, OutQuint, InOutQuint,
    InExpo, OutExpo, InOutExpo,
    InCirc, OutCirc, InOutCirc,

    // 特殊效果
    InElastic, OutElastic, InOutElastic,
    InBack, OutBack, InOutBack,
    InBounce, OutBounce, InOutBounce,

    // Flash
    Flash,

    // 自定义
    INTERNAL_Zero,
    INTERNAL_Custom
}
```

## LoopType 循环类型

```csharp
public enum LoopType {
    Restart,  // 从头重新开始
    Yoyo,     // 往返动画
    Incremental // 每次循环递增 endValue
}
```

## UpdateType 更新类型

```csharp
public enum UpdateType {
    Normal,     // Update (使用 Time.deltaTime)
    Late,       // LateUpdate
    Fixed       // FixedUpdate
}
```

## RotateMode 旋转模式

```csharp
public enum RotateMode {
    Fast,              // 最快 (360° = 0°)
    FastBeyond360,     // 允许超过 360°
    WorldAxisAdd,      // 在世界轴上旋转增量
    LocalAxisAdd       // 在本地轴上旋转增量
}
```

## 常用扩展方法

### Transform 扩展

```csharp
// 位置
DOMove(Vector3 to, float duration, bool snapping = false)
DOMoveX(float to, float duration, bool snapping = false)
DOMoveY(float to, float duration, bool snapping = false)
DOMoveZ(float to, float duration, bool snapping = false)
DOLocalMove(Vector3 to, float duration, bool snapping = false)
DOLocalMoveX(float to, float duration, bool snapping = false)
DOLocalMoveY(float to, float duration, bool snapping = false)
DOLocalMoveZ(float to, float duration, bool snapping = false)

// 跳跃
DOJump(Vector3 targetPosition, float jumpPower, int numJumps, float duration, bool snapping = false)

// 旋转
DORotate(Vector3 to, float duration, RotateMode mode = RotateMode.Fast)
DORotateQuaternion(Quaternion to, float duration)
DOLocalRotate(Vector3 to, float duration, RotateMode mode = RotateMode.Fast)

// 缩放
DOScale(float to, float duration)
DOScale(Vector3 to, float duration)
DOScaleX(float to, float duration)
DOScaleY(float to, float duration)
DOScaleZ(float to, float duration)

// Punch (弹性冲击)
DOPunchPosition(Vector3 punch, float duration, int vibrato, float elasticity, bool snapping = false)
DOPunchRotation(Vector3 punch, float duration, int vibrato, float elasticity)
DOPunchScale(Vector3 punch, float duration, int vibrato, float elasticity)

// Shake (震动)
DOShakePosition(float duration, float/Vector3 strength, int vibrato, float randomness, bool snapping = false, bool fadeOut = true)
DOShakeRotation(float duration, float/Vector3 strength, int vibrato, float randomness, bool fadeOut = true)
DOShakeScale(float duration, float/Vector3 strength, int vibrato, float randomness, bool fadeOut = true)

// 路径
DOPath(Vector3[] path, float duration, PathType pathType = PathType.Linear, PathMode pathMode = PathMode.Full3D, int resolution = 10, Color? gizmoColor = null)
DOLocalPath(Vector3[] path, float duration, PathType pathType = PathType.Linear, PathMode pathMode = PathMode.Full3D, int resolution = 10, Color? gizmoColor = null)
```

### RectTransform 扩展

```csharp
// 锚点位置
DOAnchorPos(Vector2 to, float duration, bool snapping = false)
DOAnchorPosX(float to, float duration, bool snapping = false)
DOAnchorPosY(float to, float duration, bool snapping = false)
DOAnchorPos3D(Vector3 to, float duration, bool snapping = false)
DOAnchorPos3DX(float to, float duration, bool snapping = false)
DOAnchorPos3DY(float to, float duration, bool snapping = false)
DOAnchorPos3DZ(float to, float duration, bool snapping = false)

// 尺寸
DOSizeDelta(Vector2 to, float duration)

// Punch 和 Shake
DOPunchAnchorPos(Vector2 punch, float duration, int vibrato, float elasticity, bool snapping = false)
DOShakeAnchorPos(float duration, float/Vector2 strength, int vibrato, float randomness, bool snapping = false, bool fadeOut = true)
```

### UI 组件扩展

```csharp
// Image
DOFade(float to, float duration)
DOColor(Color to, float duration)

// CanvasGroup
DOFade(float to, float duration)

// Text (Legacy)
DOFade(float to, float duration)
DOColor(Color to, float duration)
DOText(string to, float duration, bool richTextEnabled = true, ScrambleMode scrambleMode = ScrambleMode.None, string scrambleChars = null)

// Outline
DOFade(float to, float duration)
DOScale(Vector2 to, float duration)
```

### Material 扩展

```csharp
DOColor(Color to, float duration)
DOColor(Color to, string property, float duration)
DOFade(float to, float duration)
DOFade(float to, string property, float duration)
DOFloat(float to, string property, float duration)
DOVector(Vector4 to, string property, float duration)
DOGradientColor(Gradient to, string property, float duration)
```

### Camera 扩展

```csharp
DOOrthoSize(float to, float duration)
DOFieldOfView(float to, float duration)
DOColor(Color to, float duration)
DOAspect(float to, float duration)
DOShakePosition(float duration, float/Vector3 strength, int vibrato, float randomness, bool fadeOut = true)
DOShakeRotation(float duration, float/Vector3 strength, int vibrato, float randomness, bool fadeOut = true)
```

### TextMeshPro 扩展

```csharp
DOFade(float to, float duration)
DOColor(Color to, float duration)
DOFontSize(float to, float duration)
DOMaxVisibleCharacters(int to, float duration)
DOFaceColor(Color to, float duration)
DOOutlineColor(Color to, float duration)
DOGlowColor(Color to, float duration)
```

### Light 扩展

```csharp
DOColor(Color to, float duration)
DOIntensity(float to, float duration)
DOShadowStrength(float to, float duration)
DORange(float to, float duration)
DOSpotAngle(float to, float duration)
```

### AudioSource 扩展

```csharp
DOFade(float to, float duration)
DOPitch(float to, float duration)
DOVolume(float to, float duration) // 同 DOFade
```

### Rigidbody 扩展

```csharp
DOMove(Vector3 to, float duration, bool snapping = false)
DORotate(Vector3 to, float duration, RotateMode mode = RotateMode.Fast)
DOMoveX/Y/Z(float to, float duration, bool snapping = false)

// 注意: Rigidbody 动画会在 FixedUpdate 中执行
```

### Rigidbody2D 扩展

```csharp
DOMove(Vector2 to, float duration, bool snapping = false)
DORotate(float to, float duration, RotateMode mode = RotateMode.Fast)
DOMoveX(float to, float duration, bool snapping = false)
DOMoveY(float to, float duration, bool snapping = false)
```

## Sequence 方法

```csharp
// 创建序列
Sequence seq = DOTween.Sequence();

// 添加动画
seq.Append(Tween tween)
seq.Join(Tween tween)
seq.Insert(float atPosition, Tween tween)
seq.AppendCallback(TweenCallback callback)
seq.InsertCallback(float atPosition, TweenCallback callback)
seq.AppendInterval(float interval)
seq.InsertInterval(float atPosition, float interval)

// 预设方法
seq.Prepend(Tween tween)
seq.PrependCallback(TweenCallback callback)
seq.PrependInterval(float interval)

// 设置
seq.SetDelay(float delay)
seq.SetLoops(int loops, LoopType loopType = LoopType.Restart)
seq.SetEase(Ease easeType | AnimationCurve easeCurve)
seq.SetUpdate(UpdateType updateType, bool isIndependentUpdate = false)
seq.SetRecyclable(bool value)
seq.SetAutoKill(bool autoKillOnCompletion = true)
seq.SetId(object id)
seq.SetTarget(object target)
seq.SetSpeedBased()
seq.SetAs(Tween tween) // 复制另一个 tween 的设置

// 播放控制
seq.Pause()
seq.Play()
seq.Restart()
seq.Rewind()
seq.Flip()
seq.Kill(bool complete = false)
seq.Complete()

// 状态
seq.IsActive()
seq.IsPlaying()
seq.IsBackwards()
seq.Elapsed()
seq.ElapsedPercentage(bool includeLoops)
seq.Position()
```

## PathType 和 PathMode

```csharp
public enum PathType {
    Linear,      // 直线连接点
    CatmullRom   // 平滑曲线 (默认)
}

public enum PathMode {
    Full3D,      // 完全 3D 路径
    IgnoreZ,     // 忽略 Z 轴
    Sidescroller2D // 2D 横版游戏路径
}
```

## ScrambleMode

```csharp
public enum ScrambleMode {
    None,        // 无乱码
    All,         // 所有字符
    Upper,       // 大写字母
    Lower,       // 小写字母
    Numerals,    // 数字
    Custom       // 自定义
}
```

## DOTween 设置

```csharp
// 全局设置
DOTween.SetTweensCapacity(int tweenersCapacity, int sequencesCapacity)
DOTween.SetMode(bool independentTime, bool useSafeMode)
DOTween.Debug.LogBehaviour = LogBehaviour.Default | Verbose | OnlyErrors

// 错误日志
public enum LogBehaviour {
    Default,   // 默认
    Verbose,   // 详细
    OnlyErrors // 仅错误
}

// 安全模式
// 启用后，如果单例被销毁，tween 不会报错
DOTween.Init(useSafeMode: true)
```

## 回调方法

```csharp
// Tween 回调
tween.OnComplete(TweenCallback callback)
tween.OnComplete(TweenCallback callback, bool returnToCachedIfNotActive)
tween.OnKill(TweenCallback callback)
tween.OnPlay(TweenCallback callback)
tween.OnPause(TweenCallback callback)
tween.OnRewind(TweenCallback callback)
tween.OnStart(TweenCallback callback)
tween.OnUpdate(TweenCallback callback)
tween.OnUpdate(TweenCallback<float> callback) // 带进度参数
tween.OnWaypointChange(TweenCallback<int> callback) // 路径回调

// Sequence 回调
seq.OnComplete(TweenCallback callback)
seq.OnKill(TweenCallback callback)
seq.OnPlay(TweenCallback callback)
seq.OnPause(TweenCallback callback)
seq.OnRewind(TweenCallback callback)
seq.OnStart(TweenCallback callback)
seq.OnStepComplete(TweenCallback callback)
seq.OnUpdate(TweenCallback callback)
```

## 实用工具方法

```csharp
// 延迟调用
DOTween.DelayedCall(float delay, TweenCallback callback, bool ignoreTimeScale = false)

// To (自定义值动画)
DOTween.To(getter, setter, to, float duration)

// 示例
DOTween.To(() => myValue, x => myValue = x, 10f, 1f);

// 带缓动
DOTween.To(getter, setter, to, float duration, bool snapping = false)
```

## 性能优化建议

1. **设置 Tweens 容量**
   ```csharp
   // 初始化时设置
   DOTween.SetTweensCapacity(200, 50);
   ```

2. **使用 SetRecyclable**
   ```csharp
   tween.SetRecyclable(true); // 允许 tween 被回收重用
   ```

3. **及时清理**
   ```csharp
   // 场景切换时
   DOTween.Clear();
   ```

4. **使用 SetAutoKill**
   ```csharp
   tween.SetAutoKill(true); // 完成后自动杀死
   ```

5. **避免在 Update 中创建 Tween**
   ```csharp
   // ❌ 错误
   void Update() {
       transform.DOMoveX(target, 1f);
   }

   // ✅ 正确
   void Start() {
       _moveTween = transform.DOMoveX(target, 1f);
   }
   ```

---

*此文档基于 DOTween 官方文档整理: https://dotween.demigiant.com/documentation.php*