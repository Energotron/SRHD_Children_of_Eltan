# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling, asset tooling, and mod-first architecture docs.
- `game/webgl/` is legacy/reference only and is not the shipping runtime.
- Standalone WebGL/APK release promotion remains frozen.
- Master parent for this increment: `a7c5066ba468cfb6b19f205229b186ca2716d5b3`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the user-mod root.
- Real SRHD modules may use nested layout `Mods/<Category>/<Mod>/ModuleInfo.txt` rather than only direct children of `Mods/`.
- Official Steam depot examples include `Mods/Tweaks/German/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt`, `Mods/Tweaks/LeoDomikShipsUpdate30/ModuleInfo.txt`, `Mods/Tweaks/SR2LoadingScreen/ModuleInfo.txt`, `Mods/Tweaks/SR2PQuestStyle/ModuleInfo.txt`, and `Mods/Tweaks/Spanish/ModuleInfo.txt`.
- `ModCFG.txt` activation syntax is `verified-tool-assisted`: the current MIT-licensed SRHD Mod Organizer 2 plugin documents `Mods/ModCFG.txt` with a `CurrentMod=` key containing an ordered comma-separated enabled-mod list.
- Nested `CurrentMod` token shape is `verified-moddable`: public Molder's Mods instructions use `CurrentMod=OtherMods\MolderHulls,OtherMods\MolderMM`, while a public SRHD runtime log from build `2.1.2468` records `CurrentMod=ShusRangers\ShuEmitter`.
- `Priority` from `ModuleInfo.txt` participates in effective load order. `CurrentMod` order maps directly only when enabled modules have equal priority; MO2 normalizes enabled modules to `Priority=1` in its VFS for deterministic ordering.
- The exact Children of Eltan category remains `researching`; the final concrete token is not yet promoted to release contract.
- **`Section` + `SectionEng` coexistence/derivation is now `verified-tool-assisted`.** GPL-3.0 `jaroslavknotek/SRHD-lang-dat-translate` preserves `Section` and creates `SectionEng=<parent category folder>` during its SRHD module translation flow. Its test fixture asserts exactly one `SectionEng` equal to the parent category. README documents use across a broad Evolution/Expansion/Revolution/ShusRangers/OtherMods/Tweaks mod set.
- This resolves the previous false either/or interpretation: `SectionEng` evidence does not justify deleting `Section`. It does **not** yet resolve exact game-facing encoding/BOM or prove that `SectionEng` is mandatory for a Russian-only module.
- `ModuleInfo.txt` release-safe encoding remains `researching`: XenoModKit accepts several encodings statically, while the current MO2 plugin expects UTF-16+BOM. Do not promote the current UTF-8 research template to installable status yet.
- XenoModKit remains `verified-tool-assisted` for mod structure audit, ModuleInfo/ModCFG analysis, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks, deterministic release staging and native-plugin validation.
- XenoNativeLoader Host API V1 remains `verified-tool-assisted` as an optional advanced extension path, not the default path for mechanics already supported by SRHD data/script systems.

Evidence:
- `docs/evidence/2026-09-07-srhd-modcfg-layout.md`
- `docs/evidence/2026-09-07-currentmod-token-shape.md`
- `docs/evidence/2026-09-07-moduleinfo-sectioneng-semantics.md`
- https://github.com/ringill/spacerangers-modorganizer-plugin
- https://www.nexusmods.com/spacerangersawarapart/mods/57
- https://steamdb.info/depot/214731/
- https://www.playground.ru/space_rangers_2_dominators/file/space_rangers_hd_a_war_apart_sborka_molders_mods-1057692
- https://steamcommunity.com/app/214730/discussions/0/4363500699215030060/
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://github.com/Xenomorphchyma/XenoMods
- https://github.com/jaroslavknotek/SRHD-lang-dat-translate

## Asset pipeline state

- GI↔PNG and supported GAI/PKG tooling remain `verified-tool-assisted` through XenoModKit.
- No asset was generated in this increment because no newly verified asset import point was involved.
- Generated assets must remain original/license-clean and validated for the exact SRHD target format before inclusion.

## Last completed increment

Verified a specific **`ModuleInfo.txt` localization/category pattern** against an independent SRHD community toolchain:

- inspected `jaroslavknotek/SRHD-lang-dat-translate` (GPL-3.0, archived public repository, master tree `05b3f4f72029336b5f0a5a5aada22a6806897d22`);
- confirmed its translator preserves `Section` and derives `SectionEng` from the parent category folder;
- confirmed the repository test requires exactly one `SectionEng` with that category value;
- recorded the pattern as `verified-tool-assisted` rather than engine-native;
- documented why this resolves the `Section` vs `SectionEng` either/or conflict without claiming the byte encoding is solved;
- deliberately left `mod/templates/ChildrenOfEltan/ModuleInfo.txt` unchanged.

## Checks

- Inspected fresh `master` (`a7c5066ba468cfb6b19f205229b186ca2716d5b3`) and recent commits.
- Open issues: none.
- Inspected README, `docs/AGENT_DEVELOPMENT_LOOP.md`, `docs/MOD_ARCHITECTURE.md`, `docs/MODDING_CAPABILITY_MATRIX.md`, `docs/ROADMAP.md`, `.github/project-mode.json`, `.github/release-decision.json`, checkpoint, `mod/`, current `ModuleInfo.txt`, `data/`, `quests/`, lore, and current mod-first validation workflow.
- Inspected external `SRHD-lang-dat-translate` source, tests, README/tool purpose, repository state and GPL-3.0 license.
- No third-party code, game binaries, proprietary assets, or third-party mod content copied.
- No WebGL/APK work selected; standalone release freeze remains unchanged.
- No asset or mechanic implementation attempted in this evidence-only increment.

## Known blocker

A real shipped/installed SRHD `ModuleInfo.txt` artifact is still required to resolve exact release-safe byte encoding/BOM and determine which localized category fields are engine-required versus tool-convenience. Runtime acceptance still requires a pinned SRHD smoke-test.

## Next recommended increment

Acquire one real shipped/installed SRHD `Mods/Tweaks/*/ModuleInfo.txt` as a byte-level artifact and record BOM/encoding plus `Section`, `SectionEng`, `Name` and `Priority` before mutating the Children of Eltan template.
