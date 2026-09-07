# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `030e79cfdef551e6ec7295b1977c8bd607d494c7`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods.
- Real SRHD layout permits nested module directories such as `Mods/Tweaks/German/ModuleInfo.txt`; therefore the release path must not assume every module is a direct child of `Mods/`.
- `Mods/ModCFG.txt` is confirmed as the enabled-mod/load-order configuration read by the game, but the exact minimal activation entry for a new `ChildrenOfEltan` module is still not runtime-verified in this repository.
- `Priority` from `ModuleInfo.txt` participates in effective load order. The textual order in `ModCFG.txt` is only sufficient when relevant mods have equal Priority values.
- XenoModKit's parser accepts `ModuleInfo.txt` descriptor lines in `key=value` form and discovers the descriptor case-insensitively.
- XenoModKit's own native-loader test fixture exercises the descriptor keys `Name`, `Section`, `Priority`, and `Languages` together; this exact four-field research template is therefore `verified-tool-assisted` for static parsing/tooling, not yet `verified-moddable` for SRHD runtime loading.
- SRHD XenoModKit remains accepted as `verified-tool-assisted` for structure/ModuleInfo audit, `ModCFG.txt` compatibility analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.
- **XenoNativeLoader Host API V1 is now classified `verified-tool-assisted` as a native-extension toolchain path.** XenoModKit 0.10.2 can scaffold/build/static-validate x86 PE32 `*.XenoPlugin.dll` modules and exact ABI exports `XenoPlugin_Query` / `XenoPlugin_Initialize`.
- Public `Xenomorphchyma/XenoMods` examples demonstrate XenoNativeLoader 0.6.7 with real SRHD native mods including `XenoBigGalaxy`, `XenoEquipmentInflation`, `XenoHangarPaging`, `XenoCoalitionSupplyLines`, and `XenoDomRangers`. The loader uses `dsound.dll`/`XenoCore.dll`, reads active `Mods/ModCFG.txt`, loads per-mod DLLs from `Native/`, and performs signature checks before hooks rather than modifying `Rangers.exe` on disk.
- This does **not** verify any specific Children of Eltan native hook or runtime compatibility. Native plugins remain an advanced fallback only where DAT/RScript/QMM cannot provide the mechanic.
- `Xenomorphchyma/XenoMods` reports SPDX `NOASSERTION`; use it as behavioral/architectural evidence only unless reuse permission is established. Do not copy its code/assets/content into this repository on that evidence alone.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/module_info.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/tests/test_native_loader.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/README_RU.md
- https://github.com/Xenomorphchyma/XenoMods
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/

## Last completed increment

Verified and documented the professional **native-extension path** used by current SRHD mod tooling without adopting it as the default mechanic path:

- added `Nativные DLL-плагины через XenoNativeLoader` to `docs/MODDING_CAPABILITY_MATRIX.md` as `verified-tool-assisted`;
- recorded XenoModKit 0.10.2 Host API V1 static validation constraints (MSVC x86/PE32, exact ABI exports, manifest/config discovery);
- recorded real XenoMods/XenoNativeLoader 0.6.7 examples as behavioral evidence of per-mod native DLL loading and signature-guarded hooks;
- preserved the boundary that specific hooks remain unverified until an installed-game smoke-test;
- preserved the legal boundary: XenoMods source/content is reference-only while its reuse license remains unclear.

Matrix commit for this increment: `d8e1b32fe83ab6bb0be05651ad1f462981a093fe`.

## Checks

- No proprietary base-game code/assets or third-party mod files were copied.
- No XenoMods code/content was imported; only public architecture/tool behavior was documented.
- Capability was classified at the toolchain level only; no unsupported Children of Eltan engine hook was claimed.
- `.github/project-mode.json` and `.github/release-decision.json` remain unchanged; standalone WebGL/APK releases remain disabled.
- No WebGL/APK product work was selected.
- Repository has no open blocking issues at the start of this run.

## Known blocker

A legally installed Space Rangers HD instance is still required to prove the exact `ChildrenOfEltan` activation entry in `ModCFG.txt`, accepted category/module path, descriptor encoding and clean-game launch/effective-load-order behavior. The newly verified native-extension toolchain also cannot promote a specific hook to runtime-supported without an explicitly versioned SRHD smoke-test.

## Next recommended increment

On a legally installed, explicitly versioned SRHD build, perform one clean smoke-test of the existing `mod/templates/ChildrenOfEltan/ModuleInfo.txt`: derive the activation entry from the installed game's real `ModCFG.txt`, enable only `ChildrenOfEltan`, verify effective load order/mod UI and clean launch, then record the exact accepted path, encoding and result.
