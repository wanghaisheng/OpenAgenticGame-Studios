---
name: doTween-unity
description: DOTween Unity 动画插件。用于补间动画、UI 过渡、相机震动、序列、TextMeshPro 动画以及 Unity 中任何动画需求。此 Skill 应用于 Unity 项目中与 DOTween 动画系统相关的所有任务。
---

# DOTween Unity Skill

DOTween (DG.Tweening) 是一个快速、高效、类型安全的 Unity 动画引擎，支持动画所有内容，包括 Transform、UI、Material、颜色、文本等。

## 何时使用此 Skill

在以下情况下触发此 Skill：
- DOTween 动画插件 (Demigiant/DOTween)
- UI 动画和过渡效果 (UI animations and transitions)
- Transform 动画 (位置、旋转、缩放)
- Material 和 Color 动画
- 相机震动和屏幕特效 (Camera shake and screen effects)
- 动画序列和时序控制 (Animation sequences)
- 延迟执行和回调 (Delays and callbacks)
- TextMeshPro 文字打字机效果
- 自定义扩展方法 (OHExtend.cs 中的扩展)
- OH 框架特定的 UI 动画效果

## 快速参考

### Hello World - 基础动画

```csharp
using DG.Tweening;

// 位置动画 - 将 transform 移动到目标位置，持续 1 秒
transform.DOMove(new Vector3(10, 0, 5), 1f);

// 本地位置动画
transform.DOLocalMoveX(10f, 1f);

// 旋转动画
transform.DORotateQuaternion(Quaternion.Euler(0, 90, 0), 1f);
transform.DORotate(new Vector3(0, 360, 0), 1f, RotateMode.WorldAxisAdd);

// 缩放动画
transform.DOScale(2f, 0.5f);

// UI 透明度动画
image.DOFade(0f, 1f);

// 设置缓动和循环
transform.DOMoveX(10, 1f).SetEase(Ease.OutBounce).SetLoops(-1, LoopType.Yoyo);
```

### 1. Transform 动画

#### 位置动画

```csharp
using DG.Tweening;

// 世界坐标位置
transform.DOMove(new Vector3(10, 0, 5), 1f);
transform.DOMoveX(10f, 1f);
transform.DOMoveY(5f, 1f);
transform.DOMoveZ(0f, 1f);

// 本地坐标位置
transform.DOLocalMove(new Vector3(10, 0, 5), 1f);
transform.DOLocalMoveX(10f, 1f);
transform.DOLocalMoveY(5f, 1f);
transform.DOLocalMoveZ(0f, 1f);

// 跳跃动画
transform.DOJump(targetPosition, jumpPower: 2f, numJumps: 2, duration: 1f);
```

#### 旋转动画

```csharp
// 欧拉角旋转
transform.DORotate(new Vector3(0, 90, 0), 1f);
transform.DORotateQuaternion(Quaternion.Euler(0, 90, 0), 1f);

// 本地旋转
transform.DOLocalRotate(new Vector3(0, 360, 0), 1f, RotateMode.WorldAxisAdd);

// 旋转模式 (RotateMode)
// - Fast: 最快的旋转方式 (360° = 0°)
// - FastBeyond360: 允许超过 360°
// - WorldAxisAdd: 在世界轴上旋转增量
// - LocalAxisAdd: 在本地轴上旋转增量
```

#### 缩放动画

```csharp
// 均匀缩放
transform.DOScale(2f, 0.5f);

// 非均匀缩放
transform.DOScale(new Vector3(2, 1, 0.5f), 0.5f);

// 单轴缩放
transform.DOScaleX(2f, 0.5f);
transform.DOScaleY(0.5f, 0.5f);
transform.DOScaleZ(1.5f, 0.5f);

// Punch 效果 (弹性缩放冲击)
transform.DOPunchScale(new Vector3(0.2f, 0.2f, 0.2f), 0.5f, 2, 0.5f);
```

### 2. UI 动画

```csharp
using DG.Tweening;
using UnityEngine.UI;

// RectTransform 位置和大小
rectTransform.DOAnchorPos(new Vector2(100, 100), 0.5f);
rectTransform.DOAnchorPosX(100f, 0.5f);
rectTransform.DOAnchorPosY(100f, 0.5f);
rectTransform.DOAnchorPos3D(new Vector3(100, 100, 0), 0.5f);
rectTransform.DOSizeDelta(new Vector2(200, 100), 0.5f);

// UI 颜色和透明度
image.DOColor(Color.red, 1f);
image.DOFade(0f, 1f); // 透明度从当前值到目标值
image.DOFade(1f, 1f);

// CanvasGroup 透明度
canvasGroup.DOFade(1f, 0.3f);

// Text 颜色和文本
text.DOColor(Color.yellow, 1f);
text.DOFade(0f, 1f);
text.DOText("Hello World!", 2f, richTextEnabled: true);
```

### 3. Material 动画

```csharp
// Material 颜色
material.DOColor(Color.blue, 1f);
material.DOColor(Color.white, "_EmissionColor", 1f); // 自定义属性颜色

// Material 透明度
material.DOFade(0f, 1f);

// Material 颜色渐变
material.DOColor(new Color(0, 0, 0, 0), 1f);

// Shader 属性动画
material.DOFloat(1f, "_Metallic", 1f);
material.DOVector(Vector4.one, "_Color", 1f);
```

### 4. 相机动画

```csharp
using DG.Tweening;

// 相机属性
camera.DOOrthoSize(5f, 1f);
camera.DOFieldOfView(60f, 1f);
camera.DOColor(Color.black, 2f);

// 相机震动
camera.DOShakePosition(1f, strength: new Vector3(1, 1, 0), vibrato: 10, randomness: 90);
camera.DOShakeRotation(1f, strength: 10, vibrato: 10, randomness: 90);

// 震动参数说明
// duration: 震动持续时间
// strength: 震动强度 (Vector3)
// vibrato: 震动频率
// randomness: 随机性 (0-180)
// fadeOut: 是否淡出 (默认 true)
```

### 5. TextMeshPro 动画

```csharp
using DG.Tweening;
using TMPro;

// TextMeshPro 颜色和透明度
textMeshPro.DOColor(Color.yellow, 1f);
textMeshPro.DOFade(0f, 1f);

// 字体大小
textMeshPro.DOFontSize(48f, 0.5f);

// MaxVisibleCharacters (打字机效果基础)
textMeshPro.DOMaxVisibleCharacters(textMeshPro.textInfo.characterCount, 2f);

// 注意: 项目中 OHExtend.cs 已有打字机效果扩展，但已使用 Text Animator 插件代替
```

### 6. 震动和冲击效果

```csharp
using DG.Tweening;

// 位置震动
transform.DOShakePosition(duration: 1f, strength: 1f, vibrato: 10, randomness: 90);

// 旋转震动
transform.DOShakeRotation(duration: 1f, strength: 45f, vibrato: 10);

// 缩放震动
transform.DOShakeScale(duration: 0.5f, strength: 0.5f, vibrato: 10);

// Punch 效果 (单向冲击，然后回到原值)
transform.DOPunchPosition(direction: transform.up * 2, duration: 0.5f, vibrato: 10, elasticity: 0.5f);
transform.DOPunchRotation(rotation: new Vector3(0, 0, 90), duration: 0.5f, vibrato: 10, elasticity: 0.5f);
transform.DOPunchScale(punch: Vector3.one * 0.5f, duration: 0.5f, vibrato: 10, elasticity: 0.5f);
```

### 7. 回调和延迟

```csharp
using DG.Tweening;

// OnComplete 回调
transform.DOMoveX(10, 1f).OnComplete(() => Debug.Log("Animation completed!"));

// OnUpdate 回调
transform.DOMoveX(10, 1f).OnUpdate(() => Debug.Log("Animating..."));

// OnStart 回调
transform.DOMoveX(10, 1f).OnStart(() => Debug.Log("Animation started!"));

// 延迟执行
DOTween.DelayedCall(1f, () => Debug.Log("Executed after 1 second"));

// 多个回调
transform.DOMoveX(10, 1f)
    .OnStart(() => Debug.Log("Started"))
    .OnUpdate(() => Debug.Log("Updating"))
    .OnComplete(() => Debug.Log("Completed"));
```

### 8. 循环动画

```csharp
using DG.Tweening;

// 无限循环，Yoyo 往返模式
transform.DOMoveY(10, 0.5f).SetLoops(-1, LoopType.Yoyo);

// 指定循环次数
transform.DOScale(2f, 0.5f).SetLoops(3, LoopType.Yoyo);

// LoopType 选项:
// - Restart: 从头重新开始
// - Yoyo: 往返动画
// - Incremental: 每次循环递增 endValue

// 设置循环和缓动
transform.DOMoveX(10, 1f).SetLoops(3, LoopType.Restart).SetEase(Ease.InOutSine);
```

### 9. 序列动画

```csharp
using DG.Tweening;

// 基础序列
Sequence seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f));
seq.Append(transform.DOScale(2f, 0.5f));
seq.Append(transform.DORotate(new Vector3(0, 90, 0), 0.5f));

// 并行动画 (Join)
seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f));
seq.Join(transform.DOScale(2f, 1f)); // 与前一个动画并行
seq.Append(transform.DORotate(new Vector3(0, 90, 0), 0.5f));

// 预设序列 (链式调用)
seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f))
   .Join(transform.DOScale(2f, 1f))
   .Append(transform.DORotate(new Vector3(0, 90, 0), 0.5f));

// 插入动画 (Insert)
seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f));
seq.Insert(0.5f, transform.DOScale(2f, 1f)); // 在 0.5 秒处插入
seq.Append(transform.DORotate(new Vector3(0, 90, 0), 0.5f));

// 回调序列
seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f))
   .AppendCallback(() => Debug.Log("Move completed"))
   .Append(transform.DOScale(2f, 0.5f))
   .AppendCallback(() => Debug.Log("Scale completed"));

// 延迟间隔
seq = DOTween.Sequence();
seq.Append(transform.DOMoveX(10, 1f));
seq.AppendInterval(1f); // 延迟 1 秒
seq.Append(transform.DOScale(2f, 0.5f));
```

### 10. 协程和异步

```csharp
using DG.Tweening;
using System.Collections;

// 协程等待
IEnumerator CoroutineExample() {
    Tween tween = transform.DOMoveX(10f, 1.5f);
    yield return tween.WaitForCompletion();

    transform.DOScale(2f, 0.5f);
    yield return new WaitForSeconds(1f);

    transform.DORotate(new Vector3(0, 90, 0), 1f);
    yield return new WaitForSeconds(1f);

    Debug.Log("Sequence completed");
}

// 等待其他方式
IEnumerator WaitForOtherWays() {
    // 等待动画被杀死 (包括完成)
    yield return transform.DOMoveX(10f, 1.5f).WaitForKill();

    // 等待动画达到指定位置
    yield return transform.DOMoveX(10f, 1.5f).WaitForElapsedLoops(2);

    // 等待动画位置
    yield return transform.DOMoveX(10f, 1.5f).WaitForPosition(0.5f);
}

// UniTask 集成 (项目中使用 UniTask)
async void AsyncExample() {
    await transform.DOMoveX(10f, 1.5f).ToUniTask();
    await transform.DOScale(2f, 0.5f).ToUniTask();
    await transform.DORotate(new Vector3(0, 90, 0), 1f).ToUniTask();
    Debug.Log("Sequence completed");
}
```

### 11. 控制动画

```csharp
using DG.Tweening;

// 创建并存储 tween 引用
Tweener tween = transform.DOMoveX(10, 1f);

// 检查是否活跃
if (tween.active()) {
    Debug.Log("Animation is active");
}

// 暂停/恢复
tween.Pause();
tween.Play();

// 反向播放
tween.Flip();

// 重启
tween.Restart();

// 倒带
tween.Rewind();

// 杀死动画 (停止并清理)
tween.Kill();
tween.Kill(complete: false); // 不完成直接停止
tween.Kill(complete: true);  // 完成后停止

// 完成动画
tween.Complete();

// 杀死所有动画
DOTween.KillAll();
DOTween.Kill(transform); // 杀死指定对象上的所有动画

// 暂停所有动画
DOTween.PauseAll();
DOTween.Pause(transform);

// 清空所有动画
DOTween.Clear();
DOTween.Clear(transform); // 清空指定对象上的所有动画

// 获取动画数据
Debug.Log($"Elapsed time: {tween.Elapsed()}");
Debug.Log($"Position (percentage): {tween.Position()}"); // 0-1
Debug.Log($"Elapsed percentage: {tween.ElapsedPercentage()}"); // 0-1
```

### 12. 缓动函数

```csharp
using DG.Tweening;

// 使用标准 Ease
transform.DOMoveX(10, 1f).SetEase(Ease.InOutSine);
transform.DOScale(2f, 0.5f).SetEase(Ease.OutBounce);
image.DOFade(0f, 1f).SetEase(Ease.InQuad);

// 常用 Ease 类型:
// - Linear: 线性
// - InOutSine: 正弦缓入缓出
// - OutBounce: 弹跳效果
// - InQuad: 二次方缓入
// - OutQuad: 二次方缓出
// - InOutQuad: 二次方缓入缓出
// - InCubic, OutCubic, InOutCubic
// - InQuart, OutQuart, InOutQuart
// - InQuint, OutQuint, InOutQuint
// - InExpo, OutExpo, InOutExpo
// - InCirc, OutCirc, InOutCirc
// - InElastic, OutElastic, InOutElastic
// - InBack, OutBack, InOutBack
// - flash: 闪烁效果

// 使用 AnimationCurve
AnimationCurve customCurve = new AnimationCurve();
customCurve.AddKey(0, 0);
customCurve.AddKey(1, 1);
transform.DOMoveX(10, 1f).SetEase(customCurve);

// 自定义缓动函数
transform.DOMoveX(10, 1f).SetEase((float time, float duration, float overshootOrAmplitude, float period) => {
    // 自定义缓动逻辑
    return time; // 返回 0-1 的值
});
```

### 13. 设置选项

```csharp
using DG.Tweening;

// 链式设置
transform.DOMoveX(10, 1f)
    .SetEase(Ease.OutBounce)
    .SetLoops(3, LoopType.Yoyo)
    .SetDelay(0.5f)
    .SetRelative(true) // 相对当前值
    .SetAutoKill(true) // 自动杀死
    .SetRecyclable(true) // 可回收
    .SetUpdate(true); // 使用 unscaled time

// SetRelative: 相对当前值动画
transform.DOLocalMoveX(5, 1f).SetRelative(true); // 从当前位置向右移动 5

// SetUpdate: Update 类型
// - UpdateType.Normal: 使用 Time.deltaTime (默认)
// - UpdateType.Late: 使用 LateUpdate
// - UpdateType.Fixed: 使用 FixedUpdate
// - true: 使用 Time.unscaledDeltaTime (无视 timeScale)

// SetDelay: 开始前延迟
transform.DOMoveX(10, 1f).SetDelay(0.5f); // 延迟 0.5 秒后开始

// SetSpeedBased: 基于速度的动画 (duration 会根据距离自动计算)
transform.DOMove(targetPosition, 1f).SetSpeedBased();

// SetOptions: 特定动画的额外选项
text.DOText("Hello World", 2f).SetOptions(scrambleMode: ScrambleMode.All);
```

### 14. OH 框架扩展方法

项目中 `OHExtend.cs` 提供了针对 Image 的扩展方法，符合 OH 框架的编码规范。

```csharp
using OHTools;

// Image 闪烁效果 (白到黑)
image.OHFlashWhiteToBlack(duration: 0.5f, isClear: true);

// Image 闪烁效果 (黑到白)
image.OHFlashBlackToWhite(duration: 0.5f, isClear: true);

// 故障艺术切换 Sprite
image.OHGlitchChangeSprite(nextSprite: newSprite, duration: 0.5f);

// 渐变切换 Sprite
image.OHFadeChangeSprite(nextSprite: newSprite, duration: 0.5f);

// 霓虹灯故障闪烁特效
image.OHNeonFlicker(
    emissionColor: Color.cyan,
    maxFlicker: 1f,
    minFlicker: 0.2f,
    speed: 4f,
    isLoop: true,
    totalDuration: 1f
);

// 结束特效并恢复原始材质
image.OHEndEffect(originalMat: null);

// 注意: OHTypeWriter 打字机效果已使用 Text Animator 插件代替，不再使用
```

### 15. DOTween 设置和优化

```csharp
using DG.Tweening;

// 全局设置
DOTween.Init(
    autoKillMode: AutoKillMode.Default, // 自动杀死模式
    useSafeMode: true, // 安全模式 (防止单例被销毁时的错误)
    logBehaviour: LogBehaviour.Default // 日志行为
);

// TimeScale 控制
DOTween.timeScale = 1f; // 全局时间缩放 (影响所有动画)
DOTween.useUnscaledTime = false; // 是否使用 unscaled time

// 最大同时播放的 tweener 数量 (性能优化)
DOTween.SetTweensCapacity(200, 50);

// 检查是否有活跃的 tween
bool isActive = DOTween.IsTweening(transform);
bool anyActive = DOTween.IsTweening();

// 获取所有活跃的 tweens
List<Tween> activeTweens = DOTween.Totals();
```

### 16. 特殊动画类型

```csharp
using DG.Tweening;

// 颜色混合
image.DOColor(Color.red, 1f).SetEase(Ease.Linear);

// 透明度淡入淡出
image.DOFade(0f, 1f); // 淡出
canvasGroup.DOFade(1f, 1f); // 淡入

// 文本动画
text.DOText("New Text", 2f, richTextEnabled: true, scrambleMode: ScrambleMode.None);

// ScrambleMode 选项:
// - None: 无乱码
// - All: 所有字符
// - Upper: 大写字母
// - Lower: 小写字母
// - Numerals: 数字
// - Custom: 自定义字符集

// 渐变动画
Gradient gradient = new Gradient();
gradient.SetKeys(
    new GradientColorKey[] { new GradientColorKey(Color.red, 0f), new GradientColorKey(Color.blue, 1f) },
    new GradientAlphaKey[] { new GradientAlphaKey(1f, 0f), new GradientAlphaKey(1f, 1f) }
);
material.DOGradientColor(gradient, "_Color", 2f);

// 路径动画 (Vector3 数组)
Vector3[] path = new Vector3[] {
    new Vector3(0, 0, 0),
    new Vector3(5, 0, 0),
    new Vector3(5, 5, 0),
    new Vector3(0, 5, 0)
};
transform.DOPath(path, 4f, PathType.Linear)
    .SetLookAt(0.01f) // 沿路径方向旋转
    .SetOptions(closePath: true); // 闭合路径

// PathType 选项:
// - Linear: 直线连接
// - CatmullRom: 平滑曲线 (默认)
```

### 17. DOTween 与 UniTask 集成

项目中已集成 UniTask，DOTween 提供了扩展方法用于异步操作。

```csharp
using DG.Tweening;
using Cysharp.Threading.Tasks;

// 等待 Tween 完成
async UniTask AsyncExample() {
    await transform.DOMoveX(10f, 1f).ToUniTask();
    Debug.Log("Move completed");
}

// 等待 Sequence 完成
async UniTask SequenceExample() {
    Sequence seq = DOTween.Sequence();
    seq.Append(transform.DOMoveX(10f, 1f));
    seq.Append(transform.DOScale(2f, 0.5f));
    await seq.Play().ToUniTask();
    Debug.Log("Sequence completed");
}

// 取消令牌
CancellationTokenSource cts = new CancellationTokenSource();

async UniTask CancellableExample() {
    try {
        await transform.DOMoveX(10f, 1f).WithCancellation(cts.Token);
    } catch (OperationCanceledException) {
        Debug.Log("Animation cancelled");
    }
}

// 取消动画
cts.Cancel();
```

### 18. 常见使用模式

```csharp
using DG.Tweening;

// UI 淡入淡出
void FadeUI(CanvasGroup canvasGroup, bool fadeIn, float duration) {
    canvasGroup.DOFade(fadeIn ? 1f : 0f, duration)
        .SetEase(Ease.InOutSine)
        .OnComplete(() => {
            canvasGroup.interactable = fadeIn;
            canvasGroup.blocksRaycasts = fadeIn;
        });
}

// UI 缩放弹跳
void BounceUI(RectTransform rect) {
    rect.DOScale(1.2f, 0.1f)
        .SetEase(Ease.OutQuad)
        .OnComplete(() => {
            rect.DOScale(1f, 0.2f).SetEase(Ease.OutBounce);
        });
}

// 按钮点击反馈
void ButtonClickFeedback(RectTransform button) {
    button.DOScale(0.9f, 0.05f)
        .SetEase(Ease.OutQuad)
        .OnComplete(() => {
            button.DOScale(1f, 0.2f).SetEase(Ease.OutBounce);
        });
}

// 无限旋转
void InfiniteRotate(Transform target) {
    target.DORotate(new Vector3(0, 360, 0), 2f, RotateMode.WorldAxisAdd)
        .SetEase(Ease.Linear)
        .SetLoops(-1, LoopType.Restart);
}

// 浮动效果
void FloatingEffect(Transform target) {
    Sequence seq = DOTween.Sequence();
    seq.Append(target.DOMoveY(target.position.y + 0.5f, 1f).SetEase(Ease.InOutSine));
    seq.Append(target.DOMoveY(target.position.y - 0.5f, 1f).SetEase(Ease.InOutSine));
    seq.SetLoops(-1, LoopType.Yoyo);
}
```

## 参考文件

此 Skill 包含以下参考资源：

- **[DOTween Documentation](https://dotween.demigiant.com/documentation.php)** - 官方在线文档
- **DOTween 官方示例**: 位于 `Assets/Plugins/Demigiant/DOTween/` 目录
- **OHExtend.cs**: 位于 `Assets/OH框架工具包/OHExtend.cs` - OH 框架扩展方法

## 项目规范

在使用 DOTween 时，必须遵循以下 OH 框架规范：

1. **动画优先级**: 除非动画与物理有关，或用户指定要求使用其他插件，否则所有动画都必须使用 DoTween 插件实现。

2. **扩展方法优先**: 优先检查 `OHExtend.cs` 中是否已有封装好的方法（如颜色转换、UI 特效）。通用的工具函数应作为 static 扩展方法归入 OHTools 命名空间。

3. **命名规范**:
   - DOTween 扩展方法使用 `OH` 前缀 (如 `OHFlashWhiteToBlack`)
   - 放置在 `OHTools` 命名空间下
   - 使用中文注释说明方法功能

4. **内存优化**:
   - 使用 `SetAutoKill(true)` 自动杀死完成的 tween
   - 使用 `SetRecyclable(true)` 允许 tween 被回收
   - 在 `OnDisable` 或 `OnDestroy` 中杀死对象上的所有 tween
   - 避免在 `Update` 中创建新的 tween

5. **生命周期管理**:
   ```csharp
   // 在 OnDisable 或 OnDestroy 中清理
   void OnDisable() {
       transform.DOKill(); // 杀死此对象上的所有 tween
   }

   // 或使用 CanvasGroup/UI 组件
   void OnDisable() {
       canvasGroup.DOKill();
       image.DOKill();
   }
   ```

6. **异常处理**:
   - 除非用户要求，否则必须避免做出多余的防御性编程操作
   - 不添加额外的判空检查、日志打印、异常处理

## DOTween vs PrimeTween

项目中同时存在 DOTween 和 PrimeTween 插件。根据架构原则：

- **DOTween**: 传统的 Unity 动画插件，提供丰富的扩展方法和 OH 框架集成
- **PrimeTween**: 高性能零分配动画库，适合性能敏感场景

选择建议：
- 使用 DOTween 当需要 OH 框架扩展方法（如 `OHGlitchChangeSprite`）
- 使用 DOTween 当使用项目已有的 UI 特效系统
- 使用 PrimeTween 当性能是首要考虑因素
- 不要混用两者处理同一对象的动画

## 最佳实践

1. **初始化**: 在游戏启动时调用 `DOTween.Init()`
2. **清理**: 在场景切换或对象销毁时调用 `DOTween.Clear()` 或 `transform.DOKill()`
3. **复用**: 使用 `SetRecyclable(true)` 允许 tween 被回收
4. **性能**: 避免在 Update 中频繁创建 tween
5. **调试**: 使用 `DOTween.Debug.LogBehaviour` 控制日志输出
6. **序列**: 使用 `Sequence` 组合复杂动画序列
7. **缓动**: 选择合适的 `Ease` 类型提升动画质感
8. **时间**: 使用 `SetUpdate(true)` 处理暂停/时间缩放场景

## DOTween Inspector 面板

在 Unity Editor 中，可通过 `Tools/Demigiant/DOTween Utility Panel` 打开设置面板，配置：
- 全局设置
- 安全模式
- 时间缩放
- 最大 tween 数量
- 调试选项

---

*此 Skill 基于 [DOTween 官方文档](https://dotween.demigiant.com/) 和 OH 框架规范创建。*