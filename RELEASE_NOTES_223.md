# LumiFrame Windows 1.1.0-dev.223

**Latest unified Windows download — NVIDIA + AMD: [Download the single Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.223/LumiFrame-Windows-1.1.0-dev.223-Setup.exe).** Install it and launch LumiFrame from the new Start menu entry. AMD users should use this installer; the older 1.0.0 release is NVIDIA-only.

This is the existing unsigned development build, now listed as GitHub's Latest download. The installer, models and runtime files are unchanged. AMD physical hardware validation remains pending. The included AMD channel displays `1.1.0-dev.218` in the app footer; `1.0.0` identifies an older executable.

Version 223 reduces first-time NVIDIA AnimeVideo-v3 and CUGAN preparation at more AI input sizes, while retaining the earlier 640 × 360 improvement. It ships the same application, model and engine files as the validated local 223 installer. The models, computation precision, input-resolution settings and playback path are preserved; image and playback comparisons passed the criteria below.

## Download and installation

Download **[LumiFrame-Windows-1.1.0-dev.223-Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.223/LumiFrame-Windows-1.1.0-dev.223-Setup.exe)**. This small installer downloads both GPU channels automatically and verifies their SHA-256 hashes. Choose a folder in Setup; internet is required during installation. Normal playback and benchmarking remain offline. Allow about 4.1 GB installed plus download/extraction space.

The package contains **NVIDIA 223 and unchanged AMD 218**. Existing preferences and the once-only initial performance check are preserved. Close LumiFrame before updating an existing installation. [Installer checksum](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.223/SHA256SUMS-Setup.txt).

Optional manual deployment uses the launcher, AMD, NVIDIA and NVIDIA TensorRT ZIPs from this release. NVIDIA needs both NVIDIA ZIPs; extract packages into the same destination so their `LumiFrame-Windows` folders merge. They are not required when using Setup. [ZIP checksums](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.223/SHA256SUMS.txt).

## Faster first preparation

Compatible prepared TensorRT engines avoid rebuilding the same model for the selected input shape. Existing valid GPU-specific caches remain preferred. The app checks model/runtime identity and hardware compatibility before restoring a prepared engine. Missing, corrupt or incompatible bundles return to the original preparation path.

Times below measure **an empty AI engine cache through the first presented video frame**, on RTX 4070 SUPER. They do not measure installer time or subsequent steady-state FPS.

| Model | Actual AI input | Original preparation | Prepared engines |
|---|---|---:|---:|
| V3 | 853 × 480 | 18.32 s | 1.82 s |
| V3 | 1280 × 720 | 54.21 s | 1.91 s |
| V3 | 1920 × 1080 | 80.97 s | 2.27 s |
| CUGAN | 640 × 480 | 75.51 s | 2.03 s |
| CUGAN | 853 × 480 | 93.09 s | 1.94 s |
| CUGAN | 1280 × 720 | 173.16 s | 2.26 s |
| CUGAN | 1920 × 1080 | 331.09 s | 2.69 s |

## Exact input shapes and GPU coverage

Coverage depends on the **actual width × height**, calculated from AI input height and source aspect ratio. A chosen height above the source height remains capped to the source, as before. An unlisted aspect ratio/shape uses normal preparation.

| Engine group | Eligible hardware | Included actual input shapes |
|---|---|---|
| Retained 640 × 360, V3 and CUGAN | NVIDIA Ampere or newer, compatible driver/runtime | 640×360 |
| Additional V3, Ampere-compatible | NVIDIA Ampere or newer, compatible driver/runtime | 256×144, 320×180, 320×240, 426×240, 427×240, 480×270, 569×320, 640×480, 720×540, 960×540, 768×576, 1024×576, 960×720, 1280×720 |
| Additional V3, matching compute capability | NVIDIA SM 8.9, compatible driver/runtime | 480×360, 853×480, 854×480, 1600×900, 1920×1080, 2560×1440, 3840×2160 |
| Additional CUGAN, matching compute capability | NVIDIA SM 8.9, compatible driver/runtime | 256×144, 320×180, 320×240, 426×240, 427×240, 480×270, 569×320, 480×360, 640×480, 853×480, 854×480, 720×540, 960×540, 768×576, 1024×576, 960×720, 1280×720, 1600×900, 1920×1080 |

GeForce RTX 30 series is an Ampere example; GeForce RTX 40 series uses SM 8.9. Check [NVIDIA's compute capability table](https://developer.nvidia.com/cuda/gpus) for other models. Hardware-compatible plans are distributed, not the development PC's ordinary device-bound cache. Runtime and driver checks still apply, including CUDA 13 driver support. Sufficient GPU memory remains required.

CUGAN 2560×1440 and 3840×2160 prepared engines are **not included**: the original preparation baseline did not complete on the 12 GB validation host. Their previous behavior remains. This update does not extend AMD preparation coverage or port CUDA models to older unsupported GPUs.

## Validation and limits

- Real application comparisons passed for 42 model/input combinations. Each compared the same three consecutive source frames and 240 playback frames per version, using alternating old/new runs.
- Quality limits were maximum pixel difference 3/255 and mean absolute difference 0.15/255. Observed maximum was 2/255, with worst frame mean difference 0.05263/255. Small floating-point differences are possible; this is not a bit-identical-output claim.
- Playback limits were mean GPU time ≤105%, P95 GPU time ≤110%, and playback FPS ≥95% of the baseline. Across the full checks and seven final representative reruns, the worst measured FPS ratio was 97.87% and largest mean GPU-time ratio was 104.88%. No playback drops or engine errors occurred in those comparisons.
- Six separate audio/video synchronization runs passed. Missing/corrupt bundle fallback and existing valid-cache preference passed 12 checks. These short checks do not certify every video or resolve every historical long-video issue.
- Windows long installation paths were corrected and seven representative GPU cases rerun. The local offline installer passed fresh installation and an update from 222, full payload hashes and 14 installed-GUI comparisons. Installed output matched the validated 223 candidate exactly.
- Measurements used RTX 4070 SUPER. Other physical GPUs have not been benchmarked for this release. Compatibility metadata enables use on eligible other PCs but does not guarantee identical preparation time or performance there.

The unified installer and earlier NVIDIA compatibility policy remain. Older GPUs use eligible Anime4K models; saved unsupported selections use a compatible session profile without rewriting the saved choice. AMD 218 is byte-for-byte unchanged; **AMD and GTX 1060 physical hardware validation remain pending**. This is an unsigned preview. The previous stable 1.0.0 and earlier previews remain available.
