# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.

## Migration directive

Autonomous agents must stop selecting standalone WebGL feature work as the default next increment. Work should first establish a verified KR2 modding capability, package layout, install path and smoke-test workflow. Do not guess unsupported formats or commit proprietary base-game assets.

## Legacy state

The existing WebGL prototype, Android work, tests and prior release history are preserved for reference. They may be mined for original mechanics/data/design, but they do not override the mod-first architecture.

## Next recommended increment

Complete the M1 modding capability audit: verify the exact KR2/SRHD mod mechanism, target version, directory/layout, encodings, packaging, install/uninstall procedure and smallest reproducible loadable mod.
