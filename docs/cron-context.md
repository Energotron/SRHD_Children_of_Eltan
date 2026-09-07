# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `4d0a2714b9a2fbdd8ef225526b608735d2889884`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods.
- Real SRHD layout permits nested module directories such as `Mods/Tweaks/German/ModuleInfo.txt`; therefore the release path must not assume every module is a direct child of `Mods/`.
- `Mods/ModCFG.txt` is confirmed as the enabled-mod/load-order configuration read by the game, but the exact minimal activation entry for a new `ChildrenOfEltan` module is still not runtime-verified in this repository.
- `Priority` from `ModuleInfo.txt` participates in effective load order. The textual order in `ModCFG.txt` is only sufficient when relevant mods have equal Priority values.
- XenoModKit's parser accepts `ModuleInfo.txt` descriptor lines in `key=value` form and discovers the descriptor case-insensitively.
- XenoModKit's own native-loader test fixture exercises the descriptor keys `Name`, `Section`, `Priority`, and `Languages` together; this exact four-field research template is therefore `verified-tool-assisted` for static parsing/tooling, not yet `verified-moddable` for SRHD runtime loading.
- SRHD XenoModKit remains accepted as `verified-tool-assisted` for structure/ModuleInfo audit, `ModCFG.txt` compatibility analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/module_info.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/tests/test_native_loader.py
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/

## Last completed increment

Added the first **legally clean, evidence-backed `ModuleInfo.txt` research template** without claiming a runtime-ready package:

- created `mod/templates/ChildrenOfEltan/ModuleInfo.txt` with original values `Name=ChildrenOfEltan`, `Section=OtherMods`, `Priority=1`, `Languages=Rus`;
- created `mod/templates/ChildrenOfEltan/README.md` documenting the evidence, capability boundary and exact smoke-test recipe;
- kept the descriptor and package runtime status at `researching` until a legally installed SRHD build confirms category path, activation entry, encoding, mod UI/effective load order and clean launch.

## Checks

- Template uses only original project text; no proprietary base-game code/assets or third-party mod files were copied.
- Descriptor syntax is limited to the `key=value` form parsed by XenoModKit and the four keys exercised by its own synthetic native-loader test fixture.
- `.github/project-mode.json` and `.github/release-decision.json` remain unchanged; standalone WebGL/APK releases remain disabled.
- No WebGL/APK product work was selected.

## Known blocker

A legally installed Space Rangers HD instance is still required to prove the exact `ChildrenOfEltan` activation entry in `ModCFG.txt`, accepted category/module path, descriptor encoding and clean-game launch/effective-load-order behavior. Static/toolchain evidence does not justify promoting the template to runtime-verified.

## Next recommended increment

On a legally installed, explicitly versioned SRHD build, perform one clean smoke-test of this exact descriptor: derive the activation entry from the installed game's existing `ModCFG.txt` format, enable only the `ChildrenOfEltan` module, verify it appears in effective load order/mod UI, launch without loader errors, and record the final path/encoding/result.
