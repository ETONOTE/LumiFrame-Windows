# Windows beta status

**[Windows 0.1.0 Beta 1 is available](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v0.1.0-beta.1)** as an experimental portable release. Download both the application ZIP and required TensorRT runtime ZIP; extract them into the same parent folder. Remote SHA-256 digests were checked against the local validated archives before publication.

| Area | Status |
|---|---|
| Public distribution and issue tracker | Available |
| Player, image upscaling, and video conversion | Implemented in the development build |
| Mobile-inspired UI, Pretendard font, and LumiFrame icon | Applied |
| V3, Hybrid, CUGAN, and 6B Auto startup checks | Passed on the reference GPU |
| Current fine-tuned weights | Retained in the published beta |
| Personal-path removal from runtime libraries | Five FFmpeg DLLs rebuilt and checked; upstream libdovi CI paths classified |
| Third-party notices and corresponding source | Included as notices and a separate source asset |
| Other GPUs and clean Windows installations | Not yet validated |
| Downloadable beta | 0.1.0 Beta 1 published |
| Microsoft Store | Not submitted |

## Beta scope

This is a portable Windows x64 package split into two ordinary ZIPs to fit GitHub's per-asset limit. Both are required. Extract both before starting the application; do not copy only the executable. The executable retains the filename `AniEdge.exe` for compatibility, while the application is branded LumiFrame.

The initial AI hardware scope is NVIDIA CUDA/TensorRT with Vulkan. The reference system uses an RTX 4070 SUPER. No universal GPU compatibility or all-engine 30 FPS guarantee is made.

Additional training and Anime 6B reaching 30 FPS are not prerequisites for this first beta. Validated quality and performance improvements can follow in later releases.

## Publication safeguards

Only the reviewed application archive, required TensorRT runtime archive, corresponding-source archive and SHA-256 sums were uploaded. Training videos, user media, captures, private logs, caches, credentials, and private source history are excluded. Component notices are included; required library sources are a separate download.

The current executables retain a clean Release build with 27 passing host tests. After the FFmpeg rebuild, clean-path decoding/seeking and video/audio parity passed. Four peer engines passed Auto first-frame/shutdown and pixel parity checks. These bounded checks do not establish sustained performance on every video or GPU.
