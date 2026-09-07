# Automation Context Checkpoint

Updated: 2026-09-07

## Canonical state

- Branch: `master`.
- Product: **«Дети Эльтана» — mod for Space Rangers 2 / Space Rangers HD: A War Apart**.
- Canonical mod work: `mod/`, `data/`, `quests/`, mod tooling and current mod architecture docs.
- `game/webgl/` is legacy/reference only and is no longer the shipping runtime.
- Standalone WebGL/APK release promotion is frozen.
- Restored master before this increment: `f20d6607d09fb56b746749e60a54d6fce45179a0`.

## Verified modding/toolchain state

- `Space Rangers HD/Mods/` is confirmed as the filesystem root for user mods by a real distributed SRHD mod and by SRHD XenoModKit deployment semantics.
- SRHD XenoModKit 0.10.2 is accepted as a `verified-tool-assisted` research/build candidate for structure/ModuleInfo audit, `ModCFG.txt` load-order inspection, DAT, SCR/RSON/RSM, QM/QMM, GI/GAI/HAI/PKG, encoding checks and deterministic release staging.
- Full activation/load procedure is **not yet considered verified in this repository**: exact minimal `ModuleInfo`, required runtime files, target SRHD build and a clean in-game smoke-test remain open.
- `ModCFG.txt` is confirmed to participate in active-mod/load-order configuration; XenoModKit reads it but deliberately does not rewrite it automatically.

Evidence:
- https://github.com/Xenomorphchyma/SRHD-XenoModKit
- https://www.moddb.com/mods/rogue-tranclucator

## Last completed increment

Documented the first verified part of the real SRHD mod path instead of inventing a package layout:

- split installation root from activation/load-order status in the capability matrix;
- classified supported XenoModKit-backed formats as `verified-tool-assisted` while preserving in-game smoke-test boundaries;
- updated `mod/README.md` so `Mods/` is now the confirmed deployment root but the internal package skeleton remains intentionally unclaimed until tested.

## Checks

- Documentation-only increment; no proprietary game assets/code added.
- Existing project/release JSON files were inspected and remain mod-first with standalone releases disabled.
- Open blocking GitHub issues: none found.
- No standalone WebGL/APK release changes.

## Known blocker

A legally installed Space Rangers HD instance is required to prove the minimal `ChildrenOfEltan` runtime skeleton, exact `ModuleInfo` fields, `ModCFG.txt` activation entry and clean-game launch behavior. Static tooling alone is not enough to claim this final load path as verified.

## Next recommended increment

Use SRHD XenoModKit against a clean installed SRHD copy to derive and validate the **smallest legally-clean `ChildrenOfEltan` mod skeleton**: minimal `ModuleInfo` + directory contents + explicit `ModCFG.txt` activation/load-order evidence + successful game smoke-test, then commit only the original skeleton/templates and reproducible validation instructions.
