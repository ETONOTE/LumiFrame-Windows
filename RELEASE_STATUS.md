# Release status

Last updated: **October 26, 2026**.

## Latest Windows download — NVIDIA + AMD

[Public 1.1.0-dev.230](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.230) includes the actual V3/CUGAN file-conversion improvements through local 230, with its final CUGAN optimization generalized for compatible target GPUs. [Download one Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.230/LumiFrame-Windows-1.1.0-dev.230-Setup.exe) for NVIDIA 230 and unchanged AMD 218. Setup downloads both channels with SHA-256 verification.

The latest CUGAN route requires SM 8.9 and actual 640 × 360 AI input. Other supported configurations retain the generic conversion path. Model weights, precision and quality limits remain unchanged. Read the [measurements, coverage and validation limits](RELEASE_NOTES_230.md).

Actual renderer/encoder comparisons passed against 225, 226, 229 and 230. Final binary output, frame/timestamp/audio, cancellation, cache/integrity, photo/playback and host checks passed. Isolated fresh and 223 upgrade installations and downloaded Setup are verified before Latest promotion. Existing installed230 development files and previous public assets are preserved.

**AMD and a second NVIDIA physical GPU remain untested here.** AMD 218 is identical to 223. This is an unsigned development build, not a Microsoft Store release. Internet is required during installation, but normal processing is local. No Android APK is included.

## AMD selection for the next unified release

At each new unified release, the application owner checks the current production release in [LumiFrame-AMD-Releases](https://github.com/ETONOTE/LumiFrame-AMD-Releases), reviews its AMD hardware validation and compatibility, and pins the selected AMD version, asset URLs and SHA256 values in the installer. Include the AMD update feature and verify fresh installation, upgrade, rollback and preservation of the NVIDIA channel and user settings before publication. Record the included AMD version in the unified release notes.

Existing unified installer assets remain unchanged between unified releases. AMD publication does not automatically rebuild them or change which AMD version an existing Setup downloads. Users with the in-app AMD updater can continue receiving AMD channel releases independently. See the [AMD update policy](updates/README.md).

## Previous Windows versions

[223](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.223) remains available as the previous unified NVIDIA/AMD installer. [1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) is an older NVIDIA-only release without AMD DirectML support. Use the latest unified Setup on AMD.

## Android

[Android notes](ANDROID.md) describe a separate closed-test track. This Windows release does not establish Play review or mobile validation status.
