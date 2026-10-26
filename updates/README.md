# AMD channel updates

AMD channel development and publication are managed separately in [LumiFrame-AMD-Releases](https://github.com/ETONOTE/LumiFrame-AMD-Releases). The in-app AMD updater reads [that repository's current feed](https://github.com/ETONOTE/LumiFrame-AMD-Releases/blob/main/updates/amd.json).

The `amd.json` file in this directory is a legacy record of the AMD218 asset included with unified230. The new updater does not use this legacy feed. The unified installer and NVIDIA release assets remain managed in this repository.

The AMD developer builds and validates the AMD channel and publishes it directly in the separate AMD release repository. Per-release approval or manual integration by the application owner is not required. AMD repository access does not grant write access to the unified application or NVIDIA repositories.

Existing230 installations need the [AMD update feature package](https://github.com/ETONOTE/LumiFrame-AMD-Releases/releases/tag/amd-update-support-v1) once before the in-app update button is available. This first feature package is a prerelease awaiting physical AMD acceptance; it has not replaced the stable unified installer or activated a new production AMD feed.

After that initial setup, users running the AMD channel can check, download, apply and roll back AMD updates from Settings. The updater verifies the AMD package and changes only the AMD channel version, preserving NVIDIA, the root launcher and previous AMD versions. Physical AMD quality, playback, conversion, frame/PTS/audio and rollback checks remain the AMD developer's responsibility before each engine release.

For each new unified installer release, the application owner checks the current production AMD release, its hardware validation evidence and shared-app compatibility, then includes a selected AMD version with pinned download URLs and SHA256 values. The next unified package must also include the AMD update feature. Independent AMD publication does not rebuild existing unified installers, and Setup does not select a different AMD version dynamically at installation time. Existing in-app AMD updates continue independently of the unified installer release schedule.
