# LumiFrame Windows 1.1.0-dev.217

This preview adds independent NVIDIA and AMD runtimes, first-run performance-based model selection, and main/settings screen repaint fixes.

## Download and install

Download the **launcher** ZIP plus your GPU channel, then extract them into the same **new** writable folder:

| GPU | Additional ZIPs required |
|---|---|
| AMD | `amd-win-x64.zip` |
| NVIDIA | `nvidia-win-x64.zip` **and** `nvidia-tensorrt-runtime-win-x64.zip` |
| Both channels | All three channel ZIPs |

All archive names begin with `LumiFrame-Windows-1.1.0-dev.217-`. Merge their `LumiFrame-Windows` folders and launch the top-level `LumiFrame.exe`. The 1.0.0 flat-folder runtime ZIP cannot replace the new NVIDIA channel ZIP. `SHA256SUMS.txt` lists checksums; the corresponding-source ZIP is not needed to run the app.

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
