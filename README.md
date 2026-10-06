# LumiFrame for Windows

LumiFrame is a GPU-accelerated video player and image/video upscaler for Windows. It brings local playback and file conversion into one desktop application.

This repository hosts Windows releases, user documentation, and issue reports. The application source and training media are not hosted here.

## Beta availability

**[Download LumiFrame Windows 0.1.0 Beta 1](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v0.1.0-beta.1)**. This is an unsigned experimental Windows x64 release. See [release status](RELEASE_STATUS.md) for its validation scope and limitations.

Download **both** runtime archives from the release:

1. `LumiFrame-Windows-0.1.0-beta.1-win-x64.zip` (about 1.17 GB).
2. `LumiFrame-Windows-0.1.0-beta.1-tensorrt-runtime.zip` (about 1.63 GB, required for AI engines).

Extract both into the **same writable parent folder**, merging the `LumiFrame-Windows` directories, then start `LumiFrame-Windows/AniEdge.exe`. Do not run inside the ZIP or copy only the executable. Check downloads against `SHA256SUMS.txt` and read the included `README.txt` and terms. The corresponding-source ZIP is for library source/build recipes; it is not another runtime part. GitHub's automatically generated source-code archive contains this documentation repository, not the application.

## Features

- Local video playback with GPU upscaling.
- Image upscaling and video file conversion.
- Anime4K Fast/Quality, E6 (EfRLFN family), AnimeVideo-v3, Hybrid, Real-CUGAN, and Anime 6B engine options.
- Manual selection or adaptive switching within a bounded engine chain.
- Playback controls, volume, timeline seeking, and frame capture.

The playback defaults are **AnimeVideo-v3, Auto, 1080p output, and 360p AI input height**. The app UI currently uses Korean labels.

V3, Hybrid, CUGAN, and 6B are peer choices. Auto considers the selected peer together with E6 and Anime4K; it does not automatically rotate between all four peer models. This grouping is a selection policy, not a claim of equal quality or speed.

## Hardware and startup

The current AI package uses NVIDIA CUDA/TensorRT and Vulkan on the same GPU. Runtime checks have been performed on an RTX 4070 SUPER. Other GPUs and clean Windows installations are not yet validated; AMD and Intel AI support is not claimed for this package.

First-time AI preparation can take several minutes while execution plans are built for your GPU and input shape. Plans are cached locally. Changing the engine, input shape, driver, or runtime may require rebuilding them.

Performance depends on the engine, video, resolution, GPU, and other workloads. **30 FPS is not guaranteed for every engine or device.** Earlier measurements from development-only acceleration paths do not describe the new portable beta path.

## Feedback

Use [Issues](https://github.com/ETONOTE/LumiFrame-Windows/issues) to report playback, conversion, or compatibility problems. Include the app version, Windows version, GPU and driver, engine, input/output resolution, and reproducible steps.

Do not upload original videos, private paths, account details, keys, or full unreviewed logs. Share only the minimum information and media you have permission to publish.

## Licenses

LumiFrame uses third-party libraries, models, and shaders. Full notices and applicable terms are included with the application. It dynamically links FFmpeg under LGPL version 2.1 or later, libplacebo and libiconv. Matching library sources, patches and build recipes are available in the `corresponding-source.zip` asset on the same release page. Upstream names identify their respective projects; they do not imply endorsement.

PC and Android releases have separate validation and performance results. This repository does not distribute the Android app.
