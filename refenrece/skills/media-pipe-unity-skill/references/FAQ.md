# Build/Installation
## Is there any negative impact on performance by using Docker?

Docker is only used to build native libraries, not at runtime, so there is no impact on performance.\
It is possible that the build time will increase (especially when the host OS is Windows), but unless you are building libraries repeatedly, it should be much less stressful than installing all the dependent tools manually.

## How much CPU and memory should be allocated to a Docker container?
You don't need to mind this issue if your host OS is Linux, but on Windows, you need to specify `--cpus` and `--memory` option when starting a container.

According to my rule of thumb, it is better to adjust the parameters as follows (this doesn't apply if you have too little memory):

1. When starting [Windows container](https://github.com/homuler/MediaPipeUnityPlugin/wiki/Installation-Guide#docker-windows-container), allocate more than `1.2g * [cpus]` memory.

   ```bat
   docker run --cpus=8 --memory=10g -it mediapipe_unity:windows
   ```

1. But if you'd like to build libraries for Android on Windows container, allocate more than `1.5g * [cpus]` memory.

   ```bat
   docker run --cpus=8 --memory=12g -it mediapipe_unity:windows
   ```

1. On the other hand, when starting [Linux container](https://github.com/homuler/MediaPipeUnityPlugin/wiki/Installation-Guide#docker-linux-container), allocate more than `1g * [cpus]` memory.

   ```bat
   docker run --cpus=8 --memory=8g -it mediapipe_unity:linux
   ```

## How to reduce the plugin size?

Strip symbols from native libraries. See [Build Command](https://github.com/homuler/MediaPipeUnityPlugin/wiki/Installation-Guide#build-command) for more details.

# Development
## UnityEditor crashes!
When some errors occur, MediaPipe doesn't throw an exception but aborts the whole program (signals `SIGABRT`).\
It is not fatal in production since the application should crash in such a situation after all, but in a development environment, it is very annoying since the UnityEditor crashes.

On Linux and macOS, this plugin avoids UnityEditor crashing by handling `SIGABRT`, so if UnityEditor crashes, please let us know!\
On Windows, there seem to be no ways to handle `SIGABRT` properly, so if you cannot tolerate this, use a different OS.

## InternalException: INTERNAL: ; eglMakeCurrent() returned error 0x3000

If you encounter an error like below and you use OpenGL Core as the Unity's graphics APIs, please try Vulkan.

```txt
InternalException: INTERNAL: ; eglMakeCurrent() returned error 0x3000_mediapipe/mediapipe/gpu/gl_context_egl.cc:261)
```