# SRHD `ModuleInfo.txt`: `Section` / `SectionEng` semantics evidence

Date: 2026-09-07

## Capability

Classification: **`verified-tool-assisted`** for coexistence and generation semantics of `Section` + `SectionEng` in community SRHD mod tooling.

This evidence does **not** claim that the final release encoding of `ModuleInfo.txt` is resolved, and it does not replace an installed-game smoke test.

## Source inspected

- Repository: `jaroslavknotek/SRHD-lang-dat-translate`
- Repository state inspected: master tree `05b3f4f72029336b5f0a5a5aada22a6806897d22`
- License: GPL-3.0
- Status: archived public repository; used as behavioral/toolchain evidence only, no code copied into Children of Eltan.
- Purpose documented by the project: translate/transliterate Space Rangers HD mods, including `ModuleInfo.txt` and `CFG/<Lang>/Lang.dat`.

Relevant files:
- `python/app.py`
- `tests/test_app.py`
- `README.md`

## Verified behavior

`_transl_module_info_file(...)` preserves the original `Section=<value>` entry. When it encounters `Section`, it additionally creates `SectionEng=<location>`, where `location` is derived from `module_info_path.parent.parent.name` — the parent category directory in a layout equivalent to `Mods/<Category>/<Mod>/ModuleInfo.txt`.

The project's test fixture verifies this behavior with a synthetic `ModSection/TestMod/ModuleInfo.txt`: after translation there is exactly one `SectionEng`, and its value is `ModSection`.

The same test fixture models a practical descriptor with fields including `Name`, `Author`, `Conflict`, `Dependence`, `Priority`, `Section`, `Languages`, `SmallDescription`, and repeated `FullDescription` entries. This is useful field-shape evidence, but is not treated as proof that every field is engine-required.

The README states that the tool was used against a large community mod set spanning Evolution, Expansion, Revolution, ShusRangers, OtherMods and Tweaks modules. This makes the `Section`/`SectionEng` behavior relevant to established SRHD mod workflows rather than a Children of Eltan-specific invention.

## What this resolves

The previous apparent choice between `Section` **or** `SectionEng` was too strong. Community tooling provides independent evidence that the fields may legitimately coexist:

- `Section` is preserved;
- `SectionEng` is an English/category counterpart generated from the parent category folder.

Therefore the current Children of Eltan research descriptor must not delete `Section` merely because another tool reads `SectionEng`.

## What remains unresolved

1. Exact release-safe byte encoding/BOM for game-facing `ModuleInfo.txt`.
2. Whether `SectionEng` is engine-required for a Russian-only module or only required/expected by specific tooling/localization flows.
3. Final Children of Eltan category folder and therefore final `SectionEng`/`CurrentMod` token.
4. Runtime acceptance on a pinned SRHD build.

## References

- https://github.com/jaroslavknotek/SRHD-lang-dat-translate
- https://github.com/jaroslavknotek/SRHD-lang-dat-translate/blob/master/python/app.py
- https://github.com/jaroslavknotek/SRHD-lang-dat-translate/blob/master/tests/test_app.py
