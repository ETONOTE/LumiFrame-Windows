# Release status

Last documented update: **October 15, 2026** (Windows update; Android remains a separate test track).

## Windows

[1.0.0](https://github.com/ETONOTE/LumiFrame-Windows/releases/tag/v1.0.0) is the Windows update, distributed as an unsigned x64 portable app. Download both the application ZIP and the required AI runtime ZIP. Keep the old version for rollback and extract the update into a new folder. Open `LumiFrame.exe`.

The release includes playback and image/video conversion. Playback offers Anime4K, E6, V3, Hybrid and CUGAN; **Anime 6B is conversion-only**. Auto uses the selected heavy playback engine with E6 and Anime4K, not unrestricted switching among all models.

Validation has focused on RTX 4070 SUPER. Other GPUs and clean Windows installations are not yet validated. All-model 30 FPS, Microsoft Store release, and automatic updates are not available.

Version 1.0.0 adds saved Korean/English switching beside Help and refines the footer layout. It retains the refreshed UI, expanded CUGAN shape handling and the bounded common photo/video conversion optimizations without changing model weights or encoder quality. The release notes describe the current build's tests. A clean build passed 34 host tests; the final footer revision passed 21 bounded runtime checks. Both language modes and the footer were checked in dark/light themes. Signing is deferred; Windows security warnings remain possible. Historical speed measurements are not broad hardware or sustained-stability certification. Reference-device native6B experiments are excluded from the public package.

Known limitations include GPU memory and model bounds on large/unusual inputs, potentially lengthy first-time plans and slow conversion with heavy engines. A previously observed V3 whole-file audio-drain timeout remains a compatibility follow-up; short passing tests do not certify every media file. Large long-video speedup is not complete.

## Android

The [Android notes](ANDROID.md) describe an earlier closed-test cycle. This Windows update does not establish current Play review status, tester eligibility or the feature set of a newer mobile build.

No APK is included with this Windows release. Mobile distribution and testing are managed separately.

See [Windows setup and features](README.md) and [Android test details](ANDROID.md).
