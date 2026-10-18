# Release status

Last updated: **October 18, 2026**.

## Current Windows preview

[1.1.0-dev.217](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.217) integrates AMD DirectML and NVIDIA CUDA/TensorRT runtimes, independent GPU channel updates, first-run performance-based model selection, and main/settings repaint fixes. Download the [single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.217/LumiFrame-Windows-1.1.0-dev.217-Setup.exe); it includes both GPU channels and detects the GPU automatically on launch. The separate ZIPs are optional advanced packages. See [installation](README.md#windows-installation) and [release notes](RELEASE_NOTES_217.md).

32 NVIDIA and 27 AMD host regression tests passed. Actual NVIDIA playback and benchmark/UI flows were checked on RTX 4070 SUPER. **AMD physical hardware validation remains pending**; DirectML contract checks on NVIDIA do not certify AMD hardware. The short benchmark recommends a starting model; it does not guarantee full playback performance for every video.

This is an unsigned prerelease. It is not a Microsoft Store release and does not download updates automatically. Model preparation, input bounds, GPU memory and long-video compatibility remain limitations. No Android APK is included.

## Previous stable Windows version

[1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) remains available for NVIDIA users and rollback. Its application and TensorRT archives use the older flat-directory layout; they are not interchangeable with preview channel archives.

## Android

[Android notes](ANDROID.md) describe an earlier closed-test cycle. This Windows update does not establish current Play review status, tester eligibility or a newer mobile build's feature set. Mobile distribution and testing remain separate.
