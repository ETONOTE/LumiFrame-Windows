# LumiFrame for Android

## Availability

As of **October 6, 2026**, version **1.0.0-beta1 (version code 5)** has been submitted to Google Play closed testing. The last verified submission status was under review. This is not a public Play Store launch or confirmation that testers can install it yet.

**A public APK download is not available in this repository yet.** The direct-download package must complete its public-distribution privacy checks first. No inactive tester URL or internal debug APK is presented as an installation link.

Newer local development builds are separate from the submitted beta. Do not assume that a feature shown in a development screenshot is included in beta1.

## Features in the test build

- Local video playback using Anime4K, E6, and a lightweight AnimeVideo-v3 path.
- Automatic/manual engine selection, pause/resume, timeline seeking, 10-second jumps, and landscape playback.
- Image-to-PNG and video-to-MP4 conversion, with cancellation and save/open controls.
- **Maximum output: 1920 x 1080.** Android 1440p output is not supported.

Playback uses mobile-oriented models and settings; it is not the complete six-engine Windows package. Model choices for file conversion can also differ from those used for live playback.

## Device requirements

- Android 10 or later and a 64-bit ARM device.
- Vulkan 1.1 or later with compatible hardware media decoding and GPU support.
- Image conversion currently requires Android 14 or later.

Testing has focused on a Samsung SM-F741N with Adreno 750. Support and speed on other devices are not guaranteed. A supported Android version alone does not prove that a device supports the required GPU/media path.

## Known limitations

- **V3 audio/video synchronization remains unresolved in the general release path.** Beta1 is not a fix for that issue.
- Exported AAC audio can have a startup timing offset on affected inputs.
- Separate earlier tests reached 30 FPS with specific mobile models and working resolutions. Those results do not guarantee every model, input, device, or long playback session in this package.
- Automatic switching, long-duration thermal behavior, and wider device compatibility still need further validation.

Use test media you have permission to process and keep your originals. This is an experimental test build, not a replacement for a reliable player when uninterrupted playback is essential.

## Installation channels

When an APK becomes available, use only the link published in this repository and verify its SHA-256. Android may require per-app permission to install a downloaded APK. Do not disable device-wide security protections or install files from unofficial mirrors.

Google Play and directly distributed APKs can use different signing certificates. One may not update the other in place; newer internal builds may also have a higher version code. **Do not uninstall an existing app without checking its saved data first.** Separate channel-specific installation instructions will be provided with the APK.

## Feedback and privacy

[Open an issue](https://github.com/ETONOTE/LumiFrame-Windows/issues) with your device model, Android version, app version, engine, input/output settings, and reproduction steps. Do not post device serial numbers, wireless-debugging addresses, personal media, or unreviewed logs.

Media is processed locally rather than uploaded to an upscaling server. See the [privacy and support policy](https://lumiframe-privacy.etonote.chatgpt.site).
