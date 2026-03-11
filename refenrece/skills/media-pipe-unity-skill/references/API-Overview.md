It is assumed that you have read the [Framework Concepts](https://google.github.io/mediapipe/framework_concepts/framework_concepts.html) article, so if you haven't read it yet, I recommend you do.

- [MediaPipe API](#mediapipe-api)
  - [CalculatorGraph](#calculatorgraph)
  - [CalculatorGraphConfig](#calculatorgraphconfig)
  - [Packet\<TValue\>](#packett)
  - [Timestamp](#timestamp)
  - [ImageFrame](#imageframe)
  - [Protocol Buffers](#protocol-buffers)
  - [Gpu Compute](#gpu-compute)
    - [GpuResources](#gpuresources)
    - [GlCalculatorHelper](#glcalculatorhelper)
    - [GpuBuffer](#gpubuffer)
    - [GlSyncPoint](#glsyncpoint)
  - [Logging](#logging)
- :construction: [MediaPipe Unity API](#mediapipe-unity-api)
  - [ResourceManager](#resourcemanager)
  - [OutputStream](#outputstream)
  - [CoordinateSystem](#coordinatesystem)
  - [Annotation](#annotation)

# MediaPipe API

> :warning: MediaPipe does not publish API documentation (AFAIK), so it is possible that the usage described in this wiki is incorrect.

## CalculatorGraph
> [mediapipe/framework/calculator_graph.h](https://github.com/google/mediapipe/blob/cf101e62a9d49a51be76836b2b8e5ba5c06b5da0/mediapipe/framework/calculator_graph.h)
> ```cpp
> // The class representing a DAG of calculator nodes.
> //
> // CalculatorGraph is the primary API for the MediaPipe Framework.
> // In general, CalculatorGraph should be used if the only thing you need
> // to do is run the graph (without pushing data in or extracting it as
> // the graph runs).
> ```

### Initialization
The simplest way is to initialize an instance with a text representing `CalculatorGraphConfig`.
```cs
var configText = "your favorite config";
var calculatorGraph = new CalculatorGraph(configText);
```

You can also initialize `CalculatorGraph` using `CalculatorGraphConfig`.

```cs
var configText = "your favorite config";
var config = CalculatorGraphConfig.Parser.ParseFromTextFormat(configText);
var calculatorGraph = new CalculatorGraph(config);
```

> :bulb: With the latter method, you can manipulate `CalculatorGraphConfig` freely, so you can modify the config dynamically.

See [CalculatorGraphConfig](#calculatorgraphconfig) for more details.

#### Enable GPU Compute 
When your target platform supports GPU compute, you can make use of it.
See [GPU Compute](#gpu-compute) for more details.

```cs
var gpuResources = GpuResources.Create();
calculatorGraph.SetGpuResources(gpuResources);
```

### Before Running
You need to do some work before running the `CalculatorGraph` to receive outputs from it.

#### Initialize OutputStreamPoller
`OutputStreamPoller` provides a synchronous, polling API for accessing a stream's output.

```cs
// Suppose the name of the output stream is `out` and the output type is `string`.
var poller = calculatorGraph.AddOutputStreamPoller<string>("out");
```

`OutputStreamPoller` won't return values by default if there's no output (e.g. faces are not detected in the input image).\
Because `OutputStreamPoller#Next` will block the thread until it gets a new value, this behavior can cause the entire application to hang.

To get an empty packet when there's no output, set `observeTimestampBounds` (the 2nd argument) to `true`.

```cs
var poller = calculatorGraph.AddOutputStreamPoller<string>("out", true);
```

#### Register NativePacketCallback
You can also add listeners, which will be invoked on every packet emitted by the output stream.\
Note that those listeners will be called from a thread other than the main thread, so you cannot call most of the Unity APIs in them.

```cs
// Suppose the name of the output stream is `out` and the output type is `string`.
calculatorGraph.ObserveOutputStream("out", Foo.Callback);

class Foo
{
  // NOTE: To support IL2CPP, NativePacketCallback must be static.
  [AOT.MonoPInvokeCallback(typeof(CalculatorGraph.NativePacketCallback))]
  private static IntPtr Callback(IntPtr graphPtr, int streamId, IntPtr packetPtr)
  {
    using (var packet = Packet.CreateForReference(packetPtr)) // `packetPtr` is a reference to the output packet
    {
      // ...
    }    
  }
}
```

As with `CalculatorGraph#AddOutputStreamPoller`, to emit an empty packet when there's no output, set `observeTimestampBounds` to `true`.

```cs
calculatorGraph.ObserveOutputStream("out", Foo.Callback, true);
```

### Start Running
```cs
calculatorGraph.StartRun();
```

If your graph receives `PacketMap` (= `SidePacket`), you can set it here.

```cs
var sidePacket = new PacketMap();

sidePacket.Emplace("num_faces", Packet.CreateInt(2));
sidePacket.Emplace("with_attention", Packet.CreateBool(true));

calculatorGraph.StartRun(sidePacket);
```

### During Running
#### Send input packets
```cs
var timestamp = 0;

// Suppose the name of the input stream is `in` and the input type is `string`.
calculatorGraph.AddPacketToInputStream("in", Packet.CreateStringAt("Hello World!", timestamp));
```

See [Timestamp](#timestamp) to know how to set up `Timestamp`.

#### Fetch Output Packets
To get output packets from `OutputStreamPoller`, you need to call `OutputStreamPoller#Next` explicitly.

```cs
// NOTE: this packet can be reused in a loop
var packet = new Packet<string>(); // initialize an empty packet

if (poller.Next(packet)) // `OutputStreamPoller#Next` will block the thread
{
  if (!packet.IsEmpty()) // if `observeTimestampBounds` is set to `true`, output packets can be empty
  {
    var value = packet.Get();
    // ...
  }
}
```

### After Running
If your work is done, dispose of `CalculatorGraph` to free up resources.

First, close the input source.

```cs
// Suppose the name of the input stream is `in`.
calculatorGraph.CloseInputStream("in");
```

If there are several input sources, you may want to close them at once.

```cs
calculatorGraph.CloseAllPacketSources();
```

After that, stop `CalculatorGraph`.

```cs
calculatorGraph.WaitUntilDone();
calculatorGraph.Dispose();
```

## CalculatorGraphConfig
> [mediapipe/framework/calculator.proto](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/framework/calculator.proto)
> ```proto
> // Describes the topology and function of a MediaPipe Graph.  The graph of
> // Nodes must be a Directed Acyclic Graph (DAG) except as annotated by
> // "back_edge" in InputStreamInfo.  Use a mediapipe::CalculatorGraph object to
> // run the graph.
> ```

This class represents the configuration of a `CalculatorGraph` and can be used to initialize the graph, but it is not necessary since `CalculatorGraph` can be also initialized with an equivalent string.

However, using `CalculatorGraphConfig`, you can modify the config easily at runtime (cf. [MediaPipeVideoGraph.cs](https://github.com/homuler/MediaPipeUnityPlugin/blob/5222faa9a21e1c523614f8c082b92ec521c2005b/Assets/Mediapipe/Samples/Scenes/MediaPipe%20Video/MediaPipeVideoGraph.cs#L83-L86)).

### Initialization
```cs
var configTxt = "your favorite config"; // this must not be null
var config = CalculatorGraphConfig.Parser.ParseFromTextFormat(configTxt); // throws if the format is invalid
```

### ValidatedGraphConfig
`CalculatorGraphConfig.Parser.ParseFromTextFormat` can be used to validate the format, but it doesn't validate the config itself (e.g. it can parse the config if some calculators don't exist).\
To validate the config, you can use the `ValidatedGraphConfig` API.

```cs
var config = CalculatorGraphConfig.Parser.ParseFromTextFormat("your favorite config");

using (var validatedGraphConfig = new ValidatedGraphConfig())
{
  validatedGraphConfig.Initialize(config); // throws if the config is not valid
}
```

The beauty of `ValidatedGraphConfig` is that it canonicalizes the `CalculatorGraphConfig`, expanding all the [subgraphs](https://google.github.io/mediapipe/framework_concepts/graphs.html#subgraph).\
That is, it enables us to access all the nodes of the graph at runtime.

The following code shows how to modify `CalculatorOptions` of `TensorsToDetectionsCalculator` (cf. [FaceDetectionGraph.cs](https://github.com/homuler/MediaPipeUnityPlugin/blob/5222faa9a21e1c523614f8c082b92ec521c2005b/Assets/Mediapipe/Samples/Scenes/Face%20Detection/FaceDetectionGraph.cs#L94-L106)).

```cs
using System.Linq;
using Google.Protobuf;

var config = CalculatorGraphConfig.Parser.ParseFromTextFormat("your favorite config");

using (var validatedGraphConfig = new ValidatedGraphConfig())
{
  validatedGraphConfig.Initialize(config);

  // NOTE: Calculator#Options is an [Extension](https://developers.google.com/protocol-buffers/docs/proto#extensions)
  //       To parse it, we need to initialize an `ExtensionRegistry`.
  var extensionRegistry = new ExtensionRegistry() { TensorsToDetectionsCalculatorOptions.Extensions.Ext };
  var canonicalizedConfig = validatedGraphConfig.Config(extensionRegistry);

  var tensorsToDetectionsCalculators = cannonicalizedConfig.Node.Where((node) => node.Calculator == "TensorsToDetectionsCalculator");

  foreach (var calculator in tensorsToDetectionsCalculators)
  {
    var options = calculator.Options.GetExtension(TensorsToDetectionsCalculatorOptions.Extensions.Ext);
    options.MinScoreThresh = 0.1; // modify `MinScoreThresh` at runtime
  }
}
```

## Packet\<T\>
> [mediapipe/framework/packet.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/framework/packet.h)
> ```cpp
> // A generic container class which can hold data of any type.  The type of
> // the data is specified when accessing the data (using Packet::Get<T>()).
> //
> // The Packet is implemented as a reference-counted pointer.  This means
> // that copying Packets creates a fast, shallow copy.  Packets are
> // copyable, movable, and assignable.  Packets can be stored in STL
> // containers.  A Packet may optionally contain a timestamp.
> ```

> ```cpp
> // This class is thread compatible.
> ```

`Packet` is used to communicate data with MediaPipe (cf. https://google.github.io/mediapipe/framework_concepts/framework_concepts.html#packet).

For example, if the input type is `string`, you cannot send a `string` directly to the `CalculatorGraph`, but need to initialize `Packet` which contains the data.\
The same is true when receiving the output, which is not the data itself, but a `Packet` that contains it.

### Initialization
To initialize an empty packet, call the default constructor.

```cs
// the data type is string
var stringPacket = new Packet<string>();
```

It is also possible to initialize a packet with the data.
To do so, call a `Packet.Create~` method.
These methods are similar to the official [packet_creator](https://developers.google.com/mediapipe/api/solutions/python/mp/packet_creator) APIs.

TODO: list all methods.

```cs
var stringPacket = Packet.CreateString("data");
var intPacket = Packet.CreateInt(0);
```

You can also set the timestamp at the initialization time.

> :bell: You need to set a timestamp to the input packet before sending it to MediaPipe (cf. https://google.github.io/mediapipe/framework_concepts/packets.html).

```cs
var stringPacket = Packet.CreateStringAt("data", 0);
var intPacket = Packet.CreateIntAt(0, 1);
```

If it's impossible to set the timestamp at the initialization time, you can set it after (not recommended).

```cs
var stringPacket = Packet.CreateString("data");

stringPacket = stringPacket.At(0);
```

There is one exceptional case where you need to initialize a packet using `IntPtr` (see [#Register NativePacketCallback](#register-nativepacketcallback)).

```cs
// NOTE: In such a case, you don't need to manage the Packet (it is managed by MediaPipe).
var stringPacket = Packet.CreateForReference(packetPtr);
```

### Get the value
You can use `Get` methods to read the value.

```cs
var stringPacket = Packet.CreateString("data");
var str = stringPacket.Get(); // "data"

var imageFramePacket = Packet.CreateImageFrame(imageFrame);
var imageFrame = imageFramePacket.Get();

// In a `NativePacketCallback`.
var handLandmarksPacket = Packet<NormalizedLandmarkList>.CreateForReference(packetPtr);

// If the packet can be empty, you need to check if it's empty before calling `Get`.
if (!handLandmarksPacket.IsEmpty())
{
  // For now, to get the proto message, you need to specify the parser.
  var handLandmarks = handLandmarksPacket.Get(NormalizedLandmarkList.Parser);
}
```

### Get the timestamp
```cs
var stringPacket = Packet.CreateStringAt("data", 10);
var timestamp = stringPacket.TimestampMicroseconds();

Debug.Log(timestamp); // 10
```

## Timestamp
Each `Packet` can have its `Timestamp`.\
When sending input packets to MediaPipe, the correct timestamp must be set for each packet.

> [mediapipe/framework/timestamp.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/framework/timestamp.h)
> ```cpp
> // A class which represents a timestamp in the calculator framework.
> // There are several special values which can only be created with the
> // static functions provided in this class.
> ```

### Initialization
There are 2 things that must be observed

1. The underlying value is in microseconds.
1. The timestamp value of the new packet must be greater than the previous packets.

It is usually a good idea to use elapsed microseconds since the start as the timestamp value.

```cs
var stopwatch = new System.Diagnostics.Stopwatch();
stopwatch.Start();

var currentTimestampMicrosec = stopwatch.ElapsedTicks / (TimeSpan.TicksPerMillisecond / 1000);
```

### Get its value
When working with output packets, you may want to know their timestamps.

```cs
var microsec = packet.TimestampMicroseconds(); // Get the value in microseconds.
```

## ImageFrame
> [mediapipe/framework/formats/image_frame.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/framework/formats/image_frame.h)
> ```cpp
> // A container for storing an image or a video frame, in one of several
> // formats.  Pixels are encoded row-major in an interleaved fashion.
> //
> // Formats supported by ImageFrame are listed in the ImageFormat proto.
> // It is the intention of ImageFormat to specify both the data format
> // and the colorspace used.  For example GRAY8 and GRAY16 both use the
> // same colorspace but have different formats.  Although it would be
> // possible to keep HSV, linearRGB, or BGR values inside an ImageFrame
> // (with format SRGB) this is an abuse of the class.  If you need a new
> // format, please add one to ImageFormat::Format.
> //
> // Do not assume that the pixel data is stored contiguously.  It may be
> // stored with row padding for alignment purposes.
> ```

This class is probably the most important API for using this plugin as you wish since if an image is used as input, which should be the case in most cases, it must always be converted to an `ImageFrame`.

### Initialization
To initialize an `ImageFrame` with pixel data, you need a pointer to the pixel data or a `NativeArray<byte>` that stores the pixel data.

```cs
using Unity.Collections;
using Unity.Collections.LowLevel.Unsafe;
using UnityEngine;

var width = 640;
var height = 480;
var format = ImageFormat.Types.Format.Srgba;

// From Texture2D
var texture2d = new Texture2D(width, height, TextureFormat.RGBA32, false);
var pixelData = texture2d.GetRawTextureData<byte>();

// `Deleter` is not required because you don't need to manage `pixelData`
// (cf. https://docs.unity3d.com/ScriptReference/Texture2D.GetRawTextureData.html).
// Instead, you need to keep `texture2d` during the corresponding `ImageFrame` is alive.

// NOTE: widthStep = channel * width (if there's no padding)
var imageFrame = new ImageFrame(format, width, height, 4 * width, pixelData);


// From NativeArray<byte>
class Foo
{
  public static pixelData;

  // NOTE: To support IL2CPP, ImageFrame.Deleter must be static.
  [AOT.MonoPInvokeCallback(typeof(ImageFrame.Deleter))]
  public static void Release(IntPtr _ptr) {
    pixelData.Dispose();
  }
}

Foo.pixelData = new NativeArray<byte>(width * height * 4, Allocator.Persistent,
                                      NativeArrayOptions.UninitializedMemory);
imageFrame = new ImageFrame(format, width, height, 4 * width, Foo.pixelData, Foo.Release);


// From NativeArray<byte>: XRCpuImage
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;

// ARCameraManager arCameraManager
pixelData = new NativeArray<byte>(width * height * 4, Allocator.Persistent,
                                  NativeArrayOptions.UninitializedMemoery);

if (arCameraManager.TryAcquireLatestCpuImage(out var image))
{
  var conversionParams = new XRCpuImage.ConversionParams(image, TextureFormat.RGBA32);
  var ptr = (IntPtr)NativeArrayUnsafeUtility.GetUnsafePtr(pixelData);
  image.Convert(conversionParams, ptr, pixelData.Length);
  image.Dispose();

  // NOTE:
  //   As long as you can guarantee that `pixelData` won't be overwritten while being referenced,
  //   you can reuse it.
  //   In that case, you don't need to implement `Deleter`.
  imageFrame = new ImageFrame(format, width, height, 4 * width, pixelData);
}
```

## Protocol Buffers
Many classes provided by this plugin are Protocol Buffer classes.

In fact, [CalculatorGraphConfig](#calculatorgraphconfig) is defined in [mediapipe/framework/calculator.proto](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/framework/calculator.proto).\
`Detection`, `NormalizedRect`, `NormalizedLandmark`, etc..., which are common output types for the official solutions, are also Protocol Buffer classes.

Their source files are automatically generated by `protoc` and output under the [`Scripts/Protobuf`](https://github.com/homuler/MediaPipeUnityPlugin/tree/b7742bc342f2fb1fdaa04f914dbe86637bc0519c/Packages/com.github.homuler.mediapipe/Runtime/Scripts/Protobuf) directory.\
To know which classes have which properties, check the original `.proto` files.

> :bell: In addition to that, it is highly recommended to enable code completion in your editor.\
>        cf. https://code.visualstudio.com/docs/other/unity#_enabling-code-completion-for-recent-versions-of-unity

## GPU compute
If GPU compute is supported on your target platform, you can enable it.
To make use of GPU, you need to initialize `GpuResources` and set it to your `CalculatorGraph`.

```cs
var gpuResources = GpuResources.Create();
calculatorGraph.SetGpuResources(gpuResources);

// `SetGpuResources` must be called before `StartRun`.
calculatorGraph.StartRun();
```

### GpuResources
You can initialize `GpuResources` using `GpuResources.Create`.\
See also [mediapipe/gpu/gpu_shared_data_internal.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/gpu/gpu_shared_data_internal.h).

```cs
var gpuResources = GpuResources.Create(); // throws if GPU computing is not supported.
```

When the [Graphics API](https://docs.unity3d.com/Manual/GraphicsAPIs.html) is OpenGL ES, you can share the context with MediaPipe (cf. https://google.github.io/mediapipe/framework_concepts/gpu.html#opengl-es-support).

```cs
// NOTE: The following code is a bit hackish. If you know a better way, please let us know!

using Mediapipe;
using System.Collections;
using UnityEngine;

class GpuInitializer
{
  private static IntPtr _CurrentContext = IntPtr.Zero;
  private static bool _IsContextInitialized = false;

  private delegate void PluginCallback(int eventId);

  [AOT.MonoPInvokeCallback(typeof(PluginCallback))]
  private static void GetCurrentContext(int eventId) {
    _CurrentContext = Egl.GetCurrentContext(); // This API is ported by this plugin.
    _IsContextInitialized = true;
  }

  public IEnumerator Initialize()
  {
    // You need to get the current context first.
    PluginCallback callback = GetCurrentContext;

    var fp = Marshal.GetFunctionPointerForDelegate(callback);
    GL.IssuePluginEvent(fp, 1);

    yield return new WaitUntil(() => _IsContextInitialized);

    // Call `GpuResources.Create` with the current context.
    var gpuResources = GpuResources.Create(_CurrentContext);
    // ...
  }
}
```

### GlCalculatorHelper
> [mediapipe/gpu/gl_calculator_helper.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/gpu/gl_calculator_helper.h)
> ```cpp
> // Helper class that manages OpenGL contexts and operations.
> // Calculators that implement an image filter, taking one input stream of
> // frames and producing one output stream of frame, should subclass
> // GlSimpleCalculatorBase instead of using GlCalculatorHelper directly.
> // Direct use of this class is recommended for calculators that do not fit
> // that mold (e.g. calculators that combine two video streams).
> ```

This class is useful when you'd like to manipulate a `GpuBuffer` instance.

#### Initialization
```cs
var gpuResources = GpuResources.Create();
var glCalculatorHelper = new GlCalculatorHelper();
glCalculatorHelper.InitializeForTest(gpuResources);
```

#### Examples
1. Convert `ImageFrame` to `GpuBuffer` and send it to your `CalculatorGraph`[^1].

   cf. [mediapipe/examples/desktop/demo_run_graph_main_gpu.cc](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/examples/desktop/demo_run_graph_main_gpu.cc#L124-L137).

   ```cs
   glCalculatorHelper.RunInGlContext(() => {
     var texture = glCalculatorHelper.CreateSourceTexture(imageFrame);
     var gpuBuffer = texture.GetGpuBufferFrame();

     Gl.Flush();
     texture.Release();

     return calculatorGraph.AddPacketToInputStream("in", Packet.CreateGpuBufferAt(gpuBuffer, 0));
   });
   ```

2. Build a `GpuBuffer` instance from a `Texture`.

   See `GpuBuffer`(#gpubuffer).

[^1]: You should usually use the `ImageFrameToGpuBufferCaclulator` to do this.

### GpuBuffer
> [mediapipe/gpu/gpu_buffer.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/gpu/gpu_buffer.h)
> ```cpp
> // This class wraps a platform-specific buffer of GPU data.
> // An instance of GpuBuffer acts as an opaque reference to the underlying
> // data object.
> ```

In most cases, you don't need to use `GpuBuffer` APIs on Unity, but when Unity shares its OpenGL ES context with MediaPipe, you may want to use them for performance (see also [`GpuResources`](#gpuresources)).

```cs
// Texture texture = your_source_texture;

var glTextureName = (uint)texture.GetNativeTexturePtr();
var glBufferFormat = GpuBufferFormat.kBGRA32; // BGRA32 is the only supported format currently.
var glContext = glCalculatorHelper.GetGlContext();
var glTextureBuffer = new GlTextureBuffer(glTextureName, texture.width, texture.height,
                                          glBufferFormat, Foo.OnRelease, glContext);
var gpuBuffer = new GpuBuffer(glTextureBuffer);

class Foo
{
  // NOTE: To support IL2CPP, DeletionCallback must be static.
  [AOT.MonoPInvokeCallback(typeof(GlTextureBuffer.DeletionCallback))]
  private static void OnRelease(uint textureName, IntPtr syncTokenPtr)
  {
    if (syncTokenPtr == IntPtr.Zero)
    {
      return;
    }
    using (var glSyncToken = new GlSyncPoint(syncTokenPtr))
    {
      glSyncToken.Wait();
    }
  }
}
```

### GlSyncPoint
> [mediapipe/gpu/gl_context.h](https://github.com/google/mediapipe/blob/c6c80c37452d0938b1577bd1ad44ad096ca918e0/mediapipe/gpu/gl_context.h)
> ```cpp
> // Generic interface for synchronizing access to a shared resource from a
> // different context. This is an abstract class to keep users from
> // depending on its contents. The implementation may differ depending on
> // the capabilities of the GL context.
> ```

This class is rarely used, but if you'd like to initialize a `GpuBuffer` instance, you need to know it because `GlSyncPoint` is passed to the `GlTextureBuffer.DeletionCallback` as the 2nd argument (`IntPtr`).\
See also [GpuBuffer](#gpubuffer).

```cs
// NOTE: To support IL2CPP, DeletionCallback must be static.
[AOT.MonoPInvokeCallback(typeof(GlTextureBuffer.DeletionCallback))]
private static void OnRelease(uint textureName, IntPtr syncTokenPtr)
{
  if (syncTokenPtr == IntPtr.Zero)
  {
    return;
  }
  using (var glSyncToken = new GlSyncToken(syncTokenPtr))
  {
    // Waits until the GPU has executed all commands up to the sync point.
    // This blocks the CPU, and ensures the commands are complete from the
    // point of view of all threads and contexts.
    glSyncToken.Wait();

    // Ensures that the following commands on the current OpenGL context will
    // not be executed until the sync point has been reached.
    // This does not block the CPU, and only affects the current OpenGL context.
    glSyncToken.WaitOnGpu();

    // Returns whether the sync point has been reached. Does not block.
    if (glSyncToken.isReady())
    {
      // ...
    }
  }
}
```

## Logging
### Logger
This plugin uses the `Mediapipe.Unity.Logger` class to output logs.

> :bell: You need to enable `Development Build` to see the log.

You can change the log level to get more verbose logs.

```cs
Logger.MinLogLevel = Logger.LogLevel.Debug;
```

### Glog
MediaPipe uses [Google Logging Library](https://github.com/google/glog) internally and this plugin ports APIs to configure it.\
See also [glog#setting-flags](https://github.com/google/glog#setting-flags).

```cs
Glog.Logtostderr = true; // Log messages to stderr (i.e. Editor.log, Player.log) instead of log files.
Glog.Minloglevel = 0; // default = 0
Glog.V = 0; // default = 0

Glog.Initialize("MediaPipeUnityPlugin"); // call `Initialize` after setting flags
```

### Protobuf
Protobuf will log messages to stdout or stderr by default.\
You can overwrite the `google::protobuf::LogHandler` so that the output appears in the Console Window.

```cs
Protobuf.SetLogHandler(Protobuf.DefaultLogHandler);

// Restore the default LogHandler before the program exits.
// Otherwise, the protobuf will retain the stale pointer, which may eventually cause SIGSEGV.
Protobuf.ResetLogHandler();
```

# MediaPipe Unity API
## ResourceManager

## OutputStream

## CoordinateSystem

## Annotation