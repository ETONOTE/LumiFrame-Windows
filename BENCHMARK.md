# LumiFrame first-run performance selection — 217

The NVIDIA and AMD applications now run a bounded synthetic benchmark on first use and choose a playback model from their own channel. The shared root launcher still selects the GPU family. Existing manually saved model settings are preserved; the benchmark recommendation is shown without replacing them. Settings → **성능 다시 측정하고 모델 자동 선택** explicitly measures and applies a new recommendation.

## Measurement and selection

- Fixed input: moving synthetic YUV420P SDR patterns at 640 × 360; output: 1920 × 1080. No user video, network request, or uploaded telemetry is involved.
- Each candidate runs in a separate `lumiframe_benchmark.exe` process on the launcher's selected GPU LUID. `GpuRenderer::prewarm()` exercises the actual playback engine policy, upload, color conversion, inference and final GPU composition. A dedicated headless startup flag avoids the swapchain while retaining playback model/backend choices. Export-only model policies are not used.
- Four warm-up frames are excluded. Each measured frame is timed through actual GPU completion (`drain_profile_prewarm`), not just asynchronous submission. Collect 32–120 completed samples, with at most five seconds of measurement per candidate. Decoder, audio and display refresh are outside this synthetic check; live Auto continues to respond to actual video load.
- The 30 fps target permits P95 ≤ 25 ms and P99 ≤ 30 ms, reserving time for the rest of playback. Prefer the highest existing product tier that meets both limits. At the same tier, prefer the lower P95. Tier ordering is an application policy, not an objective image quality measurement. If none meets the target, choose the fastest successfully measured model and tell the user to lower the AI input height if needed. If none completes, do not claim a measured recommendation; new users get Anime4K Fast in the current session.
- NVIDIA candidates: Anime4K Fast, Anime4K Quality, EfRLFN, Hybrid, AnimeVideo-v3, CUGAN. AMD candidates: Anime4K Fast, Anime4K Quality, AMD CUGAN Denoise ×2. Conversion-only Anime6B is excluded. Unsupported or failed candidates cannot be recommended.
- Each child has a 45-second limit including model preparation; the suite has a 150-second wall-clock limit. Heavy first-time model preparation can therefore be excluded. The UI displays candidate progress and elapsed time, and allows skipping. A Windows kill-on-close job bounds child lifetime; cancellation terminates the child and leaves the main app usable.

## Persistence and user choices

`%LOCALAPPDATA%/LumiFrame/benchmark-nvidia217.txt` and `benchmark-amd217.txt` are independent. A SHA256 fingerprint includes the GPU vendor/device/subsystem/revision, dedicated memory, driver version, CPU thread count, RAM, benchmark parameters, channel inventory, and model/shader/runtime file stamps. LUID is used for execution but is not persisted as a cache key because it may change after reboot. Channel or model updates invalidate only that channel's result.

Cache parsing is bounded and checks channel, fingerprint, sample validity and duplicate entries. Atomic replacement protects the last stored report. A first-run skip is remembered rather than prompting every launch. Cancelling an explicit remeasurement preserves a previous successful report. A named mutex prevents duplicate measurement for the same GPU/build in multiple app instances. Cache hits skip GPU inference.

Preferences format 5 adds `model_user_selected`. Valid formats 1–4 migrate as user choices; benchmark-applied defaults remain automatic. Explicit Settings saves are user choices. Automatic application uses the measured 360p input / 1080p output / Auto settings, while preserving volume, appearance, language and other preferences. Manual remeasurement applies its successful recommendation. Merely skipping or failing does not overwrite a saved user choice.

## Validation and limits

Policy tests cover quality tiers, tail-latency budgets, same-tier choice, AMD/NVIDIA separation, failed/slow/insufficient/non-finite results, cache corruption, fingerprint changes and skip persistence. Preferences tests cover legacy migration and automatic/manual provenance. The process test measures real child cancellation and reuse of a saved skip marker. Validation used an RTX 4070 SUPER host.

The final host regression runs passed 32 NVIDIA and 27 AMD tests (runtime staging, photo storage/preview admission and the unrelated NTFS binding test were excluded). The isolated cancellation test completed within 171 ms. Real NVIDIA V3 playback presented 12 synthetic-video frames with no drops, fallback, CUDA errors or normal readbacks; initial model setup is included in that playback log and is not a throughput benchmark.

The actual GUI verified legacy-choice preservation, live candidate progress, explicit remeasurement and Preferences 5 persistence. In the remeasurement all six NVIDIA candidates completed; Hybrid had P95 9.14 ms versus V3 11.22 ms and CUGAN 33.82 ms, so the shared tier/budget policy selected Hybrid and saved Auto / 360 / 1080. These values describe that short run on this host only. The initial cold run had timed out preparing Hybrid, illustrating why incomplete candidates are recorded rather than assigned invented scores.

The final application change invalidated the previous fingerprint and remeasured successfully. The next launch recorded `STARTUP_BENCHMARK cache=1 cancelled=0 force=0` and restored Hybrid without new GPU measurement. Cache checking no longer flashes the measurement dialog on ordinary launches. Final executable hashes match the builds and both channel inventories were verified.

The available host is an NVIDIA RTX 4070 SUPER. AMD compilation and shared selection/persistence logic can be checked here; AMD driver compatibility and the resulting AMD model choice still require an AMD PC. A short synthetic check is a startup recommendation, not a guarantee for every resolution, frame rate, video or background GPU workload.
