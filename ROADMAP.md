# LumiFrame Windows roadmap

The immediate priority is a usable, clearly documented release. Dates and performance gains are not promised before validation.

## Release foundation

- Publish a privacy-reviewed Windows package with complete runtime setup instructions.
- Add trusted code signing after publisher identity and privacy requirements are settled.
- Preserve previous releases for rollback and gather reproducible compatibility reports.
- Prepare Microsoft Store packaging, account verification and certification. The app is **not yet available in Microsoft Store**.

## Next updates

1. **Reliability and compatibility:** startup failures, black playback, media import and export errors, cancellation and shutdown.
2. **Preparation time:** reduce first-use CUGAN/V3 preparation and improve progress feedback without displaying unprocessed frames as AI output.
3. **Conversion throughput:** reduce whole-video processing time while preserving frames, timestamps, audio and agreed image quality. A photo-only improvement is not a video-speed claim.
4. **Quality:** compare V3, CUGAN and 6B on diverse scenes, then evaluate tuning and training with appropriately licensed data.
5. **Broader hardware support:** validate the new AMD DirectML integration on AMD hardware, improve its transfer path, and investigate Intel support separately.

Anime 6B remains conversion-only. No all-model 30 FPS or automatic scene-to-best-model selection is promised. Changes should be supported by numerical checks and visible comparisons, not a benchmark number alone.
