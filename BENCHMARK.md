# LumiFrame startup and first-run performance selection — 230

The NVIDIA and AMD applications now run a bounded synthetic benchmark on first use and choose a playback model from their own channel. The shared root launcher still selects the GPU family. Existing manually saved model settings are preserved; the benchmark recommendation is shown without replacing them. Settings → **성능 다시 측정하고 모델 자동 선택** explicitly measures and applies a new recommendation.

## Measurement and selection

- Fixed input: moving synthetic YUV420P SDR patterns at 640 × 360; output: 1920 × 1080. No user video, network request, or uploaded telemetry is involved.
- Each candidate runs in a separate `lumiframe_benchmark.exe` process on the launcher's selected GPU LUID. `GpuRenderer::prewarm()` exercises the actual playback engine policy, upload, color conversion, inference and final GPU composition. A dedicated headless startup flag avoids the swapchain while retaining playback model/backend choices. Export-only model policies are not used.
- Four warm-up frames are excluded. Each measured frame is timed through actual GPU completion (`drain_profile_prewarm`), not just asynchronous submission. Collect 32–120 completed samples, with at most five seconds of measurement per candidate. Decoder, audio and display refresh are outside this synthetic check; live Auto continues to respond to actual video load.
- The 30 fps target permits P95 ≤ 25 ms and P99 ≤ 30 ms, reserving time for the rest of playback. Prefer the highest existing product tier that meets both limits. At the same tier, prefer the lower P95. Tier ordering is an application policy, not an objective image quality measurement. If none meets the target, choose the fastest successfully measured model and tell the user to lower the AI input height if needed. If none completes, do not claim a measured recommendation; new users retain Anime4K Fast as their saved fallback.
- NVIDIA candidate pool: Anime4K Fast, Anime4K Quality, EfRLFN, Hybrid, AnimeVideo-v3, CUGAN. AMD candidates: Anime4K Fast, Anime4K Quality, AMD CUGAN Denoise ×2. Conversion-only Anime6B is excluded. Before launching a NVIDIA candidate, version 219 checks the selected adapter through the system CUDA driver matched by DXGI LUID. The CUDA 13 channel requires compute capability 7.5 or newer and CUDA 13 driver support; GTX 1060 / Pascal, absent CUDA, and unsupported drivers retain Anime4K Fast/Quality. CUGAN is excluded when dedicated VRAM is no greater than its existing 4 GiB reserve below 720p input or 8 GiB reserve at 720p and above. Runtime free-memory checks still apply. Unsupported or failed candidates cannot be recommended.
- Each child has a 45-second limit including model preparation; the suite has a 150-second wall-clock limit. Heavy first-time model preparation can therefore be excluded. The UI displays candidate progress and elapsed time, and allows skipping. A Windows kill-on-close job bounds child lifetime; cancellation terminates the child and leaves the main app usable.

## Persistence and user choices

The automatic benchmark runs once per Windows user. `%LOCALAPPDATA%/LumiFrame/benchmark-initial-run-v1.txt` records the initial attempt before GPU work begins. It is shared by NVIDIA and AMD and does not depend on the GPU, driver, model or app version. Later launches, updates, reinstalls and installation-folder changes preserve it. Cancellation, failure and interrupted attempts also leave later measurement manual.

Existing `benchmark-nvidia217.txt` or `benchmark-amd217.txt` reports migrate to this permanent marker without running again, including skipped or stale reports. Saved model preferences are retained. Version 219 uses a compatible session profile if a saved NVIDIA model cannot run on the detected GPU; this does not rewrite the saved preference. Manual measurement or an explicit Settings save can select a new model. Changed or deleted benchmark caches do not start a new automatic check. If all user settings are intentionally removed, the app is new again and the initial check can run once.

Settings → **성능 다시 측정하고 모델 자동 선택** always permits manual remeasurement. Reports remain channel-specific, with a fingerprint identifying the measurement's hardware/software context. A fingerprint change does not schedule another benchmark. Atomic report replacement and a shared per-settings mutex protect results and prevent duplicate initial work in concurrent launches. Cancelling manual remeasurement leaves the saved model choice unchanged.

Preferences format 5 adds `model_user_selected`. Valid formats 1–4 migrate as user choices; benchmark-applied defaults remain automatic. Explicit Settings saves are user choices. Automatic application uses the measured 360p input / 1080p output / Auto settings, while preserving volume, appearance, language and other preferences. Manual remeasurement applies its successful recommendation. Merely skipping or failing does not overwrite a saved user choice.

## Validation and limits

Policy tests cover quality tiers, tail-latency budgets, same-tier choice, AMD/NVIDIA separation, failed/slow/insufficient/non-finite results, cache corruption, fingerprint changes and skip persistence. Preferences tests cover legacy migration and automatic/manual provenance. The process test measures real child cancellation and suppression of later automatic runs. New lifecycle tests cover initial failure, changed/deleted caches, explicit manual retry, migration from either channel, interrupted writes and concurrent launches in both builds. Validation used an RTX 4070 SUPER host.

The version 217 host regression runs passed 32 NVIDIA and 27 AMD tests (runtime staging, photo storage/preview admission and the unrelated NTFS binding test were excluded). The isolated cancellation test completed within 171 ms. Real NVIDIA V3 playback presented 12 synthetic-video frames with no drops, fallback, CUDA errors or normal readbacks; initial model setup is included in that playback log and is not a throughput benchmark.

The version 217 GUI verified legacy-choice preservation, live candidate progress, explicit remeasurement and Preferences 5 persistence. In the remeasurement all six NVIDIA candidates completed; Hybrid had P95 9.14 ms versus V3 11.22 ms and CUGAN 33.82 ms, so the shared tier/budget policy selected Hybrid and saved Auto / 360 / 1080. These values describe that short run on this host only. The initial cold run had timed out preparing Hybrid, illustrating why incomplete candidates are recorded rather than assigned invented scores.

Those measurements describe version 217. In 218, later launches record `STARTUP_BENCHMARK automatic_skipped=1 manual_remeasurement_only=1`, restore saved preferences and do not check hardware fingerprints or open the measurement dialog. Driver/model/application changes require manual remeasurement in Settings.

Version 218 passed five targeted tests in each GPU build (ten total). A fresh real NVIDIA run saved AnimeVideo-v3; restarting after changing the test runtime inventory left both preferences and the report byte-for-byte unchanged and logged automatic suppression. Explicit real-child cancellation completed in about 181 ms, and subsequent automatic execution remained suppressed.

The available host is an NVIDIA RTX 4070 SUPER. AMD compilation and shared selection/persistence logic can be checked here; AMD driver compatibility and the resulting AMD model choice still require an AMD PC. A short synthetic check is a startup recommendation, not a guarantee for every resolution, frame rate, video or background GPU workload.

Version 219 passed seven NVIDIA tests and four shared-code AMD regression tests. Real packaged Fast/Quality runs completed 120 frames each, V3 completed 51 frames, and a synthetic 640 × 360 photo produced a 1920 × 1080 PNG on RTX 4070 SUPER. Pascal/Turing/Ada, old-driver, missing-CUDA, low-VRAM and saved-choice cases are policy fixtures; GTX 1060 physical testing is not claimed. The shipped AMD 218 channel is byte-for-byte unchanged.

## Version 223: AI engine preparation at more input sizes

The once-only model-selection benchmark above is unchanged. Version 223 separately reduces V3/CUGAN engine preparation using verified hardware-compatible prepared engines. Coverage is keyed to actual input width × height; see [all shapes and GPU conditions](RELEASE_NOTES_223.md#exact-input-shapes-and-gpu-coverage). Existing valid native caches take priority. Unsupported or damaged bundles fall back to the original build path.

On RTX 4070 SUPER, an empty engine cache through the first presented frame at 1280 × 720 measured V3 **54.21 → 1.91 seconds** and CUGAN **173.16 → 2.26 seconds**. At 1920 × 1080, V3 measured **80.97 → 2.27 seconds** and CUGAN **331.09 → 2.69 seconds**. These are first-frame timings, not steady-state frame rates or guarantees for other PCs.

42 model/input combinations compared the same three consecutive source frames and 240 playback frames per version in alternating runs. Seven representative cases were rerun after the final long-path correction. Maximum pixel error was 2/255, and worst frame mean absolute error was 0.05263/255 (limits 3/255 and 0.15/255). Playback passed mean GPU time ≤105%, P95 GPU time ≤110%, and FPS ≥95% of baseline. The worst observed FPS ratio was 97.87% and largest mean GPU-time ratio was 104.88%. Models, precision and input settings were preserved; small floating-point differences remain possible.

Six audio/video sync runs and 12 fallback/cache checks passed. CUGAN 2560×1440 and 3840×2160 prepared engines were excluded because the original baseline could not complete on the 12 GB host. Other physical GPUs remain unmeasured, and these short runs do not certify every video. The AMD 218 channel and its initial benchmark remain unchanged.

## Version 230: actual video-file conversion

The once-only playback model-selection benchmark above is unchanged. Public 230 separately improves file conversion; its last CUGAN route is portable across eligible SM 8.9 devices and builds cuDNN plans on the target GPU. Other architectures/shapes keep the generic route.

| Engine | Compared with | Conversion seconds, old → public 230 | Reduction | Full-process seconds, old → public 230 |
|---|---|---:|---:|---:|
| V3 | 226 | 1.763 → 1.766 | -0.17% | 3.340 → 3.276 |
| V3 | 229 | 1.770 → 1.765 | 0.28% | 3.248 → 3.242 |
| V3 | 230 | 1.771 → 1.777 | -0.38% | 3.271 → 3.311 |
| CUGAN | 226 | 8.893 → 7.727 | 13.11% | 10.433 → 9.519 |
| CUGAN | 229 | 7.861 → 7.736 | 1.59% | 9.509 → 9.464 |
| CUGAN | 230 | 7.726 → 7.730 | -0.06% | 9.386 → 9.462 |

Three interleaved repeats per version used a 298-frame source on RTX 4070 SUPER, with caches warm and no competing GPU job. Whole-process time includes preparation and finalization. These are actual file-conversion timings, not playback FPS. See [quality, hardware coverage and installation validation](RELEASE_NOTES_230.md). AMD 218 bytes are unchanged, and other physical GPUs were not benchmarked.
