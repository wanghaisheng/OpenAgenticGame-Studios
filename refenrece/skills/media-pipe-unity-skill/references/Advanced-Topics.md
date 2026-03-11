:construction:

# Getting output from stream
To receive output from a running graph, you need to setup `OutputStreamPoller` or `NativePacketCallback` before calling `CalculatorGraph#StartRun`.\
There are two main ways to do this.

Now suppose we want to get results from `HolisticLandmarkCpu`.

```txt
node {
  calculator: "HolisticLandmarkCpu"
  input_stream: "IMAGE:input_video"
  input_side_packet: "MODEL_COMPLEXITY:model_complexity"
  input_side_packet: "REFINE_FACE_LANDMARKS:refine_face_landmarks"
  output_stream: "POSE_LANDMARKS:pose_landmarks"
  output_stream: "WORLD_LANDMARKS:pose_world_landmarks"
  output_stream: "POSE_ROI:pose_roi"
  output_stream: "POSE_DETECTION:pose_detection"
  output_stream: "FACE_LANDMARKS:face_landmarks"
  output_stream: "LEFT_HAND_LANDMARKS:left_hand_landmarks"
  output_stream: "RIGHT_HAND_LANDMARKS:right_hand_landmarks"
}
```

## Synchronous API
You can get outputs synchronously with `OutputStreamPoller`.

### Before running `CalculatorGraph`

You need to initialize `OutputStreamPoller` before running the graph.

```cs
// NOTE: `POSE_LANDMARKS` type is `NormalizedLandmarkList`.
var poseLandmarksStreamPoler = calculatorGraph.AddOutputStreamPoller<NormalizedLandmarkList>("pose_landmarks");

// You can poll multiple streams at the same time.
// NOTE: `POSE_ROI` type is `NormalizedRect`;
var poseRoiStreamPoller = calculatorGraph.AddOutputStreamPoller<NormalizedRect>("pose_roi");
```

If the output is empty (e.g. no person in the input image), MediaPipe does not send output packets to the stream by default.
To get an empty packet when there's no output, specify `observeTimestampBounds` parameter (`false` by default).

> :bell: Since there is no other way to determine if the output is empty, it is basically better to set it to `true`.

```cs
var poseLandmarksStreamPoler = calculatorGraph.AddOutputStreamPoller<NormalizedLandmarkList>("pose_landmarks", true);
```

### After running `CalculatorGraph`

Once the graph is initialized, send input packets to the input stream, and wait for the output.

```cs
Packet inputPacket; // initialize it properly in the actual code
calculatorGraph.AddPacketToInputStream("input_video", inputPacket);

var poseLandmarksPacket = new Packet<NormalizedLandmarkList>();
if (poseLandmarksStreamPoller.Next(poseLandmarksPacket))
{
    if (poseLandmarksPacket.IsEmpty()) // when `observeTimestampBounds` is `true`, output packet can be empty
    {
        var poseLandmarks = packet.Get(NormalizedLandmarkList.Parser);
        // Do something
    }
}
```

> :bell: `OutputStreamPoller#Next` will block the thread.\
> This means if you've not set `observeOutputStream` to `true` and the output stream becomes empty, the whole application will hang.

## Asynchronous API
Using callbacks, You can also get outputs asynchronously.

To support platforms that require AOT compilation or [IL2CPP](https://docs.unity3d.com/Manual/IL2CPP.html) (e.g. iOS), you need to use lower level APIs.

### Callback Definitions

First, you need to define a callback (`NativePacketCallback`) that you want to be called by MediaPipe.

> :warning: The critical restrictions here are:
>    1. that the callback must be a _static_ method
>    2. that it is called from a thread other than the "main thread" (you cannot call most Unity APIs).

```cs
[AOT.MonoPInvokeCallback(typeof(CalculatorGraph.NativePacketCallback))]
private static IntPtr PoseLandmarksCallback(IntPtr graphPtr, IntPtr packetPtr)
{
    try
    {
        using (var packet = Packet<ValueType>.CreateForReference(packetPtr))
        {
            if (!packet.IsEmpty()) // when `observeTimestampBounds` is `true`, output packet can be empty
            {
                var output = packet.Get();
                // Do something
            }
        }
        // Return a pointer to the result status
        return Status.Ok().mpPtr;
    }
    catch (Exception e)
    {
        // Return a pointer to the result status
        return Status.FailedPrecondition(e.ToString()).mpPtr;
    }
}
```

The callback will receive 2 `IntPtr`s, the first is the pointer to the running `CalculatorGraph` and the second is the pointer to the output packet.

To get the output, you need to initialize an output packet from the pointer.
> :bell: The output packet is managed by C++ and you don't _own_ it.

```cs
using (var packet = Packet<ValueType>.CreateForReference(packetPtr))
```

But what is the first argument for?\
In fact, you can use it to access to the running `CalculatorGraph` instance.\
Of course you can access it if it's _static_ (in this case, you cannot still access to instance methods), but what if you wanted to save it to an instance variable?

Remember that those callback methods must be static. You usually cannot refer to instance variables or instance methods from static methods, but check out [how the sample app circumvents this restriction](https://github.com/homuler/MediaPipeUnityPlugin/blob/333279e132c9601b1809260732804eaede989d2a/Assets/Mediapipe/Samples/Scenes/Holistic/HolisticTrackingGraph.cs#L150-L159).

Finally, let's look at the return value.

The callback returns a pointer to a `Status` that represents the result status.\
Note that it must not throw exceptions because it is called from C++ code (so you may want to surround your code with try-catch block).

#### UnityEngine.UnityException: * can only be called from the main thread.

As mentioned above, the callback isn't called from the main thread, so you cannot call most Unity APIs.\
One way to avoid this error is to simply set the output value to a variable in the callback, and access later in the event functions (e.g. `Update`, `LateUpdate`).

See [sample code](https://github.com/homuler/MediaPipeUnityPlugin/blob/333279e132c9601b1809260732804eaede989d2a/Assets/Mediapipe/Samples/Scenes/Holistic/HolisticTrackingSolution.cs#L175-L178) for more details.

### Before running `CalculatorGraph`

You need to register callbacks before running the graph.

```cs
calculatorGraph.ObserveOutputStream("pose_landmarks", PoseLandmarksCallback);
```

If the output is empty (e.g. no person in the input image), MediaPipe does not send output packets to the stream by default.
If you want the callback to be called even when there's no output, specify `observeTimestampBounds` parameter (`false` by default).

```cs
calculatorGraph.ObserveOutputStream("pose_landmarks", PoseLandmarksCallback, true);
```

### After running `CalculatorGraph`

The registered callbacks will be called automatically.

## Which method to use?


# Adding Custom Calculators

# Adding Custom APIs

# Use Forked MediaPipe Repository

