# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `69e0a7b71361017d56e5dc9b7b29d2624bf3856c`.
- Current increment content commit: `52616271b5db324a51a4db8d8f8ad39b56452360`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods.
- Real SRHD layout permits nested module directories such as `Mods/Tweaks/German/ModuleInfo.txt`; therefore the release path must not assume every module is a direct child of `Mods/`.
- `Mods/ModCFG.txt` is confirmed as the enabled-mod/load-order configuration read by the game, but the exact minimal activation entry for a new `ChildrenOfEltan` module is still not runtime-verified in this repository.
- `Priority` from `ModuleInfo.txt` participates in effective load order. The textual order in `ModCFG.txt` is only sufficient when relevant mods have equal Priority values.
- XenoModKit's parser accepts case-insensitive `ModuleInfo.txt` discovery and `key=value` descriptor lines.
- **Static `ModuleInfo.txt` descriptor validation is `verified-tool-assisted`.** In current XenoModKit, `Name` is the only descriptor field whose absence is a validation error; `Priority`, when present, must be an integer; missing `Languages` is informational; `Section` is parser/toolchain data rather than a validator-required field.
- XenoModKit's native-loader fixture exercises `Name`, `Section`, `Priority`, and `Languages` together, matching the current original research template.
- XenoModKit's SRHD text lint allows `cp1251`, `utf-16-le`, and `utf-16-be` for `ModuleInfo.txt`, and explicitly accepts ASCII-only UTF-8 without BOM as byte-safe. The current template is ASCII-only, so it is statically encoding-compatible. Non-ASCII descriptor values must not be added without conversion/validation to a verified game-facing encoding.
- This static validation does **not** promote the exact `ChildrenOfEltan` module path, `Section=OtherMods`, `Languages=Rus`, `Priority=1`, or `ModCFG.txt` activation form to `verified-moddable`; those remain runtime research items until a clean installed-game smoke-test.
- SRHD XenoModKit remains accepted as `verified-tool-assisted` for structure/ModuleInfo audit, `ModCFG.txt` compatibility analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.
- **XenoNativeLoader Host API V1 is `verified-tool-assisted` as a native-extension toolchain path.** XenoModKit 0.10.2 can scaffold/build/static-validate x86 PE32 `*.XenoPlugin.dll` modules and exact ABI exports `XenoPlugin_Query` / `XenoPlugin_Initialize`.
- Public `Xenomorphchyma/XenoMods` examples demonstrate XenoNativeLoader 0.6.7 with real SRHD native mods including `XenoBigGalaxy`, `XenoEquipmentInflation`, `XenoHangarPaging`, `XenoCoalitionSupplyLines`, and `XenoDomRangers`. The loader uses `dsound.dll`/`XenoCore.dll`, reads active `Mods/ModCFG.txt`, loads per-mod DLLs from `Native/`, and performs signature checks before hooks rather than modifying `Rangers.exe` on disk.
- This does **not** verify any specific Children of Eltan native hook or runtime compatibility. Native plugins remain an advanced fallback only where DAT/RScript/QMM cannot provide the mechanic.
- `Xenomorphchyma/XenoMods` reports SPDX `NOASSERTION`; use it as behavioral/architectural evidence only unless reuse permission is established. Do not copy its code/assets/content into this repository on that evidence alone.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/module_info.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/validation.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/textio.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/game_text.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/tests/test_native_loader.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/README_RU.md
- https://github.com/Xenomorphchyma/XenoMods
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/

## Asset pipeline state

- GI↔PNG and supported GAI/PKG tooling remain `verified-tool-assisted` through XenoModKit.
- No new generated asset was added in this increment because no new asset import point was required or runtime-verified.
- Continue to require original/license-clean sources plus format/dimension/encoding validation before any generated asset enters a release package.

## Last completed increment

Verified the **static `ModuleInfo.txt` descriptor and encoding contract** against current XenoModKit source and tightened the research-template documentation:

- confirmed `Name` as the only descriptor field whose absence is a static validation error;
- confirmed integer validation for `Priority` and informational treatment of missing `Languages`;
- confirmed the current four-field template remains a tool-assisted research fixture rather than runtime proof;
- confirmed XenoModKit's explicit ASCII-only UTF-8 compatibility exception, so the current ASCII descriptor does not need a fake encoding conversion merely to pass static lint;
- documented that any future non-ASCII descriptor values must be converted/validated to a verified SRHD game-facing encoding;
- left the actual `ModuleInfo.txt` values unchanged and did not claim successful game loading.

Content commit: `52616271b5db324a51a4db8d8f8ad39b56452360`.

## Checks

- Inspected fresh `master`, README, agent loop, mod architecture, capability matrix, roadmap, project mode, release decision, current `mod/` tree, recent commits, open issues and checkpoint before selecting work.
- Open GitHub issues at selection time: none.
- Cross-checked current `mod/templates/ChildrenOfEltan/ModuleInfo.txt` against XenoModKit `module_info.py`, `validation.py`, `textio.py`, and `game_text.py` behavior.
- Current descriptor remains ASCII-only: `Name=ChildrenOfEltan`, `Section=OtherMods`, `Priority=1`, `Languages=Rus`.
- No proprietary base-game code/assets or third-party mod files were copied.
- No XenoMods code/content was imported.
- `.github/project-mode.json` and `.github/release-decision.json` remain unchanged; standalone WebGL/APK releases remain disabled.
- No WebGL/APK product work was selected.

## Known blocker

A legally installed, explicitly versioned Space Rangers HD instance is still required to prove the exact `ChildrenOfEltan` activation entry in `ModCFG.txt`, accepted category/module path, final descriptor encoding behavior in the real loader, and clean-game launch/effective-load-order behavior. Static XenoModKit validation cannot substitute for that runtime test.

## Next recommended increment

On a legally installed, explicitly versioned SRHD build, perform one clean smoke-test of the existing `mod/templates/ChildrenOfEltan/ModuleInfo.txt`: derive the activation entry from the installed game's real `ModCFG.txt`, enable only `ChildrenOfEltan`, verify effective load order/mod UI and clean launch, then record the exact accepted path, activation syntax, encoding and result.
