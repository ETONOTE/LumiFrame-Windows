# Windows beta status

The first Windows beta is in final packaging. No executable or model package has been published yet.

| Area | Status |
|---|---|
| Public distribution and issue tracker | Available |
| Player, image upscaling, and video conversion | Implemented in the development build |
| Mobile-inspired UI, Pretendard font, and LumiFrame icon | Applied |
| V3, Hybrid, CUGAN, and 6B Auto startup checks | Passed on the reference GPU |
| Current fine-tuned weights | Retained for the planned beta |
| Personal-path removal from runtime libraries | In progress |
| Third-party notices and corresponding source | Final packaging in progress |
| Other GPUs and clean Windows installations | Not yet validated |
| Downloadable beta | Not yet published |
| Microsoft Store | Not submitted |

## Beta scope

The planned release is a portable Windows x64 package. Extract the complete package before starting the application; do not copy only the executable. The executable currently retains the filename `AniEdge.exe` for compatibility, while the application is branded LumiFrame.

The initial AI hardware scope is NVIDIA CUDA/TensorRT with Vulkan. The reference system uses an RTX 4070 SUPER. No universal GPU compatibility or all-engine 30 FPS guarantee is made.

Additional training and Anime 6B reaching 30 FPS are not prerequisites for this first beta. Validated quality and performance improvements can follow in later releases.

## Publication safeguards

Only the reviewed release files will be uploaded. Training videos, user media, captures, private logs, caches, credentials, and private source history are excluded. Component notices and required source downloads will be published with the application.
