# Release status

Last updated: **October 19, 2026**.

## Current Windows preview

[1.1.0-dev.218](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.218) integrates AMD DirectML and NVIDIA CUDA/TensorRT runtimes, independent GPU channel updates, first-run performance-based model selection, and main/settings repaint fixes. Download the [single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.218/LumiFrame-Windows-1.1.0-dev.218-Setup.exe); it includes both GPU channels and detects the GPU automatically on launch. The separate ZIPs are optional advanced packages. See [installation](README.md#windows-installation) and [release notes](RELEASE_NOTES_218.md).

Version 218 adds an always-visible installation folder selector and a once-only automatic performance check. Later measurements are manual in Settings; updates and GPU/driver changes do not start one automatically. Five targeted tests passed in each GPU build, and a real NVIDIA first run, saved-model restart after inventory changes, and explicit cancellation were checked. The broader 32 NVIDIA / 27 AMD host regression and short playback checks were completed for the preceding 217 version.

**AMD physical hardware validation remains pending**; DirectML contract checks on NVIDIA do not certify AMD hardware. The short benchmark recommends a starting model; it does not guarantee full playback performance for every video.

This is an unsigned prerelease. It is not a Microsoft Store release and does not download updates automatically. Model preparation, input bounds, GPU memory and long-video compatibility remain limitations. No Android APK is included.

## Previous stable Windows version

[1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) remains available for NVIDIA users and rollback. Its application and TensorRT archives use the older flat-directory layout; they are not interchangeable with preview channel archives.

## Android

[Android notes](ANDROID.md) describe an earlier closed-test cycle. This Windows update does not establish current Play review status, tester eligibility or a newer mobile build's feature set. Mobile distribution and testing remain separate.
