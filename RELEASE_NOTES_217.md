# LumiFrame Windows 1.1.0-dev.217

This preview adds independent NVIDIA and AMD runtimes, first-run performance-based model selection, and main/settings screen repaint fixes.

## Download and install — one file

**[Download LumiFrame-Windows-1.1.0-dev.217-Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.217/LumiFrame-Windows-1.1.0-dev.217-Setup.exe)**

Run this one installer, then open LumiFrame. **Both NVIDIA and AMD runtimes and models are installed automatically.** The app automatically detects the GPU and starts its matching channel; the first launch measures the available models to recommend a starting model. No GPU-specific download selection or ZIP merging is required.

Setup automatically downloads and verifies both GPU channels, so **internet is required during installation** (about 2.9 GB download / 3.8 GB installed, plus temporary space). No further downloads are needed for ordinary use or benchmarking. It installs for the current user, creates a Start menu shortcut and includes an uninstaller. A desktop shortcut is optional. GPU drivers and the Microsoft Visual C++ x64 runtime remain system prerequisites. [SHA256SUMS-Setup.txt](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.217/SHA256SUMS-Setup.txt) contains the installer checksum.

Packaging correction: the initial ZIP-only publication exposed the internal channel split to users. The unified installer fixes that installation experience; application/model bytes and GPU detection behavior are unchanged. GPU-specific ZIPs remain available only for advanced manual deployment and independent channel updates. They are not additional downloads required by Setup.

## Changes

- The launcher detects eligible NVIDIA/AMD adapters and selects the one with the most dedicated VRAM. AMD requires DirectX 12; software adapters are excluded. Both channels use the same LumiFrame interface.
- AMD runs the supplied Old-film Denoise Real-CUGAN Pro x2 model through DirectML. NVIDIA keeps its CUDA/TensorRT models. Executables, DLLs, model files, settings and benchmark caches are separate.
- `Update-Channel.ps1` verifies a complete channel package and atomically switches only that channel. Previous versions are retained. This installs downloaded local packages; it does not download updates automatically.
- First launch measures actual GPU completion using synthetic 640x360 input and 1920x1080 output. It targets 30 fps with P95 <= 25 ms and P99 <= 30 ms. It prefers the highest eligible application tier, then lower P95 within that tier; if none meets the budget, it uses the fastest completed model. Failed candidates are excluded.
- NVIDIA measures Anime4K Fast/Quality, E6, Hybrid, V3 and CUGAN. AMD measures Anime4K Fast/Quality and AMD CUGAN. The synthetic test excludes media decoding, audio and display refresh; live Auto still adapts to actual video load.
- Measurement allows skipping, has a 45-second per-model / 150-second total limit, and caches results. GPU, driver, runtime and model changes invalidate the cache. Existing manually saved choices are preserved; Settings can remeasure and apply an automatic choice.
- Main/settings window scrolling, resizing and maximize/restore now repaint the parent and moved child controls without retaining stale pixels.

## Validation and known limits

32 NVIDIA and 27 AMD host regression tests passed. Real NVIDIA V3 playback presented 12 synthetic frames with zero drops, fallback or CUDA errors. The UI checks covered progress, cancellation, settings migration, remeasurement and cache reuse. On the RTX 4070 SUPER test host, one short run selected Hybrid at approximately 9.1 ms P95; this is not a broad hardware or sustained playback claim.

**AMD physical hardware validation remains pending.** DirectML output-contract tests ran on the NVIDIA host; they do not certify AMD drivers or AMD performance. AMD AI inputs are limited to even dimensions and 720p area; use a 360p/480p working height for larger sources. Its inference path currently includes CPU transfer buffers. This preview is unsigned and Intel-only systems are not supported by the launcher. Long-video conversion and first-use model preparation limitations still apply.

AMD model bytes are unchanged. The project owner confirmed public redistribution permission on October 18, 2026; upstream notices are included. Third-party LGPL library bytes and their matching corresponding-source archive are unchanged from 1.0.0. No Android APK is included.
