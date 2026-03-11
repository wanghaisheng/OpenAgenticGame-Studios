---
name: prime-tween-unity
description: PrimeTween Unity 高性能动画库。用于补间动画、UI 过渡、相机震动、序列以及 Unity 中任何零内存分配的动画需求。
---

# PrimeTween Unity Skill

PrimeTween 是一个高性能、零内存分配的 Unity 动画库。用一行代码实现任何动画，支持 Inspector 调试、复杂序列、相机震动等功能。

## 何时使用此 Skill

在以下情况下触发此 Skill ：
- PrimeTween 动画库 (com.kyrylokuzyk.primetween)
- UI 动画和过渡效果 (UI animations and transitions)
- Transform 动画 (位置、旋转、缩放)
- Material 和 Color 动画
- 相机震动和屏幕特效 (Camera shake and screen effects)
- 动画序列和时序控制 (Animation sequences)
- 延迟执行和回调 (Delays and callbacks)
- TextMeshPro 文字打字机效果
- 从 DOTween 迁移到 PrimeTween

## 快速参考

### Hello World - 基础动画

```csharp
using PrimeTween;

// 位置动画 - 将 transform.position.y 从当前值动画到 10，持续 1 秒，使用 Ease.InOutSine 缓动
Tween.PositionY(transform, endValue: 10, duration: 1, ease: Ease.InOutSine);

// 旋转动画 - 将 transform 从当前旋转旋转到 (0, 90, 0)，持续 1 秒
Tween.Rotation(transform, endValue: Quaternion.Euler(0, 90, 0), duration: 1);

// 欧拉角旋转 - 绕 Y 轴旋转 360 度
Tween.EulerAngles(transform, startValue: Vector3.zero, endValue: new Vector3(0, 360), duration: 1);

// 缩放动画 - 将对象缩放到 2 倍大小
Tween.Scale(transform, endValue: 2f, duration: 0.5f);

// UI 透明度动画
Tween.Alpha(image, endValue: 0f, duration: 1f);
```

### 1. 常用动画类型

#### Transform 动画

```csharp
using PrimeTween;

// Position (世界坐标)
Tween.Position(transform, endValue: new Vector3(10, 0, 5), duration: 1f);
Tween.PositionX(transform, endValue: 10f, duration: 1f);
Tween.PositionY(transform, endValue: 5f, duration: 1f);
Tween.PositionZ(transform, endValue: 0f, duration: 1f);

// Local Position (本地坐标)
Tween.LocalPosition(transform, endValue: Vector3.zero, duration: 1f);
Tween.LocalPositionX/Y/Z(transform, endValue: 0f, duration: 1f);

// Rotation (四元数旋转)
Tween.Rotation(transform, endValue: Quaternion.Euler(0, 90, 0), duration: 1f);
Tween.LocalRotation(transform, endValue: Quaternion.identity, duration: 1f);

// EulerAngles (欧拉角旋转 - 支持超过 180 度的旋转)
Tween.EulerAngles(transform, endValue: new Vector3(0, 360, 0), duration: 1f);
Tween.LocalEulerAngles(transform, endValue: new Vector3(360, 0, 0), duration: 1f);

// Scale (缩放)
Tween.Scale(transform, endValue: 2f, duration: 0.5f); // 均匀缩放
Tween.Scale(transform, endValue: new Vector3(2, 1, 0.5f), duration: 0.5f); // 非均匀缩放
```

#### UI 动画

```csharp
using PrimeTween;
using UnityEngine.UI;

// UI 位置和大小
Tween.UIAnchoredPosition(rectTransform, endValue: Vector2.zero, duration: 0.5f);
Tween.UIAnchoredPositionX(rectTransform, endValue: 100f, duration: 0.5f);
Tween.UISizeDelta(rectTransform, endValue: new Vector2(200, 100), duration: 0.5f);

// UI 颜色和透明度
Tween.Color(image, endValue: Color.red, duration: 1f);
Tween.Alpha(image, endValue: 0.5f, duration: 1f);

// CanvasGroup 透明度
Tween.Alpha(canvasGroup, endValue: 1f, duration: 0.3f);
```

#### Material 动画

```csharp
using PrimeTween;

// Material 颜色
Tween.Color(material, endValue: Color.blue, duration: 1f);
Tween.Alpha(material, endValue: 0f, duration: 1f);

// 自定义属性颜色
Tween.Color(material, "_EmissionColor", Color.white, duration: 1f);
```

#### 相机动画

```csharp
using PrimeTween;

// 相机属性
Tween.OrthoSize(camera, endValue: 5f, duration: 1f);
Tween.FieldOfView(camera, endValue: 60f, duration: 1f);
Tween.BackgroundColor(camera, endValue: Color.black, duration: 2f);

// 相机震动
Tween.ShakeCamera(camera, strengthFactor: 0.5f); // 中等强度震动
Tween.ShakeCamera(camera, strengthFactor: 1.0f, duration: 0.5f, frequency: 10); // 强烈震动
```

#### 文字动画

```csharp
using PrimeTween;
using TMPro;

// TextMeshPro 颜色和透明度
Tween.Color(textMeshPro, endValue: Color.yellow, duration: 1f);
Tween.Alpha(textMeshPro, endValue: 0f, duration: 1f);

// 字体大小
Tween.FontSize(textMeshPro, endValue: 48f, duration: 0.5f);

// 打字机效果 (简单)
textMeshPro.ForceMeshUpdate();
int charCount = textMeshPro.textInfo.characterCount;
Tween.TextMaxVisibleCharacters(textMeshPro, 0, charCount, duration: 2f, ease: Ease.Linear);
```

### 2. 震动和冲击效果

```csharp
using PrimeTween;

// 位置震动
Tween.ShakeLocalPosition(transform, strength: new Vector3(0, 1, 0), duration: 1f, frequency: 10);

// 旋转震动
Tween.ShakeLocalRotation(transform, strength: new Vector3(0, 0, 15), duration: 1f, frequency: 10);

// 缩放震动
Tween.ShakeLocalScale(transform, strength: Vector3.one * 0.5f, duration: 0.5f, frequency: 15);

// Punch 效果 (单向冲击)
Tween.PunchLocalPosition(transform, strength: transform.up * 2, duration: 0.5f, frequency: 10);

// 自定义震动
var shakeSettings = new ShakeSettings(
    strength: new Vector3(1, 1, 0),
    duration: 1f,
    frequency: 10,
    easeBetweenShakes: Ease.OutQuad
);
Tween.ShakeCustom(this, startValue: transform.localPosition, shakeSettings,
    (target, val) => transform.localPosition = val);
```

### 3. 回调和延迟

```csharp
using PrimeTween;

// OnComplete 回调
Tween.Position(transform, endValue: new Vector3(10, 0), duration: 1f)
    .OnComplete(() => Debug.Log("Animation completed!"));

// 零分配回调 (推荐)
Tween.Position(transform, endValue: new Vector3(10, 0), duration: 1f)
    .OnComplete(target: this, (target) => target.SomeMethod());

// 延迟执行
Tween.Delay(duration: 1f, () => Debug.Log("Executed after 1 second"));

// 延迟调用方法 (零分配)
Tween.Delay(this, duration: 1f, target => target.SomeMethod());

// 带延迟的动画
Tween.Scale(transform, endValue: 0f, duration: 1f, endDelay: 0.5f)
    .OnComplete(target: this, target => Destroy(target.gameObject));
```

### 4. 循环动画

```csharp
using PrimeTween;

// 无限循环
Tween.PositionY(transform, endValue: 10, duration: 0.5f, cycles: -1, cycleMode: CycleMode.Yoyo);

// 指定循环次数
Tween.Scale(transform, endValue: 2f, duration: 0.5f, cycles: 3, cycleMode: CycleMode.Yoyo);

// CycleMode 选项:
// - Restart: 从头重新开始
// - Yoyo: 往返动画
// - Incremental: 每次循环递增 endValue
// - Rewind: 时间倒流
```

### 5. 序列动画

```csharp
using PrimeTween;

// 基础序列
var sequence = Sequence.Create()
    .Chain(Tween.PositionX(transform, 10f, duration: 1f))
    .Chain(Tween.Scale(transform, 2f, duration: 0.5f))
    .Chain(Tween.Rotation(transform, new Vector3(0, 90, 0), duration: 0.5f));

// 并行动画 (Group)
Sequence.Create()
    .Group(Tween.PositionX(transform, 10f, duration: 1f))
    .Group(Tween.Scale(transform, 2f, duration: 1f))
    .Chain(Tween.Rotation(transform, new Vector3(0, 90, 0), duration: 0.5f));

// 复杂序列
Sequence.Create(cycles: 2, CycleMode.Yoyo)
    .Group(Tween.PositionX(transform, 10f, duration: 1.5f))
    .Group(Tween.Scale(transform, 2f, duration: 0.5f, startDelay: 1f))
    .Chain(Tween.Rotation(transform, new Vector3(0f, 0f, 45f), duration: 1f))
    .ChainDelay(1f)
    .ChainCallback(this, target => Debug.Log("Animation completed"))
    .Insert(atTime: 0.5f, Tween.Color(image, Color.red, duration: 0.5f));

// 序列回调
Sequence.Create()
    .Chain(Tween.PositionX(transform, 10f, 1f))
    .ChainCallback(this, target => target.OnPositionComplete())
    .Chain(Tween.Scale(transform, 2f, 0.5f));
```

### 6. 协程和异步

```csharp
using PrimeTween;
using System.Collections;

// 协程
IEnumerator CoroutineExample() {
    Tween.PositionX(transform, endValue: 10f, duration: 1.5f);
    yield return Tween.Scale(transform, 2f, 0.5f, startDelay: 1f).ToYieldInstruction();
    yield return Tween.Rotation(transform, new Vector3(0f, 0f, 45f), 1f).ToYieldInstruction();
    yield return Tween.Delay(1f).ToYieldInstruction();
    Debug.Log("Sequence completed");
}

// Async/Await
async void AsyncExample() {
    Tween.PositionX(transform, endValue: 10f, duration: 1.5f);
    await Tween.Scale(transform, endValue: 2f, duration: 0.5f, startDelay: 1f);
    await Tween.Rotation(transform, endValue: new Vector3(0f, 0f, 45f), duration: 1f);
    await Tween.Delay(1f);
    Debug.Log("Sequence completed");
}
```

### 7. 控制动画

```csharp
using PrimeTween;

// 创建并存储 tween 引用
Tween tween = Tween.LocalPositionX(transform, endValue: 1.5f, duration: 1f);

// 检查是否存活
if (tween.isAlive) {
    Debug.Log($"Animation is running. Elapsed: {tween.elapsedTime}");
}

// 停止动画
tween.Stop();
Tween.StopAll(onTarget: transform);

// 完成动画
tween.Complete();
Tween.CompleteAll(onTarget: transform);

// 暂停/恢复
tween.isPaused = true;
Tween.SetPausedAll(true, onTarget: transform);
Tween.SetPausedAll(false, onTarget: transform);

// 手动设置进度
tween.elapsedTime = 0.5f;
tween.progress = 0.5f;
tween.timeScale = 2f;

// 设置剩余循环次数
tween.SetRemainingCycles(3);
tween.SetRemainingCycles(stopAtEndValue: true);
```

### 8. Inspector 集成

```csharp
using PrimeTween;
using UnityEngine;

public class AnimationExample : MonoBehaviour {
    // 在 Inspector 中配置动画参数
    [SerializeField] TweenSettings<float> positionYTweenSettings;
    [SerializeField] TweenSettings<Vector3> rotationTweenSettings;
    [SerializeField] TweenSettings<Color> colorTweenSettings;
    [SerializeField] ShakeSettings cameraShakeSettings;

    public void PlayAnimation() {
        // 使用 Inspector 中配置的设置
        Tween.PositionY(transform, positionYTweenSettings);
        Tween.Rotation(transform, rotationTweenSettings);
        Tween.Color(material, colorTweenSettings);
        Tween.ShakeCamera(camera, cameraShakeSettings);
    }

    // 示例：使用 WithDirection 方法
    [SerializeField] RectTransform window;
    [SerializeField] TweenSettings<float> windowAnimationSettings;

    public void SetWindowOpened(bool isOpened) {
        Tween.UIAnchoredPositionY(window,
            windowAnimationSettings.WithDirection(toEndValue: isOpened));
    }
}
```

### 9. 自定义动画

```csharp
using PrimeTween;

// 自定义 float 动画
float myFloatField;
Tween.Custom(0f, 10f, duration: 1f,
    onValueChange: newVal => myFloatField = newVal);

// 零分配方式
Tween.Custom(this, 0f, 10f, duration: 1f,
    (target, newVal) => target.myFloatField = newVal);

// 自定义 Color 动画
Color myColor;
Tween.Custom(Color.white, Color.black, duration: 1f,
    onValueChange: newVal => myColor = newVal);

// 自定义 Vector3 动画
Vector3 myVector;
Tween.Custom(Vector3.zero, Vector3.one, duration: 1f,
    onValueChange: newVal => myVector = newVal);

// 使用 TweenSettings
[SerializeField] TweenSettings<float> customTweenSettings;

void AnimateCustomField() {
    Tween.Custom(customTweenSettings,
        onValueChange: newVal => myFloatField = newVal);
}
```

### 10. 缓动函数

```csharp
using PrimeTween;

// 使用标准 Ease
Tween.PositionY(transform, 10f, 1f, ease: Ease.InOutSine);
Tween.Scale(transform, 2f, 0.5f, ease: Ease.OutBounce);
Tween.Alpha(image, 0f, 1f, ease: Ease.InQuad);

// 使用 AnimationCurve
AnimationCurve customCurve = new AnimationCurve();
customCurve.AddKey(0, 0);
customCurve.AddKey(1, 1);
Tween.PositionY(transform, 10f, 1f, customCurve);

// 参数化缓动
Tween.PositionY(transform, 10f, 1f, Easing.BounceExact(1f)); // 精确反弹 1 米
Tween.PositionY(transform, 10f, 1f, Easing.Overshoot(2f));    // 强度 2 的过冲
Tween.PositionY(transform, 10f, 1f, Easing.Elastic(1f, 0.3f)); // 弹性效果
```

### 11. Update 类型

```csharp
using PrimeTween;

// Update (默认)
Tween.PositionX(transform, 10f, 1f, new TweenSettings(duration: 1f, updateType: UpdateType.Update));

// LateUpdate (适用于相机跟随等)
Tween.PositionX(transform, 10f, 1f, new TweenSettings(duration: 1f, updateType: UpdateType.LateUpdate));

// FixedUpdate (适用于物理相关动画)
Tween.PositionX(transform, 10f, 1f, new TweenSettings(duration: 1f, updateType: UpdateType.FixedUpdate));

// Sequence UpdateType
Sequence.Create(updateType: UpdateType.LateUpdate);
```

### 12. 速度基础动画

```csharp
using PrimeTween;

// 速度基础动画 (duration 会自动计算)
Tween.PositionAtSpeed(transform, endValue: targetPosition, speed: 10f);
Tween.LocalPositionAtSpeed(transform, endValue: targetPosition, speed: 5f);

// 链接速度基础动画需要指定 startValue
Vector3 midPos = new Vector3(5, 0, 0);
Vector3 endPos = new Vector3(10, 0, 0);
Tween.LocalPositionAtSpeed(transform, endValue: midPos, speed: 5f)
    .Chain(Tween.LocalPositionAtSpeed(transform, startValue: midPos, endValue: endPos, speed: 5f));
```

### 13. TimeScale 控制

```csharp
using PrimeTween;

// 动画独立 timeScale
Tween tween = Tween.PositionY(transform, 10f, 1f);
tween.timeScale = 2f; // 2 倍速播放

// 动画 timeScale 动画
Tween tween = Tween.PositionY(transform, 10f, 1f);
Tween.TweenTimeScale(tween, 2f, 0.5f); // 将 timeScale 从 1 动画到 2

// 全局 Time.timeScale 动画
Tween.GlobalTimeScale(0.5f, 1f); // 慢动作效果
```

### 14. DOTween 迁移

```csharp
// 启用 DOTween Adapter
// 在 Project Settings/Player/Script Compilation 中添加: PRIME_TWEEN_DOTWEEN_ADAPTER

// 替换 using
// using DG.Tweening;
using PrimeTween;

// API 映射:
// transform.DOMove(...)          -> Tween.Position(transform, ...)
// uiImage.DOFade(...)            -> Tween.Alpha(uiImage, ...)
// material.DOColor(...)          -> Tween.Color(material, ...)
// transform.DOShakePosition(...) -> Tween.ShakeLocalPosition(transform, ...)
// tween.SetEase(...)             -> Tween.Position(..., ease: ...)
// tween.SetLoops(...)            -> Tween.Position(..., cycles: ..., cycleMode: ...)
// tween.Kill(false)              -> tween.Stop()
// tween.Kill(true)               -> tween.Complete()
// DOVirtual.DelayedCall()        -> Tween.Delay()
// DOTween.To()                   -> Tween.Custom()
// DOTween.Sequence()             -> Sequence.Create()
// sequence.Join()                -> sequence.Group()
// sequence.Append()              -> sequence.Chain()
```

## 参考文件

此 Skill 包含完整的 PrimeTween 文档，位于 `references/` 目录：

- **[README.md](references/README.md)** - 官方 README，包含完整 API 文档和示例
- **[API-Reference.md](references/API-Reference.md)** - API 参考手册
- **[changelog.md](references/changelog.md)** - 版本更新日志

## 使用此 Skill

### 初学者
1. 从简单的 `Tween.Position/Rotation/Scale` 开始
2. 学习使用 `Sequence.Create()` 组合多个动画
3. 了解 `Ease` 缓动函数的效果
4. 使用 `TweenSettings` 在 Inspector 中调试动画参数

### 中级用户
1. 使用 `OnComplete` 和 `OnUpdate` 回调
2. 掌握 `Group`、`Chain` 和 `Insert` 的区别
3. 使用协程或 async/await 管理复杂动画序列
4. 理解零分配委托模式避免 GC

### 高级用户
1. 自定义 `Tween.Custom()` 动画任意类型
2. 使用参数化缓动 (`Easing.BounceExact` 等)
3. 优化动画性能 (设置 `PrimeTweenConfig.SetTweensCapacity`)
4. 从 DOTween 迁移现有项目

## 核心概念

### PrimeTween 核心特性
- **零 GC 分配**: 运行时不会产生任何堆内存分配
- **高性能**: 专为性能优化，比 DOTween 快得多
- **Inspector 集成**: 所有动画参数可在 Inspector 中调整
- **类型安全**: 使用 struct 而非 class，避免空引用异常
- **不可重用**: Tweens 完成后自动销毁，无需手动管理

### Tween vs Sequence
- **Tween**: 单个动画，返回 `Tween` struct
- **Sequence**: 多个动画的组合，可以串行、并行或混合执行

### 内存分配注意事项
- ❌ `OnComplete(() => MyMethod())` - 闭包会分配内存
- ✅ `OnComplete(target: this, target => target.MyMethod())` - 零分配

### 推荐命名空间
```csharp
using PrimeTween;
```

### 推荐编译选项
```csharp
// 启用安全检查 (开发时)
#define PRIME_TWEEN_SAFETY_CHECKS

// 启用 DOTween 适配器 (迁移时)
#define PRIME_TWEEN_DOTWEEN_ADAPTER

// 启用实验性功能
#define PRIME_TWEEN_EXPERIMENTAL
```

## 资源

### 官方资源
- **GitHub**: https://github.com/KyryloKuzyk/PrimeTween
- **Asset Store**: https://assetstore.unity.com/packages/tools/animation/primetween-252960
- **Unity Discussions**: https://discussions.unity.com/t/926420
- **FAQ**: https://github.com/KyryloKuzyk/PrimeTween#faq

### Demo 场景位置
本地 Demo 场景位于 `Assets/Plugins/PrimeTween/Demo/`:
- `Demo.cs` - 主 Demo 脚本
- `TypewriterAnimatorExample.cs` - 打字机效果示例
- `CameraController.cs` - 相机控制示例
- `MeasureMemoryAllocations.cs` - 内存分配测量

### 常用 API 模式
```csharp
// 基础动画模式
Tween.TweenType(target, endValue, duration, ease, cycles, cycleMode, startDelay, useUnscaledTime)

// TweenSettings 模式
Tween.TweenType(target, tweenSettings)

// 回调链模式
Tween.TweenType(...).OnComplete(...).OnUpdate(...)

// 序列模式
Sequence.Create().Chain(...).Group(...).Insert(...)
```

## 说明

- 此 Skill 基于 **PrimeTween v1.3.7** (2025-12-20)
- 支持 Unity 2020.1+
- 所有代码示例遵循 C# 编码规范
- PrimeTween 与 DOTween 可以共存于同一项目中
- 首次使用建议运行 Demo 场景了解功能

## 性能优势

PrimeTween 相比其他 Tween 库的优势：
- 运行时零 GC 分配
- 更快的动画执行速度
- 无需缓存和重用 tweens
- 自动资源清理
- 更少的内存占用

---

*此 Skill 基于 [KyryloKuzyk/PrimeTween](https://github.com/KyryloKuzyk/PrimeTween) 的官方文档和示例生成。*