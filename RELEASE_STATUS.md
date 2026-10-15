# Release status

Last documented update: **October 15, 2026** (Windows update; Android remains a separate test track).

## Windows

[0.1.0 Beta 3](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v0.1.0-beta.3) is the Windows update, distributed as an unsigned experimental x64 portable app. Download both the application ZIP and the required AI runtime ZIP. Keep the old version for rollback and extract the update into a new folder. Open `LumiFrame.exe`.

The release includes playback and image/video conversion. Playback offers Anime4K, E6, V3, Hybrid and CUGAN; **Anime 6B is conversion-only**. Auto uses the selected heavy playback engine with E6 and Anime4K, not unrestricted switching among all models.

Validation has focused on RTX 4070 SUPER. Other GPUs and clean Windows installations are not yet validated. All-model 30 FPS, Microsoft Store release, and automatic updates are not available.

Beta 3 refreshes the UI, expands CUGAN shape handling and incorporates bounded common photo/video conversion optimizations without changing model weights or encoder quality. The release notes describe the current build's tests. Historical speed measurements are not broad hardware or sustained-stability certification. Reference-device native6B experiments are excluded from the public package.

Known limitations include GPU memory and model bounds on large/unusual inputs, potentially lengthy first-time plans and slow conversion with heavy engines. A previously observed V3 whole-file audio-drain timeout remains a compatibility follow-up; short passing tests do not certify every media file. Large long-video speedup is not complete.

## Android

The [Android notes](ANDROID.md) describe an earlier closed-test cycle. This Windows update does not establish current Play review status, tester eligibility or the feature set of a newer mobile build.

No APK is included with this Windows release. Mobile distribution and testing are managed separately.

See [Windows setup and features](README.md) and [Android test details](ANDROID.md).
