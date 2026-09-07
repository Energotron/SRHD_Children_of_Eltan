# SRHD `CurrentMod` token shape evidence

Date: 2026-09-07

## Question

What exact identifier shape does Space Rangers HD use inside `Mods/ModCFG.txt` for an enabled nested mod?

## Evidence inspected

1. Public Molder's Mods assembly instructions for Space Rangers HD show two enabled mods written as:

   `CurrentMod=OtherMods\MolderHulls,OtherMods\MolderMM`

   Source: https://www.playground.ru/space_rangers_2_dominators/file/space_rangers_hd_a_war_apart_sborka_molders_mods-1057692

2. A public Space Rangers HD runtime log from build `2.1.2468` (9 February 2024) records:

   `CurrentMod=ShusRangers\ShuEmitter`

   Source: https://steamcommunity.com/app/214730/discussions/0/4363500699215030060/

3. The current SRHD Mod Organizer 2 guide independently documents the physical layout as:

   `Mods\<Category_Folder>\<Mod_Folder>\ModuleInfo.txt`

   and confirms that `Mods/ModCFG.txt` controls enabled mods/load order.

   Source: https://www.nexusmods.com/spacerangersawarapart/mods/57

## Verified pattern

For nested SRHD mods, the `CurrentMod` entry is not merely the leaf mod folder name. Public mod instructions and an actual game runtime log both demonstrate a relative module identifier of the form:

`<Category>\<Mod>`

Multiple enabled modules are comma-separated on the same `CurrentMod=` value.

Capability classification: **`verified-moddable`** for the identifier *shape* and comma-separated composition.

## Children of Eltan consequence

The eventual activation token should therefore be derived from the chosen physical module path. For example, a release path `Mods/OtherMods/ChildrenOfEltan/ModuleInfo.txt` would imply an activation token shaped as `OtherMods\ChildrenOfEltan`.

That example is intentionally not promoted to the release contract yet because the project's final category folder is still blocked on `ModuleInfo.txt` category-key/encoding verification. The verified result in this note is only the `<Category>\<Mod>` token shape.

## Legal/provenance note

No game binary, proprietary asset, or third-party mod file was copied. The cited public pages are used only as behavioral/runtime evidence.
