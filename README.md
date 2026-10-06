# LumiFrame for Windows

GPU-accelerated video playback and image/video upscaling.

## Download and run

Download **both** files for [0.1.0 Beta 1](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v0.1.0-beta.1):

1. [Application ZIP](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v0.1.0-beta.1/LumiFrame-Windows-0.1.0-beta.1-win-x64.zip) - 1.17 GB
2. [Required AI runtime ZIP](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v0.1.0-beta.1/LumiFrame-Windows-0.1.0-beta.1-tensorrt-runtime.zip) - 1.63 GB

Extract both into the **same writable folder**, merging their `LumiFrame-Windows` folders. Run **`LumiFrame-Windows/AniEdge.exe`**. Do not run it inside the ZIP.

You do not need the corresponding-source or GitHub "Source code" archives to run the app. `SHA256SUMS.txt` is available to verify downloads.

## Before you start

- Windows x64, NVIDIA GPU with CUDA/Vulkan driver support, and Microsoft Visual C++ x64 runtime required. Tested on RTX 4070 SUPER; other GPUs are not yet validated.
- First-time AI preparation may take several minutes. Later launches reuse cached plans.
- Experimental, unsigned beta with a Korean interface. Performance varies; 30 FPS is not guaranteed for every engine or video.

## Support and licenses

[Report a problem](https://github.com/ETONOTE/LumiFrame-Windows/issues). Include your GPU, selected engine and reproduction steps; remove personal information from attachments.

Third-party terms and notices are included in the app. Matching sources and build recipes for LGPL libraries (FFmpeg, libplacebo and libiconv) are in the [corresponding-source archive](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v0.1.0-beta.1/LumiFrame-Windows-0.1.0-beta.1-corresponding-source.zip).
