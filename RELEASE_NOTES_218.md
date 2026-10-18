# LumiFrame Windows 1.1.0-dev.218

Choose where to install LumiFrame, and run the automatic performance check only once.

**[Download the single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.218/LumiFrame-Windows-1.1.0-dev.218-Setup.exe)**

## Changes

- Setup always shows the installation folder page, including when reinstalling or upgrading. The previous folder is suggested and can be changed.
- The first application launch automatically measures the detected GPU's models once. Later launches, application/model updates and GPU/driver changes do not start another automatic benchmark.
- Use **Settings → 성능 다시 측정하고 모델 자동 선택** for any later measurement. Cancelling or failing the initial check also leaves subsequent measurements manual.
- Existing 217 measurement records migrate without another automatic check. Saved manual model choices are kept. If an initial check cannot measure any model, a new user's Anime4K Fast fallback is saved.
- Both NVIDIA and AMD use the same once-only rule. The shared launcher still detects the GPU at every launch and starts the matching runtime. Their runtime/model updates remain independent.

## Install

Run Setup, select the destination folder, and open LumiFrame from the Start menu. This one installer downloads and verifies both NVIDIA and AMD runtimes/models. No GPU-specific selection or manual ZIP merging is needed. Internet is required during installation (about 2.9 GB download / 3.8 GB installed, plus temporary space). Normal use and measurement are offline.

The default location is `%LOCALAPPDATA%\Programs\LumiFrame`; app files are inside its `LumiFrame-Windows` subfolder. Installation is per-user, with an uninstaller and optional desktop shortcut. Measurement state remains in the user's LumiFrame settings folder across updates, reinstalls and location changes. System GPU drivers and the Microsoft Visual C++ x64 runtime remain prerequisites.

GPU-specific ZIPs are for advanced manual deployment and independent channel updates. NVIDIA manual deployment needs both NVIDIA ZIPs. Corresponding-source and GitHub source ZIPs are not installation packages. [SHA256SUMS.txt](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.218/SHA256SUMS.txt) and [installer checksum](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.218/SHA256SUMS-Setup.txt) are provided.

## Validation and limits

NVIDIA and AMD builds passed lifecycle, selection policy, preferences, UI assets and workflow tests. Lifecycle checks cover initial failure, changed/deleted caches, manual retry, migration from either GPU channel, interrupted attempts and concurrent launches. The measured model-ranking policy is unchanged from 217.

**AMD physical hardware validation remains pending.** This unsigned preview is tested on an NVIDIA host. AMD requires DirectX 12 and accepts even model input dimensions within a 720p area. Intel-only systems are not supported by the launcher. Existing long-video/model-preparation limits remain.

Model weights and third-party library bytes are unchanged from 217. AMD redistribution was authorized by the project owner on October 18, 2026. Required notices and matching LGPL corresponding sources are included. No personal media, logs, preferences or cache files are distributed.
