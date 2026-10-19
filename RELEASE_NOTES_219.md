# LumiFrame Windows 1.1.0-dev.219

Older NVIDIA GPUs now start with compatible models. One installer installs both GPU channels: **NVIDIA 219 + unchanged AMD 218**.

**[Download the single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.219/LumiFrame-Windows-1.1.0-dev.219-Setup.exe)**

## Changes

- GTX 1060 / Pascal uses Anime4K Fast and Quality. The benchmark compares only compatible candidates and chooses a starting model using the existing performance policy.
- The selected NVIDIA adapter's compute capability and installed CUDA driver support are checked before offering CUDA models. The bundled CUDA 13 neural runtime requires compute capability 7.5 or newer and CUDA 13 driver support. Missing or incompatible CUDA retains the Vulkan Anime4K profiles.
- NVIDIA CUGAN is excluded from starting candidates if total VRAM cannot satisfy the existing free-memory reserve. The runtime memory check remains in place.
- Playback and conversion filter incompatible models. An incompatible saved model uses a compatible session profile while retaining the saved preference; Settings can explicitly save a new choice.
- Explicit command-line AI requests are checked before model preparation. GPU selection follows the same adapter as the compatibility probe.
- AMD inference, models and runtime files are unchanged from the published 218 channel. NVIDIA and AMD retain independent update versions.

## Install

Run Setup, select the destination folder, and open LumiFrame from the Start menu. **Only this one installer is needed.** It downloads and SHA256-verifies both GPU channels automatically. No GPU-specific download selection or manual ZIP merging is needed.

Installation requires internet (about 2.9 GB download / 3.8 GB installed, plus temporary space). The folder page remains visible when upgrading or reinstalling. The default is `%LOCALAPPDATA%\Programs\LumiFrame`, with app files in its `LumiFrame-Windows` subfolder. Installation is per-user, with an uninstaller and optional desktop shortcut. GPU drivers and the Microsoft Visual C++ x64 runtime remain prerequisites.

GPU detection occurs on every launch. Automatic performance measurement still runs **once per Windows user**, shared across NVIDIA and AMD. Updates, reinstalls, driver/GPU changes, cancellation or initial failure do not trigger another automatic attempt. Later measurements are manual through **Settings → 성능 다시 측정하고 모델 자동 선택**. Normal use and measurement are offline.

Separate GPU ZIPs are advanced manual-update packages; an AMD archive carrying the 219 release name contains the unchanged AMD 218 channel. Manual NVIDIA deployment requires both NVIDIA ZIPs. Corresponding-source and GitHub source ZIPs are not installation packages. [ZIP checksums](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.219/SHA256SUMS.txt) and [installer checksum](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.219/SHA256SUMS-Setup.txt) are provided.

## Validation and limits

Seven targeted NVIDIA tests and four AMD shared-code regression tests passed. Compatibility fixtures cover Pascal, Turing, Ada, old drivers, absent CUDA, low VRAM and unsupported saved models. Real packaged Fast, Quality and V3 GPU workloads and a 360p-to-1080p photo conversion passed on RTX 4070 SUPER. Every shipped AMD file matches the published 218 inventory.

**GTX 1060 and AMD physical hardware validation are not claimed.** This is an unsigned preview. The compatibility update does not port the CUDA neural models to Pascal, and short synthetic measurements do not guarantee a particular frame rate. Video export is unchanged: the bundled NVENC path still requires a supported driver meeting its 570-or-newer requirement. Existing AMD DirectX 12/input-shape constraints and long-video limitations remain.

Required third-party notices and matching LGPL corresponding sources are included. Model weights and third-party library bytes are unchanged. No personal media, logs, preferences or cache files are distributed; release and installer privacy scans have no unresolved findings.
