# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `a3fc709926339c958e6c5b02e5e417eb9fdd1740`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods.
- Real SRHD layout permits nested module directories such as `Mods/Tweaks/German/ModuleInfo.txt`; therefore the release path must not assume every module is a direct child of `Mods/`.
- **`ModCFG.txt` activation syntax is now `verified-tool-assisted`.** The MIT-licensed `ringill/spacerangers-modorganizer-plugin` source documents and implements the engine-facing contract: `Mods/ModCFG.txt` contains a `CurrentMod=` key whose value is a comma-separated, ordered list of enabled mod entries. There is no separate enabled flag in that model; membership in `CurrentMod` is the activation signal.
- The same plugin documents `ModCFG.txt` as UTF-8 and writes entries joined as `CurrentMod=ModA, ModB, ...`, preserving unrelated lines and line endings. This is strong tool/source evidence for the activation record format, but the exact Children of Eltan category/name entry still requires a real installed-game smoke-test.
- `Priority` from `ModuleInfo.txt` participates in effective load order. The textual order in `CurrentMod` is authoritative only when relevant enabled mods have equal Priority values; the MO2 plugin equalizes enabled mods to `Priority=1` in its VFS so the engine order follows `CurrentMod` exactly.
- The MO2 plugin source also treats `ModuleInfo.txt` as UTF-16 with BOM and reads `SectionEng=` as the category/folder identity used for `<Category>/<Mod>` mapping. This conflicts with the current research template's ASCII-only UTF-8 plus `Section=OtherMods`, so the template must **not** be promoted to installable status until this discrepancy is resolved against real shipped modules / runtime behavior.
- XenoModKit's parser accepts case-insensitive `ModuleInfo.txt` discovery and `key=value` descriptor lines.
- **Static `ModuleInfo.txt` descriptor validation remains `verified-tool-assisted`.** In current XenoModKit, `Name` is the only descriptor field whose absence is a validation error; `Priority`, when present, must be an integer; missing `Languages` is informational; `Section` is parser/toolchain data rather than a validator-required field.
- XenoModKit's SRHD text lint allows `cp1251`, `utf-16-le`, and `utf-16-be` for `ModuleInfo.txt`, and explicitly accepts ASCII-only UTF-8 without BOM as byte-safe. That static lint result does not overrule the MO2 plugin's engine-facing UTF-16/BOM expectation; runtime evidence is now required before choosing the release encoding.
- SRHD XenoModKit remains accepted as `verified-tool-assisted` for structure/ModuleInfo audit, `ModCFG.txt` compatibility analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.
- **XenoNativeLoader Host API V1 is `verified-tool-assisted` as a native-extension toolchain path.** XenoModKit 0.10.2 can scaffold/build/static-validate x86 PE32 `*.XenoPlugin.dll` modules and exact ABI exports `XenoPlugin_Query` / `XenoPlugin_Initialize`.
- Public `Xenomorphchyma/XenoMods` examples demonstrate XenoNativeLoader 0.6.7 with real SRHD native mods including `XenoBigGalaxy`, `XenoEquipmentInflation`, `XenoHangarPaging`, `XenoCoalitionSupplyLines`, and `XenoDomRangers`. The loader uses `dsound.dll`/`XenoCore.dll`, reads active `Mods/ModCFG.txt`, loads per-mod DLLs from `Native/`, and performs signature checks before hooks rather than modifying `Rangers.exe` on disk.
- `Xenomorphchyma/XenoMods` reports SPDX `NOASSERTION`; use it as behavioral/architectural evidence only unless reuse permission is established. Do not copy its code/assets/content into this repository on that evidence alone.

Evidence:
- https://github.com/ringill/spacerangers-modorganizer-plugin/blob/main/games/spacerangershd/modcfg.py
- https://github.com/ringill/spacerangers-modorganizer-plugin
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://github.com/Xenomorphchyma/XenoMods
- https://steamdb.info/depot/214731/

## Asset pipeline state

- GI↔PNG and supported GAI/PKG tooling remain `verified-tool-assisted` through XenoModKit.
- No new generated asset was added in this increment because no new asset import point was required or runtime-verified.
- Continue to require original/license-clean sources plus format/dimension/encoding validation before any generated asset enters a release package.

## Last completed increment

Verified the engine-facing **`ModCFG.txt` / `CurrentMod=` control-file contract** against the current open-source SRHD Mod Organizer 2 plugin:

- confirmed `CurrentMod=` as the comma-separated ordered enabled-mod list;
- confirmed no separate enable flag in that model;
- confirmed UTF-8 handling for `ModCFG.txt` and canonical writer form `CurrentMod=ModA, ModB`;
- confirmed equal-Priority requirement for `CurrentMod` order to map directly to engine load order;
- identified a material compatibility discrepancy: the MO2 plugin expects UTF-16+BOM `ModuleInfo.txt` and reads `SectionEng=`, while the current Children of Eltan research template is ASCII-only UTF-8 and uses `Section=OtherMods`;
- therefore made no unsafe template mutation and did not claim the current skeleton is installable.

## Checks

- Inspected fresh `master` and prior checkpoint before selecting work.
- Inspected current `mod/templates/ChildrenOfEltan/ModuleInfo.txt`.
- Inspected `ringill/spacerangers-modorganizer-plugin` repository metadata and current `games/spacerangershd/modcfg.py` source.
- Source license header: SPDX `MIT`; no third-party code or assets copied.
- No proprietary base-game code/assets were copied.
- No WebGL/APK product work was selected.
- Standalone release freeze remains unchanged.

## Known blocker

A legally installed, explicitly versioned Space Rangers HD instance is still required to resolve the now-explicit `ModuleInfo.txt` compatibility discrepancy (`Section` vs `SectionEng`, ASCII UTF-8 vs UTF-16+BOM), derive the exact `CurrentMod=` entry for the chosen `<Category>/<Mod>` path, and prove clean launch/effective load order.

## Next recommended increment

Inspect real shipped/installed SRHD `ModuleInfo.txt` files (for example the stock `Mods/Tweaks/*` modules) and compare their byte encoding plus category keys against the MO2 plugin contract. Only after that evidence should the Children of Eltan template be converted to a concrete release-safe `ModuleInfo.txt` and paired with an exact `CurrentMod=` activation entry.
