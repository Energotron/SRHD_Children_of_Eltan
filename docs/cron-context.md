# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `e27b55bfd853100e4cfd81d6198f368264aaedf4`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods.
- Real SRHD layout permits nested module directories such as `Mods/Tweaks/German/ModuleInfo.txt`; therefore the release path must not assume every module is a direct child of `Mods/`.
- `Mods/ModCFG.txt` is confirmed as the enabled-mod/load-order configuration read by the game, but the exact minimal activation entry for a new `ChildrenOfEltan` module is still not runtime-verified in this repository.
- `Priority` from `ModuleInfo.txt` participates in effective load order. The textual order in `ModCFG.txt` is only sufficient when relevant mods have equal Priority values.
- `ModuleInfo.txt` is a real per-module descriptor: XenoModKit requires it for packaging, and official SRHD depot content contains multiple examples under `Mods/Tweaks/...`.
- SRHD XenoModKit remains accepted as `verified-tool-assisted` for structure/ModuleInfo audit, `ModCFG.txt` compatibility analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/
- https://www.moddb.com/mods/rogue-tranclucator

## Last completed increment

Verified and documented **SRHD module nesting + load-order semantics** without inventing a runtime package:

- corrected the earlier oversimplification that every mod must be a direct child of `Mods/`;
- documented verified `Mods/<Category>/<Mod>/ModuleInfo.txt` nesting;
- split activation from load-order semantics;
- promoted load-order semantics to `verified-moddable` because `ModCFG.txt` order and `ModuleInfo.txt` Priority behavior are independently documented;
- kept the exact activation entry and minimum `ModuleInfo.txt` field set at `researching` pending a clean in-game smoke-test.

## Checks

- Documentation/research-only increment; no proprietary base-game code/assets or third-party mod files were committed.
- `.github/project-mode.json` and `.github/release-decision.json` were inspected and standalone WebGL/APK releases remain disabled.
- `mod/` currently contains only repository-internal source metadata/docs (`README.md`, `project.json`); no invented native SRHD skeleton was added.
- Relevant quest inventory was inspected (`quests/quest_whisper_of_abyss.md`) but content was intentionally not modified because M1 loader verification has higher priority.
- Open blocking GitHub issues: none found.

## Known blocker

A legally installed Space Rangers HD instance is still required to prove the exact minimal `ChildrenOfEltan` activation entry, accepted `ModuleInfo.txt` keys/values, chosen category/module path and clean-game launch/effective-load-order behavior. Static/public evidence is sufficient for path and ordering semantics, not for claiming our new module is loadable.

## Next recommended increment

Derive the **smallest evidence-backed `ModuleInfo.txt` field set** from public format/tool validators and legally inspectable examples, then add only an original `ChildrenOfEltan` template plus a validation recipe; do not claim it runtime-verified until a clean installed SRHD smoke-test succeeds.
