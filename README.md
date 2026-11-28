# ESP32-AI-Control — Windows 10 Mobile updates

This branch is the update channel for the Windows 10 Mobile (ARM) application.

## Files

- `version.json` — update manifest consumed by the Lumia application.
- `app.appxbundle` — signed ARM application bundle. It is published only when a tested release is ready.

## Publishing a release

1. Build the **Release / ARM** AppX bundle from the `feature/windows10-mobile-ota` branch.
2. Keep the package identity, publisher, PhoneProductId and signing certificate unchanged.
3. Set the package version in `Package.appxmanifest` to a value greater than the currently installed version.
4. Upload the resulting bundle to this branch as `app.appxbundle`.
5. Calculate SHA-256 for the exact uploaded file and put the 64-character hexadecimal value in `version.json`.
6. Set `version` to exactly the package identity version, add release notes, and set `enabled` to `true` only after verifying the uploaded artifact and its hash.

The app checks the manifest, refuses downgrades, downloads the bundle to its private app storage, verifies SHA-256, and then requests installation through the Windows Phone deployment API. The operating system validates the package signature and may show its own installation UI.

**Do not enable the channel while the package is missing or the hash is empty.**