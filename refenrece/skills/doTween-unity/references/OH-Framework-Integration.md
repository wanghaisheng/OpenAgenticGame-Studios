# DOTween 与 OH 框架集成说明

本文档说明 DOTween 在 OH 框架中的使用规范和扩展方法。

## OH 框架扩展方法

项目中 `Assets/OH框架工具包/OHExtend.cs` 提供了针对 Image 组件的 DOTween 扩展方法。

### 命名空间

所有扩展方法位于 `OHTools` 命名空间：

```csharp
using OHTools;
```

### Image 扩展方法

#### OHEndEffect - 通用结束清理

动画结束后恢复原始材质并销毁临时材质。

```csharp
public static Sequence OHEndEffect(this Image image, Material originalMat = null)
```

**参数**:
- `image`: 目标 Image 组件
- `originalMat`: 原始材质，如果为 null 则使用默认 UI/Default Shader

**返回**: Sequence 对象

**使用场景**: 在使用自定义 Shader 动画后恢复原始材质

**示例**:
```csharp
Sequence seq = DOTween.Sequence();
// ... 执行动画
seq.AppendCallback(() => {
    image.OHEndEffect();
});
```

---

#### OHFlashWhiteToBlack - 白到黑闪烁

Image 从透明闪烁白色，然后变为黑色，最后恢复原始颜色。

```csharp
public static Sequence OHFlashWhiteToBlack(this Image image, float duration, bool isClear = true)
```

**参数**:
- `duration`: 每个阶段的持续时间
- `isClear`: 是否在开始时将 Image 颜色设为透明

**动画流程**:
1. 如果 `isClear=true`，设置颜色为透明
2. 动画到白色
3. 动画到黑色
4. 恢复原始颜色

**使用场景**: 闪烁特效、过渡动画

**示例**:
```csharp
image.OHFlashWhiteToBlack(0.5f, isClear: true).Play();
```

---

#### OHFlashBlackToWhite - 黑到白闪烁

Image 从透明闪烁黑色，然后变为白色，最后恢复原始颜色。

```csharp
public static Sequence OHFlashBlackToWhite(this Image image, float duration, bool isClear = true)
```

**参数**:
- `duration`: 每个阶段的持续时间
- `isClear`: 是否在开始时将 Image 颜色设为透明

**动画流程**:
1. 如果 `isClear=true`，设置颜色为透明
2. 动画到黑色
3. 动画到白色
4. 恢复原始颜色

**使用场景**: 闪烁特效、过渡动画

**示例**:
```csharp
image.OHFlashBlackToWhite(0.5f, isClear: true).Play();
```

---

#### OHGlitchChangeSprite - 故障艺术切换图片

使用故障艺术 Shader 切换 Image 的 Sprite。

```csharp
public static Sequence OHGlitchChangeSprite(this Image image, Sprite nextSprite, float duration)
```

**参数**:
- `nextSprite`: 目标 Sprite
- `duration`: 过渡动画持续时间

**依赖 Shader**: `OHEffect/OHGlitchChange`

**动画流程**:
1. 创建临时材质并设置故障艺术 Shader
2. 设置当前 Sprite 和目标 Sprite 贴图
3. 动画 `_Transition` 属性从 0 到 1
4. 动画完成后替换 Sprite，恢复原始材质，销毁临时材质

**使用场景**: 图片切换特效、故障艺术风格

**示例**:
```csharp
Sprite newSprite = Resources.Load<Sprite>("Images/NewSprite");
image.OHGlitchChangeSprite(newSprite, 0.5f).Play();
```

**注意事项**:
- 需要确保项目中存在 `OHEffect/OHGlitchChange` Shader
- 自动处理材质创建和销毁

---

#### OHFadeChangeSprite - 渐变切换图片

使用淡入淡出效果切换 Image 的 Sprite。

```csharp
public static Sequence OHFadeChangeSprite(this Image image, Sprite nextSprite, float duration)
```

**参数**:
- `nextSprite`: 目标 Sprite
- `duration`: 过渡动画持续时间

**动画流程**:
1. 创建叠加层 Image 显示目标 Sprite
2. 同时淡出原始 Image 和淡入叠加层
3. 动画完成后替换原始 Sprite，恢复不透明，删除叠加层

**使用场景**: 平滑图片切换、过渡动画

**示例**:
```csharp
Sprite newSprite = Resources.Load<Sprite>("Images/NewSprite");
image.OHFadeChangeSprite(newSprite, 0.5f).Play();
```

**注意事项**:
- 叠加层会自动禁用 RaycastTarget
- 叠加层会设置为原始 Image 的最后一个子节点

---

#### OHNeonFlicker - 霓虹灯故障闪烁特效

使用霓虹灯故障 Shader 实现 Image 的发光闪烁效果。

```csharp
public static Sequence OHNeonFlicker(this Image image, Color emissionColor, float maxFlicker = 1f,
    float minFlicker = 0.2f, float speed = 4f, bool isLoop = true, float totalDuration = 1f)
```

**参数**:
- `emissionColor`: 发光颜色
- `maxFlicker`: 最大闪烁强度 (默认 1)
- `minFlicker`: 最小闪烁强度 (默认 0.2)
- `speed`: 闪烁速度 (默认 4)
- `isLoop`: 是否无限循环 (默认 true)
- `totalDuration`: 总持续时间（当 `isLoop=false` 时有效）

**依赖 Shader**: `OHEffect/OHNeonFlicker`

**动画流程**:
1. 创建临时材质并设置霓虹灯闪烁 Shader
2. 设置发光颜色、闪烁范围和速度参数
3. 如果 `isLoop=true`，返回不自动结束的 Sequence
4. 如果 `isLoop=false`，在 `totalDuration` 后调用 `OHEndEffect` 恢复

**使用场景**: 霓虹灯效果、发光特效、故障艺术

**示例**:
```csharp
// 无限循环闪烁
image.OHNeonFlicker(Color.cyan, maxFlicker: 1f, minFlicker: 0.2f, speed: 4f, isLoop: true).Play();

// 定时闪烁
image.OHNeonFlicker(Color.cyan, isLoop: false, totalDuration: 3f).Play();
```

**注意事项**:
- 需要确保项目中存在 `OHEffect/OHNeonFlicker` Shader
- 无限循环时需要手动调用 `OHEndEffect` 停止
- 定时模式下会自动清理

---

## OHExtend.cs 代码架构

### 文件位置

```
Assets/OH框架工具包/OHExtend.cs
```

### 命名空间结构

```csharp
namespace OHTools
{
    // TextMeshPro 扩展（已废弃，使用 Text Animator 插件代替）
    public static class OHTMPExtend { }

    // String 扩展
    public static class OHStringExtend { }

    // Image 扩展
    public static class OHImageExtend { }
}
```

### 注释规范

所有扩展方法遵循 OH 框架注释规范：

1. 使用中文注释
2. 公共方法包含 XML 文档注释
3. 复杂逻辑块包含行内注释
4. 未使用 `[LabelText]` 的变量包含 `// 名称注释`

**示例**:
```csharp
/// <summary>
/// 通用的效果结束清理方法
/// </summary>
public static Sequence OHEndEffect(this Image image, Material originalMat = null)
{
    // 缓存当前效果材质
    var animMat = image.material;

    // 创建一个 Sequence
    var seq = DOTween.Sequence();

    // ... 实现
}
```

---

## 使用最佳实践

### 1. 扩展方法优先

在实现 UI 动画时，优先检查 `OHExtend.cs` 中是否已有封装好的方法：

```csharp
// ✅ 优先使用扩展方法
using OHTools;
image.OHGlitchChangeSprite(newSprite, 0.5f).Play();

// ❌ 避免重复实现
// 不要自己写故障艺术切换逻辑
```

### 2. 自定义扩展方法

如果需要新的动画效果，作为 static 扩展方法添加到 `OHTools` 命名空间：

```csharp
using DG.Tweening;
using UnityEngine.UI;
using UnityEngine;

namespace OHTools
{
    public static class OHImageExtend
    {
        /// <summary>
        /// 我的自定义动画效果
        /// </summary>
        public static Sequence OHMyCustomEffect(this Image image, float duration)
        {
            // 实现自定义动画
            var seq = DOTween.Sequence();
            // ...
            return seq;
        }
    }
}
```

### 3. Shader 依赖

使用 Shader 动画时，确保 Shader 存在：

```csharp
// 检查 Shader 是否存在
Shader shader = Shader.Find("OHEffect/OHGlitchChange");
if (shader == null)
{
    Debug.LogWarning("Shader 'OHEffect/OHGlitchChange' not found!");
    return;
}
```

### 4. 内存管理

自动清理材质：

```csharp
// 在扩展方法中自动处理材质销毁
seq.AppendCallback(() =>
{
    image.material = originalMat;
    image.SetMaterialDirty();
    Object.Destroy(animMat); // 销毁临时材质
});
```

### 5. 生命周期管理

在 MonoBehaviour 中正确管理 Sequence：

```csharp
using DG.Tweening;
using OHTools;
using UnityEngine;
using UnityEngine.UI;

public class MyUIManager : MonoBehaviour
{
    [SerializeField] private Image _targetImage;
    private Sequence _currentSequence;

    void OnEnable()
    {
        PlayAnimation();
    }

    void OnDisable()
    {
        // 停止并清理所有动画
        _currentSequence?.Kill();
        _targetImage.DOKill();
    }

    void PlayAnimation()
    {
        // 停止之前的动画
        _currentSequence?.Kill();

        // 播放新动画
        _currentSequence = _targetImage.OHNeonFlicker(Color.cyan);
        _currentSequence.Play();
    }
}
```

---

## 已废弃的功能

### OHTypeWriter - 打字机效果

`OHExtend.cs` 中注释掉的 `OHTypeWriter` 方法已废弃，项目现在使用 **Text Animator** 插件实现打字机效果。

**废弃原因**: 使用 Text Animator 插件代替

**建议**:
- 新项目使用 Text Animator 插件
- 不要恢复或使用 `OHTypeWriter` 方法

---

## Shader 依赖列表

以下 Shader 需要在项目中存在才能使用相应扩展方法：

1. **OHEffect/OHGlitchChange** - 故障艺术切换
2. **OHEffect/OHNeonFlicker** - 霓虹灯闪烁
3. **UI/Default** - 默认 UI Shader (Unity 内置)

Shader 位置建议：
```
Assets/Shaders/OHEffect/OHGlitchChange.shader
Assets/Shaders/OHEffect/OHNeonFlicker.shader
```

---

## 与 OH 框架其他部分的集成

### 事件驱动

在复杂场景中，结合 `OHEventCenter` 使用：

```csharp
using OHTools;

void OnEnable()
{
    OHEventCenter.AddEventListener("PlayEffect", OnPlayEffect);
}

void OnDisable()
{
    OHEventCenter.RemoveEventListener("PlayEffect", OnPlayEffect);
}

void OnPlayEffect(object[] args)
{
    if (args.Length > 0 && args[0] is Image image)
    {
        image.OHGlitchChangeSprite(newSprite, 0.5f).Play();
    }
}
```

### 数据驱动

结合 ScriptableObject 存储动画参数：

```csharp
[CreateAssetMenu(menuName = "OH/Animation Data")]
public class AnimationDataSo : ScriptableObject
{
    [LabelText("动画时长")]
    public float duration = 0.5f;

    [LabelText("发光颜色")]
    public Color emissionColor = Color.cyan;

    [LabelText("最大闪烁强度")]
    public float maxFlicker = 1f;

    [LabelText("最小闪烁强度")]
    public float minFlicker = 0.2f;
}

// 使用
image.OHNeonFlicker(
    animationData.emissionColor,
    animationData.maxFlicker,
    animationData.minFlicker,
    animationData.duration
).Play();
```

### 单例模式

结合 `OHMonoSingleton` 管理全局动画：

```csharp
using OHTools;

public class AnimationManager : OHMonoSingleton<AnimationManager>
{
    public void PlayGlitchEffect(Image image, Sprite newSprite)
    {
        image.OHGlitchChangeSprite(newSprite, 0.5f).Play();
    }

    public void PlayNeonFlicker(Image image, Color color)
    {
        image.OHNeonFlicker(color).Play();
    }
}

// 使用
AnimationManager.Instance.PlayGlitchEffect(image, newSprite);
```

---

## 常见问题

### Q1: 如何停止无限循环的霓虹灯特效？

```csharp
// 错误方式：直接 Kill 会破坏材质
image.DOKill();

// 正确方式：调用 OHEndEffect 恢复原始材质
image.OHEndEffect();
```

### Q2: 如何链式调用多个扩展方法？

```csharp
Sequence seq = DOTween.Sequence();
seq.Append(image.OHFlashBlackToWhite(0.3f));
seq.AppendInterval(0.2f);
seq.AppendCallback(() => image.OHGlitchChangeSprite(newSprite, 0.5f));
seq.Play();
```

### Q3: 扩展方法返回的 Sequence 需要手动 Play 吗？

是的，扩展方法返回暂停状态的 Sequence，需要手动调用 `.Play()`：

```csharp
// 创建 Sequence（暂停状态）
Sequence seq = image.OHNeonFlicker(Color.cyan);

// 配置其他选项
seq.SetLoops(3, LoopType.Yoyo);

// 开始播放
seq.Play();
```

---

*本文档基于 OH 框架规范和 Assets/OH框架工具包/OHExtend.cs 创建。*