# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling, asset tooling, and mod-first architecture docs.
- `game/webgl/` is legacy/reference only and is not the shipping runtime.
- Standalone WebGL/APK release promotion remains frozen.
- Master after evidence commit: `6254919b66921df62bf954522298d3a2432db62c` before checkpoint update.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the user-mod root.
- Real SRHD modules may use nested layout `Mods/<Category>/<Mod>/ModuleInfo.txt` rather than only direct children of `Mods/`.
- Official Steam depot examples include `Mods/Tweaks/German/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate30/ModuleInfo.txt`, `Mods/Tweaks/SR2LoadingScreen/ModuleInfo.txt`, `Mods/Tweaks/SR2PQuestStyle/ModuleInfo.txt`, and `Mods/Tweaks/Spanish/ModuleInfo.txt`.
- `ModCFG.txt` activation syntax is `verified-tool-assisted`: the current MIT-licensed SRHD Mod Organizer 2 plugin documents `Mods/ModCFG.txt` with a `CurrentMod=` key containing an ordered comma-separated enabled-mod list.
- **Nested `CurrentMod` token shape is now `verified-moddable`.** Public Molder's Mods instructions use `CurrentMod=OtherMods\MolderHulls,OtherMods\MolderMM`, while a public SRHD runtime log from build `2.1.2468` records `CurrentMod=ShusRangers\ShuEmitter`. Together with the documented `Mods/<Category>/<Mod>/ModuleInfo.txt` layout, this verifies the token form `<Category>\<Mod>` and comma-separated composition for multiple enabled modules.
- `Priority` from `ModuleInfo.txt` participates in effective load order. `CurrentMod` order maps directly only when enabled modules have equal priority; MO2 normalizes enabled modules to `Priority=1` in its VFS for deterministic ordering.
- The exact Children of Eltan category remains `researching`; therefore the final concrete token (for example `OtherMods\ChildrenOfEltan`) is not yet promoted to release contract even though the identifier shape itself is verified.
- `ModuleInfo.txt` release-safe encoding/category keys remain `researching`: XenoModKit accepts several encodings statically, while the current MO2 plugin expects UTF-16+BOM and reads `SectionEng=` for category identity. Do not promote the current research template to installable status yet.
- XenoModKit remains `verified-tool-assisted` for mod structure audit, ModuleInfo/ModCFG analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks, deterministic release staging and native-plugin validation.
- XenoNativeLoader Host API V1 remains `verified-tool-assisted` as an optional advanced extension path. It is not the default path for mechanics already supported by SRHD data/script systems.

Evidence:
- `docs/evidence/2026-09-07-srhd-modcfg-layout.md`
- `docs/evidence/2026-09-07-currentmod-token-shape.md`
- https://github.com/ringill/spacerangers-modorganizer-plugin
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/
- https://www.playground.ru/space_rangers_2_dominators/file/space_rangers_hd_a_war_apart_sborka_molders_mods-1057692
- https://steamcommunity.com/app/214730/discussions/0/4363500699215030060/
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://github.com/Xenomorphchyma/XenoMods

## Asset pipeline state

- GI↔PNG and supported GAI/PKG tooling remain `verified-tool-assisted` through XenoModKit.
- No asset was generated in this increment because no new runtime-verified import point was required.
- Generated assets must remain original/license-clean and must be validated for the exact SRHD target format before inclusion.

## Last completed increment

Verified the exact **nested `CurrentMod` identifier shape** used by real SRHD mods:

- confirmed `<Category>\<Mod>` from public Molder's Mods activation instructions;
- independently confirmed the same shape from an actual SRHD runtime log (`ShusRangers\ShuEmitter`);
- retained comma-separated composition for multiple enabled modules;
- classified this specific loader capability as `verified-moddable`;
- documented the evidence in `docs/evidence/2026-09-07-currentmod-token-shape.md`;
- deliberately did not mutate `mod/templates/ChildrenOfEltan/ModuleInfo.txt`, because its final category and release-safe encoding remain unresolved.

## Checks

- Inspected fresh `master`, recent commits, open issues, README, agent loop, current capability matrix, release freeze, template `ModuleInfo.txt`, and checkpoint before selecting work.
- Cross-checked independent public mod instructions, a real SRHD runtime log, the current SRHD MO2 guide/plugin model, and official nested module layout evidence.
- No WebGL/APK work selected.
- No proprietary base-game code/assets or unclear-license mod content copied.
- No asset/mechanic implementation was attempted beyond the verified loader-contract increment.

## Known blocker

A real shipped/installed SRHD `ModuleInfo.txt` artifact is still required to resolve the exact release-safe encoding and category keys (`Section` vs `SectionEng`). Until that is proven, the project should not lock the final Children of Eltan category folder or promote the research template to installable status.

## Next recommended increment

Inspect one real shipped SRHD `ModuleInfo.txt` byte-for-byte (preferably a stock `Mods/Tweaks/*` module), record BOM/encoding and category/name keys, then update the Children of Eltan research template only if that primary evidence resolves the `Section` vs `SectionEng` and UTF-8 vs UTF-16 discrepancy.
