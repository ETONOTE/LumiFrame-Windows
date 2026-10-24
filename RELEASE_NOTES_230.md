# LumiFrame Windows 1.1.0-dev.230 — NVIDIA + AMD

[Download the unified Setup.exe](https://github.com/ETONOTE/LumiFrame-Windows/releases/download/v1.1.0-dev.230/LumiFrame-Windows-1.1.0-dev.230-Setup.exe). It installs **public NVIDIA 230 and unchanged AMD 218** together, verifies the downloaded archives, and selects the GPU channel at launch. Internet is needed during installation; normal playback and conversion run locally afterward.

## Actual video-file conversion

This public rebuild includes the V3/CUGAN file-conversion improvements through local 230. It preserves the selected model, weights, AI input size and FP32 CUGAN math. Playback and photo processing keep their existing paths.

The final CUGAN optimization is no longer bound to a development GPU identifier. Its five TensorRT partitions use SAME_COMPUTE_CAPABILITY compatibility, and its four cuDNN convolution plans are created on the target GPU. This additional route applies to **SM 8.9 NVIDIA GPUs at an actual 640 × 360 AI input**. Other architectures and shapes retain the compatible generic 226 conversion route. If a target GPU cannot create an approved cuDNN plan, conversion uses that generic route before submitting frames. Integrity failures in model/runtime files remain errors.

## Measurements

RTX 4070 SUPER, the same 298-frame source, warmed caches, three interleaved repetitions per version, and no competing training/game/conversion process. Conversion time is measured separately from whole-process time, which also includes startup and finalization. Separate comparisons have separate baseline samples; do not multiply their percentages. A negative reduction is slower in that comparison.

| Engine | Compared with | Conversion seconds, old → public 230 | Reduction | Full-process seconds, old → public 230 |
|---|---|---:|---:|---:|
| V3 | 226 | 1.763 → 1.766 | -0.17% | 3.340 → 3.276 |
| V3 | 229 | 1.770 → 1.765 | 0.28% | 3.248 → 3.242 |
| V3 | 230 | 1.771 → 1.777 | -0.38% | 3.271 → 3.311 |
| CUGAN | 226 | 8.893 → 7.727 | 13.11% | 10.433 → 9.519 |
| CUGAN | 229 | 7.861 → 7.736 | 1.59% | 9.509 → 9.464 |
| CUGAN | 230 | 7.726 → 7.730 | -0.06% | 9.386 → 9.462 |

These measurements describe this host and workload. They are not playback FPS, long-video guarantees, or measurements from other physical GPUs.

## Quality and regression checks

Six representative scenes, 20 frames each, passed the **unchanged** raw-image and encoder-quality limits against 225, 226, 229 and 230. Raw bounds are maximum 3/255, frame MAE 0.05/255 and edge MAE 0.10/255. Encoded mean/worst SSIM drops are at most 0.0001/0.0005 and mean/worst PSNR drops at most 0.05/0.30 dB, measured against the same pre-encoder 225 images. Small floating-point differences remain possible; the test does not prove every video will be identical.

| Compared with | Largest pixel difference /255 | Worst frame MAE /255 | Worst edge MAE /255 |
|---|---:|---:|---:|
| 225 | 2 | 0.015616 | 0.034838 |
| 226 | 2 | 0.017840 | 0.058714 |
| 229 | 2 | 0.017763 | 0.052635 |
| 230 | 2 | 0.017763 | 0.052635 |

The final shipping converter matches the accepted diagnostic output for CUGAN and the existing 230 output for V3. Short/odd frame counts, variable timestamps, 4:3 input, multiple audio tracks, cancellation, cache recovery, integrity rejection, reload, photos, playback and host regression checks passed. Simulated other-architecture and unsupported-plan cases matched generic 226 output. Fresh installation and 223 upgrade, Unicode paths, preserved settings and installed output were checked before promotion to Latest; the downloaded public Setup is checked separately before that promotion.

## AMD and compatibility

AMD 218 is byte-for-byte identical to the AMD channel in 223, including its DirectML model and runtime. Its footer correctly shows 1.1.0-dev.218. Launch the top-level LumiFrame or the installed shortcut; an old 1.0.0 NVIDIA-only executable can report a CUDA/cuInit error on AMD.

**Physical AMD hardware and a second NVIDIA GPU have not been tested on this host.** The portable architecture policy and fallback are tested locally; device-specific driver and performance validation remains a limitation. NVIDIA CUDA neural models retain their existing architecture/driver requirements; Pascal uses Anime4K. The final CUGAN speed improvement is conditional on the GPU and AI input shape described above.

This is an unsigned development build. Keep previous installers for rollback. Existing releases remain available, and normal settings, separate channel versions and the once-only startup benchmark behavior are preserved. The corresponding-source archive covers unchanged bundled open-source dependencies; it is not an application installation package.
