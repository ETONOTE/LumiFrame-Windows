# LumiFrame Windows 1.1.0-dev.231 — Intel joins the unified installer

Release 231 adds Intel to the unified Windows package while retaining the existing NVIDIA and AMD runtimes. [231 Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.231/LumiFrame-Windows-1.1.0-dev.231-Setup.exe) installs NVIDIA, AMD and Intel channels together. The [230 release](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.1.0-dev.230) remains available for rollback.

## Intel playback and photos

Earlier unified versions rejected Intel-only systems in the launcher before the application opened. Release 231 adds an independent Intel Vulkan runtime with **Anime4K Fast and Quality**. Intel starts with Fast, opens without a startup model benchmark, and supports playback controls, audio, original/upscaled comparison, frame capture and Anime4K photo conversion with original/result viewing.

Intel Auto stays within the selected Anime4K tier: Quality can fall back to Fast; Fast stays Fast. The Intel channel has separate preferences. If an older NVIDIA/AMD AI selection is read from a copied settings file, it is normalized to Fast while unrelated valid preferences are retained.

The Intel build does not include CUDA neural models or the AMD DirectML model. **Intel video-file conversion is unavailable:** the current GUI video encoder uses NVIDIA NVENC, so the Intel video-conversion tab is hidden and direct requests are rejected. Photo conversion remains available.

## Existing NVIDIA and AMD channels

| Component | Version included in 231 | Change |
|---|---|---|
| Unified launcher | 1.1.0-dev.231 package | Adds Intel routing and Intel channel updates |
| NVIDIA runtime and models | 1.1.0-dev.230 | Byte-for-byte retained |
| AMD runtime and model | 1.1.0-dev.218 | Byte-for-byte retained |
| Intel Vulkan runtime | 1.1.0-dev.231 | New Anime4K playback/photo channel |

The local protection check verified all **674 existing NVIDIA/AMD channel files** against the public channel manifests. No NVIDIA or AMD engine/model binary is replaced by the Intel compatibility build. The channel versions shown in the application footer therefore remain NVIDIA 230 and AMD 218; Intel shows 231.

Automatic GPU choice preserves the existing NVIDIA/AMD order, including dedicated-VRAM priority and the adapter-index tie break. Intel is used automatically only when no eligible NVIDIA/AMD adapter is present. `--backend intel`, `--backend nvidia` or `--backend amd` selects a present family explicitly. Adding an integrated Intel adapter does not take priority over a previously eligible NVIDIA/AMD adapter.

NVIDIA/AMD settings, manual selections, benchmark caches and their once-only initial measurement behavior are unchanged. E6, Hybrid, V3, CUGAN and the existing conversion features remain in their respective channels. The [230 conversion measurements and limits](RELEASE_NOTES_230.md) remain historical results for that unchanged NVIDIA runtime. **Release 231 makes no new playback-FPS, conversion-speed or quality-improvement claim.**

## One online installer

The unified Setup downloads five pinned archives and verifies each SHA256 before extraction: launcher, NVIDIA runtime/models, NVIDIA TensorRT libraries, AMD runtime/models, and Intel runtime. Users do not select a GPU package or combine ZIP files manually. Internet is required during installation; normal playback and photo processing run locally afterward.

Setup retains the folder-selection page, per-user installation, Start menu entry, optional desktop shortcut and uninstaller. System GPU drivers and the Microsoft Visual C++ x64 runtime remain prerequisites. Keep earlier installers or portable packages for rollback.

Each channel keeps its own version directory and current-version pointer. The local channel updater accepts Intel packages in addition to NVIDIA and AMD, verifies the manifest, and changes only the selected channel. NVIDIA still requires both its runtime/model and TensorRT archives for manual deployment.

## Validation status and limits

Completed local compatibility checks:

- NVIDIA, AMD and Intel GPU-selection policy variants; legacy NVIDIA/AMD adapter subsets and Intel insertion order; old/new launcher choice unchanged on the development host.
- Intel settings isolation, legacy AI-choice normalization, manual/Auto/prepared AI rejection, and exclusion of AI-only benchmark evidence. Existing preference and benchmark-policy regression tests passed.
- Local updater fixtures, package-manifest checks and preservation of all protected NVIDIA/AMD channel files.
- The Intel 231 build completed Fast, Quality and Auto playback checks through the shared Vulkan path on a **NVIDIA development GPU**: 120 frames in each run, with zero fallback frames. Two GUI playback cases and transport checks covered pause, seek, replay, end of stream and audio. Fast and Quality photo conversion passed.
- Seven selected CTest checks passed; the storage-admission check also passed when run in the normal Windows environment. Package privacy scanning passed for 243 files.

These are local build, behavior and package checks. They do not constitute installation/upgrade validation or verification of publicly downloaded assets.

**Physical Intel hardware has not been tested.** The shared-path smoke checks do not establish Intel driver compatibility, sustained playback behavior, power use or FPS. AMD physical hardware validation and a second NVIDIA GPU remain existing limitations. No new performance claim is made for those devices.

This remains an unsigned development build, not a Microsoft Store release. Android follows its separate test track and no Android APK is included. Media stays local; existing privacy and third-party license notices remain applicable.
