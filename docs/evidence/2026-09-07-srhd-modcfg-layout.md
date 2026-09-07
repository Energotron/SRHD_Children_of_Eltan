# SRHD mod loader evidence — ModCFG and nested module layout

Date: 2026-09-07

## Capability classification

- `Mods/` as user-mod root: `verified-moddable`
- nested `Mods/<Category>/<Mod>/ModuleInfo.txt` layout: `verified-moddable`
- `ModCFG.txt` / `CurrentMod=` activation record: `verified-tool-assisted`
- exact Children of Eltan `CurrentMod=` entry: `researching`
- release-safe `ModuleInfo.txt` encoding/category keys: `researching`

## Evidence

### Mod Organizer 2 plugin for Space Rangers HD

Source:
- https://github.com/ringill/spacerangers-modorganizer-plugin
- https://www.nexusmods.com/spacerangersawarapart/mods/57

The current SRHD MO2 integration documents the engine-facing control file as `Mods/ModCFG.txt` and represents enabled mods through a `CurrentMod=` key containing an ordered comma-separated list.

It also documents that real SRHD modules may be nested as:

`Mods/<Category_Folder>/<Mod_Folder>/ModuleInfo.txt`

and that `Priority` from `ModuleInfo.txt` participates in effective load order. MO2 normalizes enabled modules to equal priority so the `CurrentMod` order maps directly to the engine load order.

This is used as tool-assisted evidence only; no plugin code is copied into Children of Eltan.

### Official SRHD Steam depot structure

Source:
- https://steamdb.info/depot/214731/

The shipped game depot contains real module layouts including:

- `Mods/Tweaks/German/ModuleInfo.txt`
- `Mods/Tweaks/LeoDomikShipsUpdate15/ModuleInfo.txt`
- `Mods/Tweaks/LeoDomikShipsUpdate30/ModuleInfo.txt`
- `Mods/Tweaks/SR2LoadingScreen/ModuleInfo.txt`
- `Mods/Tweaks/SR2PQuestStyle/ModuleInfo.txt`
- `Mods/Tweaks/Spanish/ModuleInfo.txt`

This independently confirms the nested `<Category>/<Mod>` structure in the released product.

## What is now safe to rely on

The Children of Eltan package may target the SRHD `Mods/` root and may use a nested category/module directory. Activation is controlled through `ModCFG.txt`/`CurrentMod=` rather than by an invented per-mod enable flag.

## What is deliberately not claimed yet

This evidence does **not** prove the final category name, exact `CurrentMod=` token, `ModuleInfo.txt` key set, byte encoding, or runtime loadability for `ChildrenOfEltan`. Those remain blocked on inspection/smoke-test against a legally installed SRHD build or an equivalently strong primary artifact.

No proprietary game files or third-party mod assets/code are included in this repository as part of this verification.
