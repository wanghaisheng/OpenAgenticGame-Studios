---
name: unity
description: Unity Engine 游戏开发。适用于 Unity 项目、C# 脚本、场景设置、GameObject 系统、2D/3D 开发、物理、动画、UI、着色器 Shader、VR/AR 或任何 Unity 相关问题。
---

# Unity Engine 开发 Skill

Unity 游戏开发的全面辅助，涵盖 C# 脚本、场景管理、物理、渲染、动画、UI 和平台特定功能。

## 何时使用此 SKill

此 Skill 应在以下情况下触发：
- Unity Engine 项目（2D/3D 游戏开发）
- Unity 中的 C# 脚本（MonoBehaviour、协程、ScriptableObjects）
- 场景设置和 GameObject 层级管理
- 物理系统（Rigidbody、Colliders、Joints、Character Controllers）
- 动画和 Animator 系统（Animation Clips、Blend Trees、State Machines）
- 渲染管线（Built-in、URP、HDRP）和着色器（ShaderLab、Shader Graph）
- UI 开发（UI Toolkit、UGUI、Canvas、TextMeshPro）
- XR/VR/AR 开发（XR Interaction Toolkit）
- 资源管理和优化
- 平台特定构建（iOS、Android、WebGL、PC/Console）
- 编辑器扩展和自定义工具

## Unity-MCP 集成

**此 Skill 可与 Unity-MCP 结合实现实时 Unity Editor 控制！**

**Unity Skill（文档）** + **Unity-MCP（操作）** = 完整的 AI 驱动开发

- **Unity Skill**：提供文档、模式和最佳实践（3,367 页）
- **Unity-MCP**：在 Unity Editor 中执行代码、创建资源和自动化工作流
- **结合使用**：从文档学习模式 → 立即应用到项目

**完整设置指南请参见 [UNITY_MCP_INTEGRATION.md](UNITY_MCP_INTEGRATION.md)。**

## 快速参考

### Unity 基本模式

#### 1. MonoBehaviour 生命周期
```csharp
using UnityEngine;

public class GameController : MonoBehaviour
{
    // 脚本实例加载时调用一次
    void Awake()
    {
        // 在 Start() 之前初始化引用和设置
    }

    // 第一帧更新前调用一次
    void Start()
    {
        // 依赖于其他对象的初始化逻辑
    }

    // 每帧调用
    void Update()
    {
        // 输入处理和基于帧的逻辑
    }

    // 以固定时间间隔调用（物理）
    void FixedUpdate()
    {
        // 物理相关代码（Rigidbody 力等）
    }

    // 所有 Update 函数完成后调用
    void LateUpdate()
    {
        // 相机跟随、后处理逻辑
    }

    // 对象变为激活/启用时调用
    void OnEnable() { }

    // 对象变为禁用/不活动时调用
    void OnDisable() { }

    // MonoBehaviour 将被销毁时调用
    void OnDestroy()
    {
        // 清理逻辑（取消订阅事件等）
    }
}
```

#### 2. 异步操作的协程
```csharp
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    void Start()
    {
        StartCoroutine(DelayedAction());
        StartCoroutine(FadeOut(GetComponent<SpriteRenderer>(), 2.0f));
    }

    // 简单延迟
    IEnumerator DelayedAction()
    {
        yield return new WaitForSeconds(2.0f);
        Debug.Log("2秒后执行");
    }

    // 淡出效果
    IEnumerator FadeOut(SpriteRenderer sprite, float duration)
    {
        float elapsed = 0f;
        Color startColor = sprite.color;

        while (elapsed < duration)
        {
            elapsed += Time.deltaTime;
            float alpha = Mathf.Lerp(1f, 0f, elapsed / duration);
            sprite.color = new Color(startColor.r, startColor.g, startColor.b, alpha);
            yield return null; // 等待下一帧
        }
    }
}
```

#### 3. 数据管理的 ScriptableObjects
```csharp
using UnityEngine;

[CreateAssetMenu(fileName = "New Weapon", menuName = "Game/Weapon")]
public class WeaponData : ScriptableObject
{
    public string weaponName;
    public int damage;
    public float fireRate;
    public Sprite icon;
    public GameObject projectilePrefab;
}

// 在 MonoBehaviour 中使用
public class WeaponSystem : MonoBehaviour
{
    [SerializeField] private WeaponData currentWeapon;

    public void Fire()
    {
        if (currentWeapon != null)
        {
            GameObject projectile = Instantiate(
                currentWeapon.projectilePrefab,
                transform.position,
                transform.rotation
            );
        }
    }
}
```

#### 4. 基于物理的移动
```csharp
using UnityEngine;

[RequireComponent(typeof(Rigidbody))]
public class PlayerMovement : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;
    [SerializeField] private float jumpForce = 10f;
    [SerializeField] private LayerMask groundLayer;

    private Rigidbody rb;
    private bool isGrounded;

    void Awake()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        // 检查是否在地面上
        isGrounded = Physics.Raycast(
            transform.position,
            Vector3.down,
            1.1f,
            groundLayer
        );

        // 移动
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        Vector3 movement = new Vector3(horizontal, 0f, vertical);
        rb.AddForce(movement * moveSpeed);
    }

    void Update()
    {
        // 跳跃
        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        }
    }
}
```

#### 5. 对象池模式
```csharp
using System.Collections.Generic;
using UnityEngine;

public class ObjectPool : MonoBehaviour
{
    [SerializeField] private GameObject prefab;
    [SerializeField] private int poolSize = 20;

    private Queue<GameObject> pool = new Queue<GameObject>();

    void Start()
    {
        for (int i = 0; i < poolSize; i++)
        {
            GameObject obj = Instantiate(prefab);
            obj.SetActive(false);
            pool.Enqueue(obj);
        }
    }

    public GameObject GetObject()
    {
        if (pool.Count > 0)
        {
            GameObject obj = pool.Dequeue();
            obj.SetActive(true);
            return obj;
        }
        else
        {
            // 如需要则扩展池
            GameObject obj = Instantiate(prefab);
            return obj;
        }
    }

    public void ReturnObject(GameObject obj)
    {
        obj.SetActive(false);
        pool.Enqueue(obj);
    }
}
```

#### 6. 单例模式
```csharp
using UnityEngine;

public class GameManager : MonoBehaviour
{
    private static GameManager _instance;

    public static GameManager Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = FindObjectOfType<GameManager>();

                if (_instance == null)
                {
                    GameObject go = new GameObject("GameManager");
                    _instance = go.AddComponent<GameManager>();
                }
            }
            return _instance;
        }
    }

    void Awake()
    {
        if (_instance != null && _instance != this)
        {
            Destroy(gameObject);
            return;
        }

        _instance = this;
        DontDestroyOnLoad(gameObject);
    }
}
```

#### 7. 事件系统模式
```csharp
using System;
using UnityEngine;

public class EventManager : MonoBehaviour
{
    public static event Action OnGameStart;
    public static event Action<int> OnScoreChanged;
    public static event Action OnGameOver;

    public static void TriggerGameStart()
    {
        OnGameStart?.Invoke();
    }

    public static void TriggerScoreChanged(int newScore)
    {
        OnScoreChanged?.Invoke(newScore);
    }

    public static void TriggerGameOver()
    {
        OnGameOver?.Invoke();
    }
}

// 使用：订阅和取消订阅
public class UIController : MonoBehaviour
{
    void OnEnable()
    {
        EventManager.OnScoreChanged += UpdateScoreDisplay;
        EventManager.OnGameOver += ShowGameOverScreen;
    }

    void OnDisable()
    {
        EventManager.OnScoreChanged -= UpdateScoreDisplay;
        EventManager.OnGameOver -= ShowGameOverScreen;
    }

    void UpdateScoreDisplay(int score)
    {
        // 更新 UI
    }

    void ShowGameOverScreen()
    {
        // 显示游戏结束
    }
}
```

#### 8. 2D 角色控制器
```csharp
using UnityEngine;

[RequireComponent(typeof(Rigidbody2D))]
public class CharacterController2D : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;
    [SerializeField] private float jumpForce = 10f;
    [SerializeField] private Transform groundCheck;
    [SerializeField] private LayerMask groundLayer;

    private Rigidbody2D rb;
    private bool isGrounded;
    private bool facingRight = true;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // 地面检测
        isGrounded = Physics2D.OverlapCircle(
            groundCheck.position,
            0.2f,
            groundLayer
        );

        // 移动输入
        float moveInput = Input.GetAxis("Horizontal");
        rb.velocity = new Vector2(moveInput * moveSpeed, rb.velocity.y);

        // 翻转角色
        if (moveInput > 0 && !facingRight)
            Flip();
        else if (moveInput < 0 && facingRight)
            Flip();

        // 跳跃
        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
        }
    }

    void Flip()
    {
        facingRight = !facingRight;
        Vector3 scale = transform.localScale;
        scale.x *= -1;
        transform.localScale = scale;
    }
}
```

#### 9. UI Toolkit（运行时 UI）
```csharp
using UnityEngine;
using UnityEngine.UIElements;

public class UIController : MonoBehaviour
{
    private UIDocument uiDocument;
    private Label scoreLabel;
    private Button startButton;

    void OnEnable()
    {
        uiDocument = GetComponent<UIDocument>();
        var root = uiDocument.rootVisualElement;

        // 查询元素
        scoreLabel = root.Q<Label>("score-label");
        startButton = root.Q<Button>("start-button");

        // 注册回调
        startButton.clicked += OnStartButtonClicked;
    }

    void OnDisable()
    {
        startButton.clicked -= OnStartButtonClicked;
    }

    void OnStartButtonClicked()
    {
        Debug.Log("游戏开始！");
    }

    public void UpdateScore(int score)
    {
        scoreLabel.text = $"分数：{score}";
    }
}
```

#### 10. 基础着色器（ShaderLab）
```shaderlab
Shader "Custom/SimpleTextureShader"
{
    Properties
    {
        _MainTex ("纹理", 2D) = "white" {}
        _Color ("着色颜色", Color) = (1,1,1,1)
        _Brightness ("亮度", Range(0, 2)) = 1
    }

    SubShader
    {
        Tags { "RenderType"="Opaque" }
        LOD 100

        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            #include "UnityCG.cginc"

            struct appdata
            {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
            };

            struct v2f
            {
                float2 uv : TEXCOORD0;
                float4 vertex : SV_POSITION;
            };

            sampler2D _MainTex;
            float4 _MainTex_ST;
            float4 _Color;
            float _Brightness;

            v2f vert (appdata v)
            {
                v2f o;
                o.vertex = UnityObjectToClipPos(v.vertex);
                o.uv = TRANSFORM_TEX(v.uv, _MainTex);
                return o;
            }

            fixed4 frag (v2f i) : SV_Target
            {
                fixed4 col = tex2D(_MainTex, i.uv);
                col *= _Color * _Brightness;
                return col;
            }
            ENDCG
        }
    }
}
```

## 参考文件

此 Skill 包含按主题在 `references/` 中组织的综合文档：

### 核心主题
- **[getting_started.md](references/getting_started.md)** - 安装、项目设置和 Unity 基础（4 页）
- **[scripting.md](references/scripting.md)** - C# 脚本、MonoBehaviour、协程、程序集（8 页）
- **[scene_management.md](references/scene_management.md)** - 场景创建、GameObjects、Transforms、Prefabs（38 页）

### 2D/3D 开发
- **[2d.md](references/2d.md)** - 精灵、瓦片地图、2D 物理、2D 动画（85 页）
- **[3d.md](references/3d.md)** - 3D 网格、地形、ProBuilder、光照（30 页）

### 系统
- **[physics.md](references/physics.md)** - Rigidbody、Colliders、Joints、Character Controllers（114 页）
- **[animation.md](references/animation.md)** - 动画剪辑、Animator、Timeline、Blend Trees（11 页）
- **[audio.md](references/audio.md)** - AudioSource、AudioMixer、空间音频（32 页）

### 渲染与图形
- **[rendering.md](references/rendering.md)** - 相机、光照、后处理、VFX（45 页）
- **[shaders.md](references/shaders.md)** - ShaderLab、Shader Graph、URP、HDRP、材质（631 页）

### UI 与界面
- **[ui.md](references/ui.md)** - UI Toolkit、UGUI、Canvas、TextMeshPro（16 页）

### 高级主题
- **[xr.md](references/xr.md)** - VR/AR 开发、XR Interaction Toolkit（238 页）
- **[editor.md](references/editor.md)** - 自定义编辑器、EditorWindows、MenuItem（8 页）
- **[optimization.md](references/optimization.md)** - 性能分析、内存管理、最佳实践（34 页）

### 平台与服务
- **[platform.md](references/platform.md)** - iOS、Android、WebGL、构建设置（16 页）
- **[assets.md](references/assets.md)** - 资源工作流、AssetBundles、Addressables（27 页）
- **[networking.md](references/networking.md)** - 多人游戏、Netcode、网络系统（19 页）
- **[services.md](references/services.md)** - Unity 服务、分析、云端构建（9 页）

### 附加资源
- **[other.md](references/other.md)** - 杂项主题和高级功能（1,707 页）
- **[index.md](references/index.md)** - 完整文档索引

**文档总计：** 3,367 页，来自官方 Unity 手册和脚本 API

需要详细信息时使用 `view` 工具读取特定参考文件。

## 使用此 Skill 

### 初学者
1. 从 [references/getting_started.md](references/getting_started.md) 开始了解 Unity 安装和基础
2. 复习上述 MonoBehaviour 生命周期模式
3. 在 [references/scene_management.md](references/scene_management.md) 中学习 GameObject 和 Transform 基础
4. 探索 [references/scripting.md](references/scripting.md) 中的简单脚本示例

### 中级开发者
1. 学习 [references/physics.md](references/physics.md) 中的物理系统
2. 使用 [references/animation.md](references/animation.md) 实现动画系统
3. 使用 [references/ui.md](references/ui.md) 构建 UI
4. 使用 [references/optimization.md](references/optimization.md) 优化性能

### 高级开发者
1. 创建自定义着色器：[references/shaders.md](references/shaders.md)
2. 构建自定义编辑器工具：[references/editor.md](references/editor.md)
3. 开发 VR/AR 体验：[references/xr.md](references/xr.md)
4. 针对特定平台优化：[references/platform.md](references/platform.md)

### 特定任务
- **2D 游戏：** 查看 [references/2d.md](references/2d.md) 了解 Sprites、Tilemaps、2D Physics
- **3D 游戏：** 查看 [references/3d.md](references/3d.md) 和 [references/rendering.md](references/rendering.md)
- **移动游戏：** 查看 [references/platform.md](references/platform.md) 了解 iOS/Android
- **多人游戏：** 探索 [references/networking.md](references/networking.md)
- **VR/AR：** 学习 [references/xr.md](references/xr.md)

## 核心概念

### Unity 架构
- **GameObjects：** 持有组件的容器对象
- **Components：** 模块化行为（Transform、Rigidbody、脚本等）
- **Prefabs：** 可重用的 GameObject 模板
- **Scenes：** 游戏的关卡或部分
- **Assets：** 项目中使用的文件（纹理、模型、音频等）

### 脚本最佳实践
- 使用 Awake() 进行初始化，Start() 进行设置
- 物理代码放在 FixedUpdate() 中
- 使用协程处理基于时间的操作
- 避免在 Update 循环中使用 FindObjectOfType()（缓存引用）
- 为频繁实例化的对象使用对象池
- 实现正确的事件清理（在 OnDisable/OnDestroy 中取消订阅）
- 使用 ScriptableObjects 存储游戏数据
- 遵循命名规范（公共用 PascalCase，私有用 camelCase）

### 性能优化
- 为静态对象启用静态批处理
- 为移动对象使用动态批处理
- 为远距离对象实现细节级别（LOD）
- 使用遮挡剔除跳过隐藏对象的渲染
- 使用 Unity Profiler 分析以识别瓶颈
- 通过共享材质优化绘制调用
- 使用对象池而非 Instantiate/Destroy
- 最小化 GetComponent 调用（缓存组件）
- 避免空的 Update 方法

### 物理技巧
- 使用图层和图层碰撞矩阵优化碰撞检测
- 选择合适的碰撞检测模式（Discrete vs Continuous）
- 使用 FixedUpdate 进行物理操作
- 对于简单检测，射线检测比碰撞器更便宜
- 尽可能使用 Physics.OverlapSphere 而非触发碰撞器
- 避免在使用物理时通过 Transform 移动对象（使用 Rigidbody）

### 渲染管线对比
- **Built-in：** 传统、功能全面、兼容性好
- **URP（通用）：** 现代、优化、移动友好、灵活
- **HDRP（高清）：** 高端图形、仅限 PC/Console

## 资源

### 官方文档
- Unity 手册：https://docs.unity3d.com/Manual/
- 脚本 API：https://docs.unity3d.com/ScriptReference/

### 学习资源
- Unity Learn：官方教程和课程
- Unity 博客：最新功能和最佳实践
- Unity 论坛：社区帮助和讨论

### 常用包
- **Input System** (com.unity.inputsystem)：现代输入处理
- **Cinemachine** (com.unity.cinemachine)：高级相机系统
- **ProBuilder** (com.unity.probuilder)：编辑器内 3D 建模
- **TextMeshPro**：高级文本渲染
- **XR Interaction Toolkit**：VR/AR 交互
- **Netcode for GameObjects**：多人游戏网络
- **Universal RP / HDRP**：渲染管线
- **Timeline**：电影级序列
- **Addressables**：高级资源管理

### 常用命名空间
```csharp
using UnityEngine;              // Unity 核心类
using UnityEngine.UI;           // UGUI 组件
using UnityEngine.UIElements;   // UI Toolkit
using UnityEngine.SceneManagement; // 场景加载
using System.Collections;       // 协程的 IEnumerator
using System.Collections.Generic; // Lists、Dictionaries
```

## scripts/
在此处添加用于常见自动化任务和实用程序的辅助脚本。

## assets/
在此处添加模板、样板代码或示例 Unity 项目文件。

## 说明

- 此 Skill 涵盖 Unity 2023.2+（兼容 Unity 6.x）
- 所有代码示例遵循 Unity C# 编码标准
- 参考文件链接到官方 Unity 文档
- 包含脚本参考 API 以获取详细的类信息
- URP（通用渲染管线）是新项目的推荐管线
- 始终在开发早期在目标平台上测试

## 更新

要使用最新的 Unity 文档刷新此 Skill ：
1. 使用最新版本 URL 更新 Unity 配置
2. 重新运行爬虫：`skill-seekers scrape --config configs/unity.json`
3. 该 Skill 将使用最新的 Unity 文档重新构建

---

*此 Skill 来自官方 Unity 文档（手册 + 脚本 API），涵盖 3,367 页全面的 Unity Engine 信息。*