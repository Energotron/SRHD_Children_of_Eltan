# Children of Eltan — ModuleInfo research template

This directory is an **original, legally clean research template** for the future SRHD module descriptor. It is not yet a runtime-verified release package.

## Evidence-backed field set

`SRHD-XenoModKit` parses `ModuleInfo.txt` as case-insensitive descriptor discovery plus `key=value` lines. Its validation code gives us a tighter static contract than the earlier synthetic fixture alone:

- `Name` is the only descriptor field whose absence is an error in `validate_mod()`;
- `Priority`, when present, must parse as an integer;
- missing `Languages` is informational rather than a validation error;
- `Section` is accepted by the parser/toolchain but is not required by this validator.

The toolkit's native-loader tests also exercise the four-field fixture used here:

- `Name`
- `Section`
- `Priority`
- `Languages`

This is sufficient to classify the **static descriptor/tooling contract** as **verified-tool-assisted**. It still does **not** prove that a fresh SRHD runtime accepts this exact module, category, values or activation entry.

Template values are original to this project:

```text
Name=ChildrenOfEltan
Section=OtherMods
Priority=1
Languages=Rus
```

`Priority=1` is chosen only to align with the documented equal-priority load-order model used by the current SRHD Mod Organizer 2 plugin. `Section=OtherMods` and `Languages=Rus` mirror forms exercised by XenoModKit tooling and still require a clean-game smoke-test before becoming runtime-verified project settings.

## Encoding contract

XenoModKit's SRHD text validator allows `ModuleInfo.txt` in `cp1251`, `utf-16-le` or `utf-16-be`. It also deliberately treats an **ASCII-only UTF-8 file without BOM as byte-safe**, because the bytes are identical for the ASCII subset. The current template is ASCII-only and therefore passes this static compatibility exception.

Do not add Cyrillic or other non-ASCII text directly to this UTF-8 template and assume it remains game-safe. If localized/non-ASCII descriptor values become necessary, generate or convert the final game-facing descriptor to a verified SRHD encoding (normally Windows-1251 or a verified UTF-16 form) and validate that output with the mod toolchain before packaging.

## Validation boundary

Before shipping this descriptor, verify on a legally installed, explicitly versioned SRHD build:

1. place the module under a confirmed `Mods/<Category>/ChildrenOfEltan/` path;
2. add exactly one corresponding activation entry to `Mods/ModCFG.txt` using a format observed from the installed game;
3. confirm the module appears in the game's effective load order/mod UI;
4. launch a clean game session without loader errors;
5. record the game build, final category path, `ModCFG.txt` entry form, final descriptor encoding, and result in `docs/cron-context.md`.

Until that succeeds, this folder must not be promoted as an installable release skeleton.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/module_info.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/validation.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/textio.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/srhd_modkit/game_text.py
- https://github.com/Xenomorphchyma/SRHD-XenoModKit/blob/master/tests/test_native_loader.py
- https://www.nexusmods.com/spacerangersawarapart/mods/57
