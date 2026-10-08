# Release status

Last documented update: **October 8, 2026** (Windows update; Android section unchanged).

## Windows

[0.1.0 Beta 2](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v0.1.0-beta.2) is the Windows update, distributed as an unsigned experimental x64 portable app. Download both the application ZIP and the required AI runtime ZIP. Keep Beta 1 for rollback and extract the update into a new folder.

The release includes playback, image/video conversion, and Anime4K, E6, V3, Hybrid, CUGAN, and Anime 6B. Auto uses the selected peer engine with E6 and Anime4K, not unrestricted switching among all models.

Validation has focused on RTX 4070 SUPER. Other GPUs and clean Windows installations are not yet validated. All-model 30 FPS, Microsoft Store release, and automatic updates are not available.

Beta 2 reduces cold V3 preparation and photo/video conversion overhead without changing model weights, default processing resolution, or video encoder quality. It includes 29 passing host tests, bounded playback/export regression checks, nonblank V3 comparisons, and a full 32-second MKV export retaining 960 frames and 1,500 audio packets. Exact checks and timing examples are in the release notes; they are not broad hardware or sustained-stability certification.

Known limitations include input-shape restrictions for CUGAN/6B, potentially lengthy first-time plans, and a previously observed V3 whole-file audio-drain timeout still requiring investigation.

## Android

**1.0.0-beta1 / code 5** was submitted to Google Play closed testing. The last verified status was under review, not public availability. Newer local debug builds are not the Play submission.

Direct APK download is pending public-distribution privacy clearance. No APK is currently published in this repository. V3 A/V synchronization and exported AAC startup timing remain known issues.

See [Windows setup and features](README.md) and [Android test details](ANDROID.md).
