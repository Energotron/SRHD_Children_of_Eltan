# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling, asset tooling, and mod-first architecture docs.
- `game/webgl/` is legacy/reference only and is not the shipping runtime.
- Standalone WebGL/APK release promotion remains frozen.
- Master after this increment: `adb282abd29101cf3ef7f51f909e5992373f657f` before checkpoint update.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the user-mod root.
- Real SRHD modules may use nested layout `Mods/<Category>/<Mod>/ModuleInfo.txt` rather than only direct children of `Mods/`.
- Official Steam depot examples include `Mods/Tweaks/German/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate30/ModuleInfo.txt`, `Mods/Tweaks/SR2LoadingScreen/ModuleInfo.txt`, `Mods/Tweaks/SR2PQuestStyle/ModuleInfo.txt`, and `Mods/Tweaks/Spanish/ModuleInfo.txt`.
- `ModCFG.txt` activation syntax is `verified-tool-assisted`: the current MIT-licensed SRHD Mod Organizer 2 plugin documents `Mods/ModCFG.txt` with a `CurrentMod=` key containing an ordered comma-separated enabled-mod list.
- `Priority` from `ModuleInfo.txt` participates in effective load order. `CurrentMod` order maps directly only when enabled modules have equal priority; MO2 normalizes enabled modules to `Priority=1` in its VFS for deterministic ordering.
- Exact Children of Eltan `CurrentMod=` token/category path remains `researching` until primary-artifact inspection or installed-game smoke-test.
- `ModuleInfo.txt` release-safe encoding/category keys remain `researching`: XenoModKit accepts several encodings statically, while the current MO2 plugin expects UTF-16+BOM and reads `SectionEng=` for category identity. Do not promote the current research template to installable status yet.
- XenoModKit remains `verified-tool-assisted` for mod structure audit, ModuleInfo/ModCFG analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks, deterministic release staging and native-plugin validation.
- XenoNativeLoader Host API V1 remains `verified-tool-assisted` as an optional advanced extension path. It is not the default path for mechanics already supported by SRHD data/script systems.

Evidence:
- `docs/evidence/2026-09-07-srhd-modcfg-layout.md`
- https://github.com/ringill/spacerangers-modorganizer-plugin
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://github.com/Xenomorphchyma/XenoMods

## Asset pipeline state

- GI↔PNG and supported GAI/PKG tooling remain `verified-tool-assisted` through XenoModKit.
- No asset was generated in this increment because no new runtime-verified import point was required.
- Generated assets must remain original/license-clean and must be validated for the exact SRHD target format before inclusion.

## Last completed increment

Recorded a dedicated evidence note for the real SRHD mod loader contract and nested module layout:

- confirmed `Mods/<Category>/<Mod>/ModuleInfo.txt` against the official Steam depot structure;
- confirmed `ModCFG.txt` / `CurrentMod=` activation semantics through the current SRHD MO2 integration;
- confirmed `Priority` participation in effective load order;
- explicitly separated verified loader behavior from still-unverified Children of Eltan category/token/ModuleInfo encoding details;
- added `docs/evidence/2026-09-07-srhd-modcfg-layout.md` without copying proprietary game files or third-party mod code/assets.

## Checks

- Inspected fresh `master` and the previous checkpoint before selecting work.
- Verified standalone release freeze remains active in `.github/release-decision.json`.
- Cross-checked the current SRHD MO2 guide/plugin references and official Steam depot layout.
- No WebGL/APK work selected.
- No proprietary base-game code/assets or unclear-license mod content copied.

## Known blocker

A legally installed, versioned SRHD instance or equivalently strong primary artifact is still required to resolve the exact release-safe `ModuleInfo.txt` encoding/category keys and the exact `CurrentMod=` entry for `ChildrenOfEltan`, then prove clean launch/effective load order.

## Next recommended increment

Inspect a real shipped SRHD `ModuleInfo.txt` byte-for-byte (preferably one of the stock `Mods/Tweaks/*` modules), record its encoding and category/name keys, then update the Children of Eltan research template only if that primary evidence resolves the `Section` vs `SectionEng` and UTF-8 vs UTF-16+BOM discrepancy.
