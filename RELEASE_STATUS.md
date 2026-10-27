# Release status

Last updated: **October 27, 2026**.

## Windows 231 — NVIDIA + AMD + Intel

[231 Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/LumiFrame-Windows-1.1.0-dev.231-Setup.exe) adds an independent Intel Vulkan channel and downloads all three channels through one installer, with pinned SHA256 checks on five archives. [Public 230](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.230) remains available for rollback.

The included channel versions are **NVIDIA 230, AMD 218 and Intel 231**. NVIDIA/AMD runtime and model files are retained byte-for-byte; the local and installed-payload checks verified all 674 protected channel files. Their GPU selection order, model choices, settings and once-only startup benchmark behavior remain unchanged. Intel is the automatic fallback when no eligible NVIDIA/AMD adapter exists, or can be selected explicitly.

Intel provides Anime4K Fast/Quality playback and photo conversion, including original/upscaled comparison. It starts with Fast without a startup model benchmark and keeps separate settings. The Intel channel includes neither CUDA models nor the AMD DirectML model, and does not offer the NVENC video-file conversion workflow.

Local GPU-selection, settings, updater and regression checks passed. Packaged Intel-runtime playback and photo conversion were exercised through the shared Vulkan path on a NVIDIA development GPU. **Physical Intel hardware has not been tested; these checks are not Intel performance measurements.** See the [231 notes](RELEASE_NOTES_231.md) for exact completed checks and limitations.

Offline fresh installation and a 230-to-231 update passed in isolated portable fixtures. The public Setup was then downloaded without GitHub authentication, matched the shipping SHA256, and passed a separate fresh installation using all five public archives. Each fixture verified all 925 payload files, the 674 unchanged NVIDIA/AMD files, channel versions and preserved fixture preferences. The real user's existing product registration, shortcuts and preferences remained unchanged. These are portable-fixture checks; they do not claim a fresh interactive registration/shortcut installation test.

An installed-package NVIDIA CUGAN comparison passed the existing raw-image limits on one captured frame, but the pixels were not exactly identical. This is a limited regression check, not a new quality or FPS result; the unchanged binary-file hashes are a separate finding.

The unchanged NVIDIA 230 runtime retains its V3/CUGAN conversion work. The latest CUGAN route requires SM 8.9 and actual 640 × 360 AI input; other supported configurations keep the generic conversion path. Model weights, precision and quality limits are unchanged. The [230 measurements and coverage](RELEASE_NOTES_230.md) remain results from that release, not new 231 measurements.

**Physical AMD hardware and a second NVIDIA GPU also remain untested here.** This is an unsigned development build, not a Microsoft Store release. Internet is required during installation, but normal processing is local. No Android APK is included.

## AMD selection for each unified release

At each new unified release, the application owner checks the current production release in [LumiFrame-AMD-Releases](https://github.com/ETONOTE/LumiFrame-AMD-Releases), reviews its AMD hardware validation and compatibility, and pins the selected AMD version, asset URLs and SHA256 values in the installer. Release 231 retains the same AMD 218 bytes as 230, preserving the existing compatibility scope. This identifies the included version and does not claim that 218 is the latest independent AMD release.

Existing unified installer assets remain unchanged between unified releases. AMD publication does not automatically rebuild them or change which AMD version an existing Setup downloads. Users with the in-app AMD updater can continue receiving AMD channel releases independently. See the [AMD update policy](updates/README.md). The Intel compatibility change does not rebuild the AMD runtime or alter that existing update policy.

## Previous Windows versions

[230](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.230) remains available as the previous unified NVIDIA/AMD installer. [223](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.223) also remains available. [1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) is an older NVIDIA-only release without AMD DirectML support. Use the 231 unified Setup for the Intel channel.

## Android

[Android notes](ANDROID.md) describe a separate closed-test track. This Windows release does not establish Play review or mobile validation status.
