# LumiFrame

![LumiFrame — local video playback and AI upscaling](docs/assets/lumiframe-banner.svg)

**[LumiFrame 231 Setup (NVIDIA + AMD + Intel)](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/LumiFrame-Windows-1.1.0-dev.231-Setup.exe)** · [Getting started](#windows-installation) · [Report an issue](https://github.com/ETONOTE/LumiFrame-Windows/issues) · [Roadmap](ROADMAP.md) · [Privacy](PRIVACY.md)

**NVIDIA, AMD and Intel users share one unified installer.** The new Intel Vulkan channel provides Anime4K Fast/Quality playback and photo conversion. NVIDIA 230 and AMD 218 are retained unchanged. This is an unsigned development build; physical Intel and AMD hardware validation is pending. Version 1.0.0 is an older NVIDIA-only download.

GPU-accelerated video playback and image/video upscaling, with a focus on animation. Processing runs on your computer; media is not uploaded to an upscaling server.

LumiFrame integrates NVIDIA, AMD and Intel runtimes behind one interface. On first launch, NVIDIA and AMD retain their existing once-only model measurement and recommendation. Intel starts with Anime4K Fast without a startup benchmark; Quality can be selected manually. The Windows interface supports Korean and English; use the language button beside Help.

This repository hosts **Windows downloads, documentation and issue reports**, plus separate Android test information. It is not the application source repository.

## Upscaling example

![Yu Yu Hakusho: the same full 360p frame, with ordinary display scaling on the left and LumiFrame AnimeVideo-v3 on the right](docs/assets/yuyuhakusho-v3-360p-to1080p.png)

**Left:** the 480 × 360 source frame enlarged with bicubic display scaling. **Right:** the same frame processed by LumiFrame 1.0.0 with AnimeVideo-v3, using the full 480 × 360 AI input and a 1440 × 1080 output. Both sides retain the original 4:3 aspect ratio; neither is cropped or additionally sharpened.

This scene illustrates cleaner facial and hair outlines, not a universal quality guarantee. Upscaling can also simplify texture or faint detail. The source artwork is from *Yu Yu Hakusho* and belongs to its respective rights holders; it is not licensed as LumiFrame artwork, and no affiliation or endorsement is implied.

## Downloads

| Platform | Status | Download |
|---|---|---|
| Windows x64, NVIDIA, AMD or Intel | **1.1.0-dev.231 development build**; installer checks passed; Intel/AMD physical hardware validation pending | [One installer for all three channels](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/LumiFrame-Windows-1.1.0-dev.231-Setup.exe) |
| Windows x64, NVIDIA only | Legacy 1.0.0; no AMD DirectML support | [Previous NVIDIA-only download](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) |
| Android | Separate closed-test track; no APK in this Windows release | [Earlier Android test notes](ANDROID.md) |

The AMD integration uses the teammate's [AniEdge for AMD](https://github.com/KORTibetfox/AniEdge-for-AMD) model and DirectML integration. Its upstream project remains separate; the unified download above runs inside LumiFrame.

### Windows installation

1. Download **[LumiFrame-Windows-1.1.0-dev.231-Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/LumiFrame-Windows-1.1.0-dev.231-Setup.exe)**.
2. Run Setup, choose the installation folder, and install LumiFrame. **This one installer automatically installs NVIDIA, AMD and Intel runtimes and the models included with each channel.** No GPU-specific download selection or manual ZIP merging is needed.
3. Open **LumiFrame** from the Start menu (or the optional desktop shortcut). It detects the GPU automatically and starts the matching runtime. NVIDIA/AMD keep the once-only initial benchmark; Intel opens directly with Anime4K Fast.

Setup automatically downloads five archives: the launcher, NVIDIA runtime/models, NVIDIA TensorRT libraries, AMD runtime/models, and Intel runtime. Every archive is checked with its pinned SHA256 before installation. **Internet is required during installation**; allow space for the downloads, installed files and temporary extraction. After installation, normal use and benchmarking are offline. Setup always shows the destination folder page, including during reinstallation. The default is `%LOCALAPPDATA%\Programs\LumiFrame`, and files are inside its `LumiFrame-Windows` subfolder. Setup installs for the current user without administrator privileges. GPU drivers and the Microsoft Visual C++ x64 runtime remain system prerequisites. [Installer SHA256](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/SHA256SUMS-Setup.txt) verifies the download.

Release 231 installs **unchanged NVIDIA 1.1.0-dev.230, unchanged AMD 1.1.0-dev.218, and new Intel 1.1.0-dev.231**. Channel files, settings and update versions remain separate. NVIDIA/AMD benchmark caches and manual choices are preserved; Intel has its own settings and no startup benchmark cache.

The public Setup was downloaded without GitHub authentication, matched the shipping SHA256, and completed a fresh installation in an isolated portable fixture. All five downloaded archives and 925 installed payload files were verified, including the 674 unchanged NVIDIA/AMD files and preserved preferences. Separate offline fresh-install and 230-to-231 update fixtures also passed. These checks preserve the real user's existing registration, shortcuts and settings; physical Intel validation remains outstanding.

The existing NVIDIA/AMD selection order is preserved: the eligible adapter with most dedicated VRAM wins, with the existing adapter-index tie break. Intel is the automatic fallback when no eligible NVIDIA/AMD adapter is present. An explicit `--backend intel`, `--backend amd` or `--backend nvidia` selects a present GPU family. Adding Intel does not redirect a working NVIDIA/AMD installation to its integrated GPU.

After installing, launch LumiFrame from the new Start menu entry or the top-level `LumiFrame-Windows/LumiFrame.exe`. The application footer shows its channel version: NVIDIA `1.1.0-dev.230`, AMD `1.1.0-dev.218`, or Intel `1.1.0-dev.231`. A footer showing `1.0.0` means an older executable is still running; check the shortcut target.

Keep your previous portable version for rollback. The standard installer creates a Start menu shortcut and an uninstaller. Advanced portable extraction is available with `Setup.exe /PORTABLE=1 /DIR="C:\LumiFrame"`.

<details>
<summary>Advanced: manual portable packages and individual channel updates</summary>

The separate launcher, AMD, NVIDIA, NVIDIA TensorRT and Intel ZIPs on the [release page](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.231) remain available for manual deployment and GPU-specific updates. **They are not required when using Setup.** Manual NVIDIA deployment requires both NVIDIA ZIPs. Extract manual packages into the same new `LumiFrame-Windows` folder and run its top-level `LumiFrame.exe`.

The [ZIP checksums](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/SHA256SUMS.txt) apply to those original assets. The 1.0.0 runtime ZIP uses an older directory layout. Corresponding-source and GitHub source-code ZIPs are not installation packages.

</details>

## What's new

- Release 231 adds an independent Intel Vulkan channel for Anime4K Fast/Quality playback and photo conversion, including original/upscaled comparison. The previous launcher rejected Intel-only PCs before opening the application.
- NVIDIA 230 and AMD 218 runtime/model files are retained byte-for-byte. Their existing GPU selection order, model choices, settings and startup benchmark behavior are preserved.
- Intel opens without the NVIDIA/AMD startup benchmark and saves settings separately. CUDA models, AMD DirectML models and NVENC video-file conversion are not included in the Intel channel.
- Local policy, updater and shared Vulkan-path checks passed, followed by isolated offline fresh/update and publicly downloaded Setup fresh-install checks. Shared Vulkan playback/photo checks ran on a NVIDIA development GPU and do not establish Intel hardware compatibility or performance. See [231 release notes](RELEASE_NOTES_231.md).

### Retained from NVIDIA 230

- Public 230 includes faster actual V3/CUGAN video-file conversion while preserving models, input settings and the existing quality limits.
- The final CUGAN improvement now uses architecture-compatible TensorRT engines and creates cuDNN plans on each target PC. It applies to SM 8.9 GPUs with actual 640 × 360 AI input; other supported configurations use the existing compatible route.
- NVIDIA 230 and unchanged AMD 218 retain GPU detection, separate channel settings and their once-only initial benchmark.
- The earlier 223 preparation improvements remain included. Actual conversion measurements and full compatibility/validation limits are in the [230 release notes](RELEASE_NOTES_230.md).

## First-run model selection

The launcher detects hardware without reading user media. It excludes software adapters and requires DirectX 12 for AMD. The following existing measurement policy applies to **NVIDIA and AMD**. Intel does not run it: Intel starts with Anime4K Fast and offers Fast/Quality directly. NVIDIA and AMD benchmark their own engines with a moving synthetic **640 × 360 input → 1920 × 1080 output**.

- Four warm-up frames are excluded; 32–120 frames are measured through actual GPU completion.
- The target is **30 fps**, with spare time for playback: **P95 ≤ 25 ms and P99 ≤ 30 ms**.
- Choose the highest eligible application tier; among peers, choose lower P95. If none meets the budget, choose the fastest successfully measured model. Failed or incomplete candidates cannot win.
- NVIDIA measures the compatible subset of Anime4K Fast/Quality, E6, Hybrid, V3 and CUGAN. GTX 1060 / Pascal uses the two Anime4K candidates. CUDA neural candidates require compute capability 7.5 or newer and CUDA 13 driver support; CUGAN must also pass its memory admission policy. AMD measures Anime4K Fast/Quality and AMD CUGAN as before.
- Preparation can take up to 45 seconds per model, bounded to 150 seconds overall. You can skip. The automatic check runs only once. Later launches, updates and GPU/driver changes do not run it again; use Settings to remeasure manually. Cancelling or failing the initial check also leaves later measurements manual. Existing 217 measurements are preserved.
- Previously saved manual choices are preserved. A model incompatible with the detected NVIDIA hardware uses a compatible session fallback without rewriting that saved preference. **Settings → remeasure and automatically select a model** explicitly applies a new recommendation, using Auto / 360p AI input / 1080p output.

This measures a short synthetic workload, not image quality or full video decoding/audio/display performance. It cannot guarantee 30 fps for every video. Live Auto continues to respond to real playback load. [More benchmark details](BENCHMARK.md).

## Engines and playback

| Channel | Engines |
|---|---|
| All three channels | Anime4K Fast and Quality |
| NVIDIA | E6 / EfRLFN, Hybrid, AnimeVideo-v3, CUGAN; Anime 6B for conversion only |
| AMD | Old-film Denoise Real-CUGAN Pro x2 through DirectML |
| Intel | Anime4K Fast/Quality only; no CUDA or AMD DirectML models |

V3, Hybrid and NVIDIA CUGAN are peer playback options, not a universal quality ranking. NVIDIA Auto falls back from the selected heavy engine through E6 and Anime4K. AMD Auto uses AMD CUGAN and Anime4K. Intel Auto stays within the selected Anime4K tier: Quality can fall back to Fast, while Fast stays Fast. Auto does not switch among every peer model to classify scenes. File conversion retains the selected engine.

Choose a local video, allow initial model preparation, then play. Pause, seek, adjust volume, capture a frame, or use F11 / Esc for fullscreen. Preferences include original/upscaled split comparison on all channels. Intel supports photo conversion with Anime4K and original/result viewing; Intel video-file conversion is unavailable because the current video export route requires NVIDIA NVENC. Existing NVIDIA/AMD conversion behavior is unchanged.

AI input height is separate from source and output resolution. Processing a 720p source at 360p before producing 1080p lowers cost but can discard detail. Window size is also separate from the upscaling target.

## Updating one GPU channel

Close LumiFrame and extract a newer channel's complete ZIP(s) into a temporary folder. For NVIDIA, combine both NVIDIA archives. Run the installed script against the extracted **version folder**:

```powershell
./Update-Channel.ps1 -PackageFolder "C:/extracted/LumiFrame-Windows/runtimes/amd/NEW-VERSION" -Channel amd
```

Use `-Channel nvidia` for NVIDIA or `-Channel intel` for Intel. The installer verifies the full `channel.json` inventory, installs the new version and changes only that channel's `current.txt`. It retains `previous.txt` and old files. Restart to activate. To roll back while closed, copy that channel's `previous.txt` over `current.txt`.

Updates require a new version directory. This script installs local packages; it does not download updates automatically.

## Requirements and known limits

- Windows x64, current Vulkan drivers, and the Microsoft Visual C++ x64 runtime. NVIDIA CUDA neural models require compute capability 7.5 or newer and CUDA 13 driver support. Older NVIDIA GPUs use Vulkan Anime4K; AMD needs DirectX 12. Intel needs a compatible Vulkan driver and uses the separate Anime4K channel.
- GTX 1060 compatibility is covered by policy fixtures, but **GTX 1060 physical hardware validation is pending**. CUDA neural models have not been ported to Pascal. Video export retains the bundled NVENC driver requirement of 570 or newer.
- **Intel physical hardware validation is pending.** Intel-channel playback and photo output were checked through the shared Vulkan path on a NVIDIA development GPU, alongside channel-selection and settings tests. These checks are not Intel driver, sustained playback or FPS measurements. Intel supports neither CUDA/AMD DirectML models nor NVENC video-file conversion. Original comparison and Anime4K photo conversion remain available.
- **AMD physical hardware validation is pending.** Both builds and shared policy tests passed on the NVIDIA development host, but AMD drivers, sustained playback and performance still require an AMD PC.
- AMD model inputs require even dimensions and at most 720p area. Use 360p/480p AI height for larger sources. Its GPU inference currently uses CPU transfer buffers.
- This is an unsigned development build; it is not a Microsoft Store release. Previous releases, including unified 230 and NVIDIA-only 1.0.0, remain available for rollback.
- Version 223 accelerates supported V3/CUGAN shapes; first-time preparation for other combinations may still be lengthy. GPU memory, input shape and background load affect performance. All-model 30 FPS and large long-video speedups are not promised.
- An earlier whole-file V3 audio-drain timeout remains a compatibility follow-up. Short passing tests do not certify every file.
- Upscaling can smooth or reconstruct faces, fine lines and texture incorrectly. It does not provide motion interpolation or recover guaranteed original detail.

## Troubleshooting

**AMD PC reports a CUDA / `cuInit` error:** check the running version and shortcut target. Version 1.0.0 uses the NVIDIA path. Install the 231 unified Setup above and launch its top-level LumiFrame or new Start menu entry. The included AMD channel uses DirectML and displays `1.1.0-dev.218` in the footer.

**Intel PC reports an unsupported GPU before the app opens:** the previous unified launcher excluded Intel-only systems. Release 231 adds the Intel Vulkan channel. Install the 231 unified Setup and launch its top-level LumiFrame or new Start menu entry. The Intel footer should show `1.1.0-dev.231`. If Vulkan initialization fails, report the exact Intel adapter, driver version and error; physical Intel validation is still pending.

**Missing channel or DLL:** run the unified Setup again and check the system GPU driver and Visual C++ runtime. Advanced ZIP users must combine the correct channel archives. Do not download individual unofficial DLLs.

**Older NVIDIA / unsupported CUDA model:** use the available Anime4K models. Version 219 checks compatibility before preparing CUDA models. Video export still requires a driver supported by the bundled NVENC encoder; successful playback does not imply encoder support.

**Benchmark skipped or a model failed (NVIDIA/AMD):** Settings offers remeasurement. Cold model preparation may exceed the bounded test; incomplete candidates are excluded. A manual model selection remains available.

**Slow or black playback:** try Anime4K, reduce AI input height, and compare another file. Report the GPU/driver, model, settings and exact error. First-time preparation and a rendering error are different cases.

**CUGAN input-size error:** reduce AI input height and include the source dimensions in a report. AMD has an explicit 720p-area limit; NVIDIA model bounds vary by shape.

**MP4 cannot preserve audio (supported video-export channels):** try MKV output. Audio is not silently discarded. Intel has no video-file conversion tab.

## Support, privacy and licenses

[Report a problem](https://github.com/ETONOTE/LumiFrame-Windows/issues) with the app version, GPU/driver, channel, engine and reproduction steps. Remove personal paths, account information and secrets. Do not upload original videos or unreviewed logs.

Processing and benchmarking are local. No private video is used by the startup benchmark and no benchmark telemetry is uploaded. See [PRIVACY.md](PRIVACY.md). Android has a separate [privacy and support policy](https://lumiframe-privacy.etonote.chatgpt.site).

Third-party terms and notices are included with each channel. AMD model redistribution permission was confirmed by the project owner on October 18, 2026; model bytes are unchanged. Matching sources and build recipes for the unchanged LGPL libraries are in the [corresponding-source archive](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.230/LumiFrame-Windows-1.1.0-dev.230-corresponding-source.zip). Upstream projects do not endorse LumiFrame. Use media you own or are authorized to process and share.
