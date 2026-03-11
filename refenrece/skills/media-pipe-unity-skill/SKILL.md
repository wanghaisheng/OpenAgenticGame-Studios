---
name: media-pipe-unity
description: MediaPipe Unity Plugin 集成。用于计算机视觉任务、手部/面部/姿态追踪、手势识别、目标检测以及 Unity 中的 ML 解决方案。
---

# MediaPipe Unity Plugin Skill

Google MediaPipe 在 Unity 中的完整集成，提供手部追踪、面部检测、姿态识别、手势识别、目标检测等计算机视觉和机器学习解决方案。

## 何时使用此 Skill 

在以下情况下触发此 Skill ：
- MediaPipe Unity Plugin (homuler/com.github.homuler.mediapipe)
- 计算机视觉任务 (Computer Vision Tasks)
- 手部关键点检测 (Hand Landmark Detection)
- 面部检测和关键点 (Face Detection & Landmarks)
- 姿态关键点检测 (Pose Landmark Detection)
- 手势识别 (Gesture Recognition)
- 目标检测 (Object Detection)
- 图像分割 (Image Segmentation)
- 音频分类 (Audio Classification)
- 自定义 Calculator 图 (Custom Calculator Graph)
- GPU 推理优化 (GPU Inference)

## 快速参考

### Hello World - 基础示例

```csharp
using Mediapipe;
using UnityEngine;

public sealed class HelloWorld : MonoBehaviour
{
    private const string ConfigText = @"
input_stream: ""in""
output_stream: ""out""
node {
  calculator: ""PassThroughCalculator""
  input_stream: ""in""
  output_stream: ""out1""
}
node {
  calculator: ""PassThroughCalculator""
  input_stream: ""out1""
  output_stream: ""out""
}
";

    private void Start()
    {
        using var graph = new CalculatorGraph(ConfigText);
        using var poller = graph.AddOutputStreamPoller<string>("out");
        graph.StartRun();

        for (var i = 0; i < 10; i++)
        {
            graph.AddPacketToInputStream("in", Packet.CreateStringAt("Hello World!", i));
        }

        graph.CloseInputStream("in");
        var packet = new Packet<string>();

        while (poller.Next(packet))
        {
            Debug.Log(packet.Get());
        }
        graph.WaitUntilDone();
    }
}
```

### 1. CalculatorGraph - 核心图管理

```csharp
using Mediapipe;
using UnityEngine;

public class GraphExample : MonoBehaviour
{
    private CalculatorGraph _graph;

    void Start()
    {
        // 初始化图
        var configText = @"
input_stream: ""input_video""
output_stream: ""output_video""
node {
  calculator: ""PassThroughCalculator""
  input_stream: ""input_video""
  output_stream: ""output_video""
}
";
        _graph = new CalculatorGraph(configText);

        // 启用 GPU 推理（可选）
        // var gpuResources = GpuResources.Create();
        // _graph.SetGpuResources(gpuResources);

        // 添加输出流监听器
        _graph.StartRun();
    }

    void OnDestroy()
    {
        // 清理资源
        _graph?.CloseAllPacketSources();
        _graph?.WaitUntilDone();
        _graph?.Dispose();
    }
}
```

### 2. Task API - 现代化解决方案接口

```csharp
using Mediapipe.Tasks.Vision.HandLandmarker;
using Mediapipe.Tasks.Vision.Core;
using UnityEngine;

public class HandDetectionExample : MonoBehaviour
{
    private HandLandmarker _handLandmarker;

    void Start()
    {
        // 创建 Hand Landmarker
        var options = new HandLandmarkerOptions
        {
            BaseOptions = new BaseOptions(ModelAssetPath: "hand_landmarker.task"),
            RunningMode = RunningMode.LIVE_STREAM,
            NumHands = 2,
            MinHandDetectionConfidence = 0.5f,
            MinHandPresenceConfidence = 0.5f,
            MinTrackingConfidence = 0.5f
        };

        _handLandmarker = HandLandmarker.CreateFromOptions(options);
    }

    void Update()
    {
        // 检测手部关键点
        var image = new Mediapipe.Tasks.Vision.Image();
        // ... 设置图像数据
        var result = _handLandmarker.Detect(image);
    }

    void OnDestroy()
    {
        _handLandmarker?.Dispose();
    }
}
```

### 3. Legacy Solution - 图运行器模式

```csharp
using Mediapipe.Unity.Sample;
using UnityEngine;

public class SolutionRunner : GraphRunner
{
    // 配置文件在 Inspector 中设置
    // [SerializeField] private TextAsset _cpuConfig;

    protected override void ConfigureCalculatorGraph(CalculatorGraphConfig config)
    {
        // 配置输出流
        calculatorGraph.Initialize(config);
        // 输出流设置...
    }

    public override void StartRun(ImageSource imageSource)
    {
        // 启动推理
        StartRun(new PacketMap());
    }

    protected override IList<WaitForResult> RequestDependentAssets()
    {
        // 加载模型文件
        return new List<WaitForResult>
        {
            WaitForAsset("model.binarypb")
        };
    }
}
```

### 4. 图像输入处理

```csharp
using Mediapipe;
using Mediapipe.Unity.Sample;
using UnityEngine;

public class ImageInputExample : MonoBehaviour
{
    private ImageSource _imageSource;

    void Start()
    {
        // 使用 WebCam 作为输入源
        _imageSource = ImageSourceProvider.ImageSource;
        StartCoroutine(_imageSource.Play());
    }

    void Update()
    {
        if (!_imageSource.isPrepared) return;

        // 获取当前帧
        var currentTexture = _imageSource.GetCurrentTexture();

        // 创建 ImageFrame
        var imageFrame = new ImageFrame(
            ImageFormat.Types.Format.SRGBA,
            currentTexture.width,
            currentTexture.height,
            currentTexture.GetRawTextureData(),
            ImageFrame.Types.GlFormatInfo.ForUnityTextureFormat(currentTexture.format)
        );

        // 发送到 CalculatorGraph
        // graph.AddPacketToInputStream("input_video", Packet.CreateImageFrameAt(imageFrame, timestamp));
    }
}
```

### 5. 处理输出结果

```csharp
using Mediapipe;
using UnityEngine;

public class OutputHandler : MonoBehaviour
{
    // 使用 OutputStreamPoller 同步获取结果
    void ProcessOutputSync()
    {
        var poller = _graph.AddOutputStreamPoller<float[]>("landmarks");

        while (true)
        {
            var packet = new Packet<float[]>();
            if (poller.Next(packet))
            {
                var landmarks = packet.Get();
                // 处理关键点数据
            }
        }
    }

    // 使用 NativePacketCallback 异步获取结果
    void ProcessOutputAsync()
    {
        _graph.ObserveOutputStream("landmarks", LandmarkCallback);

        [AOT.MonoPInvokeCallback(typeof(CalculatorGraph.NativePacketCallback))]
        private static IntPtr LandmarkCallback(IntPtr graphPtr, int streamId, IntPtr packetPtr)
        {
            using (var packet = Packet.CreateForReference<float[]>(packetPtr))
            {
                var landmarks = packet.Get();
                // 处理关键点数据（注意：在非主线程执行）
            }
            return IntPtr.Zero;
        }
    }
}
```

## 支持的解决方案

### 视觉解决方案

| Solution | Description | Android | iOS | Linux | macOS | Windows |
|----------|-------------|:-------:|:---:|:-----:|:-----:|:-------:|
| **Object Detection** | 目标检测 | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Face Detection** | 面部检测 | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Face Landmark Detection** | 面部关键点检测 (468点) | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Hand Landmark Detection** | 手部关键点检测 (21点) | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Gesture Recognition** | 手势识别 | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Pose Landmark Detection** | 姿态关键点检测 (33点) | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Image Segmentation** | 图像分割 | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Image Classification** | 图像分类 | - | - | - | - | - |
| **Image Embedding** | 图像嵌入 | - | - | - | - | - |

### 音频解决方案

| Solution | Description | Android | iOS | Linux | macOS | Windows |
|----------|-------------|:-------:|:---:|:-----:|:-----:|:-------:|
| **Audio Classification** | 音频分类 | ✓ | ✓ | ✓ | ✓ | ✓ |

### 传统解决方案

以下解决方案可通过 [MediaPipe Framework](https://ai.google.dev/edge/mediapipe/framework) 使用，但官方已停止支持：
- Holistic Tracking
- Face Mesh
- Hand Tracking
- Pose Tracking
- Objectron
- Instant Motion Tracking

## API 概览

### 核心 API

#### CalculatorGraph
MediaPipe Framework 的主要 API，用于构建和运行计算图。

**快速开始:**
```csharp
// 初始化
var graph = new CalculatorGraph(configText);

// GPU 模式
var gpuResources = GpuResources.Create();
graph.SetGpuResources(gpuResources);

// 运行
graph.StartRun();
graph.AddPacketToInputStream("input", packet);
graph.CloseInputStream("input");
graph.WaitUntilDone();
```

**详细文档:** [references/API-Overview.md](references/API-Overview.md#calculatorgraph)

#### Packet<T>
MediaPipe 中数据传递的基本单位。

**类型支持:**
```csharp
// 基本类型
Packet.CreateString("text")
Packet.CreateInt(42)
Packet.CreateBool(true)
Packet.CreateFloat(3.14f)

// 媒体类型
Packet.CreateImageFrame(imageFrame)
Packet.CreateGpuBuffer(gpuBuffer)

// 自定义时间戳
Packet.CreateStringAt("text", timestampMicrosec)
```

**详细文档:** [references/API-Overview.md](references/API-Overview.md#packett)

#### OutputStreamPoller
同步轮询输出流的数据。

```csharp
// 创建轮询器
var poller = graph.AddOutputStreamPoller<float[]>("landmarks");

// 获取数据（阻塞直到有新数据）
var packet = new Packet<float[]>();
if (poller.Next(packet)) {
    var data = packet.Get();
}

// 使用 observeTimestampBounds 处理空包
var poller = graph.AddOutputStreamPoller<float[]>("landmarks", true);
```

**详细文档:** [references/API-Overview.md](references/API-Overview.md#outputstream)

### 任务 API

Task API 提供了更高级的接口，简化了常见任务的使用。

#### HandLandmarker
手部关键点检测和手势识别。

```csharp
var options = new HandLandmarkerOptions {
    BaseOptions = new BaseOptions(ModelAssetPath: "hand_landmarker.task"),
    NumHands = 2,
    MinHandDetectionConfidence = 0.5f
};
var landmarker = HandLandmarker.CreateFromOptions(options);
var result = landmarker.Detect(image);

// 访问结果
foreach (var landmarks in result.Landmarks) {
    foreach (var landmark in landmarks) {
        Debug.Log($"({landmark.X}, {landmark.Y}, {landmark.Z})");
    }
}
```

#### FaceDetector / FaceLandmarker
面部检测和关键点识别。

```csharp
// Face Detection
var detector = FaceDetector.CreateFromOptions(options);
var detectionResult = detector.Detect(image);

// Face Landmark Detection
var landmarker = FaceLandmarker.CreateFromOptions(options);
var landmarkResult = landmarker.Detect(image);
```

#### PoseLandmarker
姿态关键点检测。

```csharp
var landmarker = PoseLandmarker.CreateFromOptions(options);
var result = landmarker.Detect(image);

// 33 个姿态关键点
// PoseLandmark 类定义了所有关键点索引
```

**更多 Task API:** [references/Tutorial-Task-API.md](references/Tutorial-Task-API.md)

### Unity 特定 API

#### ImageSource
图像输入源管理（Webcam、视频文件、静态图片）。

```csharp
// 获取图像源
var imageSource = ImageSourceProvider.ImageSource;

// 配置图像源
imageSource.SourceType = ImageSourceType.WebCamera;
imageSource.WebCameraDeviceIndex = 0;

// 启动
yield return imageSource.Play();

// 获取当前帧
var texture = imageSource.GetCurrentTexture();
```

#### GraphRunner
Unity 中 CalculatorGraph 的抽象基类，简化了图的生命周期管理。

```csharp
public class MyGraphRunner : GraphRunner
{
    protected override void ConfigureCalculatorGraph(CalculatorGraphConfig config)
    {
        // 配置图
        calculatorGraph.Initialize(config);
    }

    public override void StartRun(ImageSource imageSource)
    {
        // 启动推理
    }

    protected override IList<WaitForResult> RequestDependentAssets()
    {
        // 加载模型和资源
        return new List<WaitForResult> {
            WaitForAsset("model.binarypb")
        };
    }
}
```

## 参考文件

此 Skill 包含来自 homuler/MediaPipeUnityPlugin 的完整文档，位于 `references/` 目录：

### 入门指南
- **[Getting-Started.md](references/Getting-Started.md)** - 构建、安装和测试完整指南
- **[Tutorial-Hello-World.md](references/Tutorial-Hello-World.md)** - Hello World 教程
- **[Tutorial-Task-API.md](references/Tutorial-Task-API.md)** - Task API 使用教程

### API 文档
- **[API-Overview.md](references/API-Overview.md)** - 核心 API 概览 (CalculatorGraph, Packet, GpuResources, etc.)

### 高级主题
- **[Advanced-Topics.md](references/Advanced-Topics.md)** - 高级用法和自定义计算器
- **[Installation-Guide.md](references/Installation-Guide.md)** - 详细安装指南
- **[FAQ.md](references/FAQ.md)** - 常见问题解答

### 项目 README
- **[MediaPipeUnityPlugin-README.md](references/MediaPipeUnityPlugin-README.md)** - 项目 README 和示例说明

## 使用此 Skill 

### 初学者
1. 阅读 [references/Tutorial-Hello-World.md](references/Tutorial-Hello-World.md) 了解基本概念
2. 运行项目中的示例场景（`Assets/MediaPipeUnity/Samples/Scenes/`）
3. 查看 Hello World 示例（`Assets/MediaPipeUnity/Tutorial/Hello World/HelloWorld.cs`）

### 常见任务
- **手部追踪:** 查看 `HandLandmarkerRunner.cs` 和 Hand Landmark Detection 场景
- **面部检测:** 查看 `FaceDetectorRunner.cs` 和 Face Detection 场景
- **姿态识别:** 查看 `PoseLandmarkerRunner.cs` 和 Pose Landmark Detection 场景
- **目标检测:** 查看 `ObjectDetectorRunner.cs` 和 Object Detection 场景

### 高级用户
1. 研究 [references/API-Overview.md](references/API-Overview.md) 了解底层 API
2. 阅读 [references/Advanced-Topics.md](references/Advanced-Topics.md) 学习自定义 Calculator
3. 参考官方 MediaPipe 文档: https://ai.google.dev/edge/mediapipe

## 平台支持

| Platform | CPU | GPU | Notes |
|----------|:---:|:---:|-------|
| **Linux (x86_64)** | ✓ | ✓ | 推荐用于开发 |
| **macOS (Intel)** | ✓ | ✗ | GPU 不支持 |
| **macOS (ARM64)** | ✓ | ✗ | GPU 不支持 |
| **Windows (x86_64)** | ✓ | ✗ | GPU 实验性支持 |
| **Android** | ✓ | ✓ | 需要 OpenGL ES 3.0+ |
| **iOS** | ✓ | ✓ | 需要 Metal |
| **WebGL** | ✗ | ✗ | 不支持 |

> **注意:** GPU 模式在 macOS 和 Windows 上不支持。Windows 上 GPU 推理为实验性功能。

## 技术限制

### UnityEditor 可能崩溃
由于 MediaPipe 使用原生库，某些错误可能导致 UnityEditor 崩溃（尤其是在 Windows 上）。
- Linux 和 macOS 上插件处理了 SIGABRT 信号以避免崩溃
- Windows 上无法正确处理 SIGABRT

### Graphics API
使用 GPU 推理时，不能使用 OpenGL Core API，否则会出现错误：
```
InternalException: INTERNAL: ; eglMakeCurrent() returned error 0x3000
```
**解决方案:** 在 PC Standalone 构建中切换到 Vulkan。

### 模型文件位置
- UnityEditor: 使用 Local 模式（默认）
- 设备构建: 使用 StreamingAssets 模式，需要将模型文件复制到 `StreamingAssets/` 目录

### Android 构建注意事项
需要确保 APK 中包含 `libstdc++_shared.so`，否则会抛出 `DllNotFoundException`。

## 核心概念

### MediaPipe 架构
- **CalculatorGraph:** 计算图，连接多个 Calculator 节点
- **Calculator:** 计算节点，处理输入并产生输出
- **Packet:** 数据包，在图中传递数据的基本单位
- **InputStream / OutputStream:** 输入和输出流
- **SidePacket:** 侧包，用于传递配置参数

### 图配置
使用文本格式配置计算图：
```text
input_stream: "input_video"
output_stream: "output_video"
node {
  calculator: "PassThroughCalculator"
  input_stream: "input_video"
  output_stream: "output_video"
}
```

### 坐标系统
- **Unity:** 左下角为原点 (0, 0)
- **MediaPipe:** 右上角为原点 (0, 0)
- 需要进行坐标转换（参见 `CoordinateSystem` 类）

### 推理模式
- **CPU:** 使用 CPU 计算，兼容性好
- **GPU:** 使用 GPU 加速，性能更好（在支持的平台上）
- **OpenGL ES:** Android 平台优化的 GPU 模式

## 资源

### 官方资源
- **MediaPipe GitHub:** https://github.com/google/mediapipe
- **MediaPipe Unity Plugin:** https://github.com/homuler/MediaPipeUnityPlugin
- **MediaPipe 官方文档:** https://ai.google.dev/edge/mediapipe
- **MediaPipe Concepts:** https://ai.google.dev/edge/mediapipe/framework/framework_concepts/overview

### 示例场景位置
示例场景位于项目中的 `Assets/MediaPipeUnity/Samples/Scenes/`：
- `Face Detection/`
- `Face Landmark Detection/`
- `Hand Landmark Detection/`
- `Pose Landmark Detection/`
- `Object Detection/`
- `Image Segmentation/`
- `Legacy/` (传统解决方案)

### 常用命名空间
```csharp
using Mediapipe;                          // 核心 API
using Mediapipe.Tasks.Vision;             // 视觉任务
using Mediapipe.Tasks.Vision.HandLandmarker;  // 手部检测
using Mediapipe.Unity.Sample;             // 示例代码
```

## scripts/
帮助脚本和自动化工具可放在此处。

## assets/
模板、样板代码或示例 Unity 项目文件可放在此处。

## 说明

- 此 Skill 基于 **MediaPipe Unity Plugin v0.10.22** (homuler)
- 支持 Unity 2022.3+
- 参考文档来自官方 GitHub Wiki
- Task API 是推荐的使用方式，Legacy Solution 仅用于兼容
- 首次使用建议运行示例场景验证安装

---

*此 Skill 基于 [homuler/MediaPipeUnityPlugin](https://github.com/homuler/MediaPipeUnityPlugin) 的官方文档和示例生成。*