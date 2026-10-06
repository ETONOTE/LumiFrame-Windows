# LumiFrame for Windows

LumiFrame is a GPU-accelerated video player and image/video upscaler for Windows. It brings local playback and file conversion into one desktop application.

This repository hosts Windows releases, user documentation, and issue reports. The application source and training media are not hosted here.

## Beta availability

The first downloadable beta is being prepared. **There is no public application download yet.** See [release status](RELEASE_STATUS.md) for the current scope. Verified packages will appear on the [Releases page](https://github.com/ETONOTE/LumiFrame-Windows/releases).

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

LumiFrame uses third-party libraries, models, and shaders. Their notices, applicable terms, and required corresponding source will accompany the binary release. Upstream names identify their respective projects; they do not imply endorsement.

PC and Android releases have separate validation and performance results. This repository does not distribute the Android app.
