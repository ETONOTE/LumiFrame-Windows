# Release status

Last updated: **October 22, 2026**.

## Latest Windows download — NVIDIA + AMD

[1.1.0-dev.223](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.223) extends faster first-time NVIDIA V3/CUGAN preparation beyond 640 × 360. Download the [single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.223/LumiFrame-Windows-1.1.0-dev.223-Setup.exe); it automatically downloads and installs NVIDIA 223 and unchanged AMD 218, with SHA-256 verification. Internet is required during installation. See [installation](README.md#windows-installation) and [release notes](RELEASE_NOTES_223.md).

GitHub's Latest release and the main download link now point to this 223 unified installer. The download listing changed on October 22; the installer and all runtime/model asset bytes are unchanged. This remains a development build with the validation limits below.

Models, precision, AI input settings and the playback path are preserved. Comparisons passed for 42 model/input combinations, with seven representative GPU reruns after the Windows long-path correction. Separate audio/video sync and cache fallback checks passed. The local offline installer passed fresh/upgrade installation and 14 installed-GUI comparisons against the validated candidate. Measurements used RTX 4070 SUPER; other physical GPUs were not benchmarked.

Prepared engines apply only when actual input width × height and hardware/runtime conditions match the included inventory. Some V3 shapes and the retained 640 × 360 engines support Ampere or newer; additional CUGAN shapes require SM 8.9. Unsupported shapes, missing/corrupt bundles or incompatible hardware use the original preparation path. See the release notes for exact coverage and exclusions.

The installation folder selector, separate GPU channels and once-only initial performance check remain. Updates preserve saved preferences; later measurements are manual in Settings. The NVIDIA compatibility policy introduced in 219 remains: GTX 1060 / Pascal uses Anime4K Fast/Quality. CUDA neural models are not ported to Pascal, and video export retains the bundled NVENC driver requirement of 570 or newer.

**AMD and GTX 1060 physical hardware validation remain pending.** AMD 218 is unchanged. This is an unsigned development build, not a Microsoft Store release. It does not download application updates automatically. GPU memory and long-video compatibility remain limits. No Android APK is included.

## Previous NVIDIA-only Windows version

[1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) remains available for NVIDIA users and rollback. It does not include the AMD DirectML channel; AMD users should use the 223 unified installer above. Its application and TensorRT archives use the older flat-directory layout; they are not interchangeable with preview channel archives.

## Android

[Android notes](ANDROID.md) describe an earlier closed-test cycle. This Windows update does not establish current Play review status, tester eligibility or a newer mobile build's feature set. Mobile distribution and testing remain separate.
