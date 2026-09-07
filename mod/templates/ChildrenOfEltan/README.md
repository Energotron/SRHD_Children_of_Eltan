# Children of Eltan — ModuleInfo research template

This directory is an **original, legally clean research template** for the future SRHD module descriptor. It is not yet a runtime-verified release package.

## Evidence-backed field set

`SRHD-XenoModKit` currently uses a `ModuleInfo.txt` fixture with four descriptor keys:

- `Name`
- `Section`
- `Priority`
- `Languages`

The toolkit parser accepts case-insensitive `ModuleInfo.txt` discovery and `key=value` descriptor lines. Its native-loader tests exercise the same four fields in a synthetic mod fixture. This is sufficient to classify this exact template as **verified-tool-assisted** for static parsing/tooling research, but **not** as verified-moddable for actual SRHD loading.

Template values are original to this project:

```text
Name=ChildrenOfEltan
Section=OtherMods
Priority=1
Languages=Rus
```

`Priority=1` is chosen only to align with the documented equal-priority load-order model used by the current SRHD Mod Organizer 2 plugin. `Section=OtherMods` and `Languages=Rus` mirror field/value forms exercised by XenoModKit's own synthetic test fixture; they still require a clean-game smoke-test before being promoted to runtime-verified project settings.

## Validation boundary

Before shipping this descriptor, verify on a legally installed, explicitly versioned SRHD build:

1. place the module under a confirmed `Mods/<Category>/ChildrenOfEltan/` path;
2. add exactly one corresponding activation entry to `Mods/ModCFG.txt` using a format observed from the installed game;
3. confirm the module appears in the game's effective load order/mod UI;
4. launch a clean game session without loader errors;
5. record the game build, final category path, `ModCFG.txt` entry form, detected encoding, and result in `docs/cron-context.md`.

Until that succeeds, this folder must not be promoted as an installable release skeleton.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/module_info.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/tests/test_native_loader.py
- https://www.nexusmods.com/spacerangersawarapart/mods/57
