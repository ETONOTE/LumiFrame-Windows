# AMD channel update feed

`amd.json` identifies the AMD channel approved by the LumiFrame release owner. It is separate from the latest unified installer release. It does not grant contributors permission to publish a channel or provide access to the private application source.

The initial feed points to the existing, unchanged AMD218 asset distributed with230. It does not announce a new AMD optimization. Existing230 installers do not yet contain the new in-app updater UI; only builds that include that feature consume this feed. Latest installer links remain unchanged.

The updater accepts HTTPS assets from `ETONOTE/LumiFrame-Windows` release URLs, verifies the ZIP size/SHA256 and the full AMD channel manifest, then switches only the AMD version pointer. Previous versions remain available for rollback. Reading this feed is not permission to bypass model, licensing or hardware acceptance checks.

Before a future feed change, the owner must verify the exact published asset, AMD-only package contents, compatibility with the current shared application, image quality, actual conversion/frame/PTS/audio behavior, AMD hardware results and rollback. Deliveries made against an older development baseline must be rebased onto the current approved AMD application before publication, preserving the update UI. Monotonically increase `sequence`; keep immutable release assets and versions.

The GitHub account that owns this repository controls official feed updates. Access to a separate AMD development repository does not grant write access here. No workflow automatically promotes collaborator submissions.
