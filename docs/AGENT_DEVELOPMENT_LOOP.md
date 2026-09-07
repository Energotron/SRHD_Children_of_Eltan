# Agent Development Loop — Children of Eltan

## Purpose

Develop **«Дети Эльтана»** as a mod for **Космические Рейнджеры 2 / Space Rangers HD**, not as a standalone replacement engine.

## Canonical loop

`inspect master -> verify modding capability -> choose one mod-first increment -> implement -> validate/package -> commit -> handoff`

## Required reading

1. `README.md`
2. `docs/MOD_ARCHITECTURE.md`
3. `docs/ROADMAP.md`
4. latest `master` commits
5. current modding research / compatibility docs
6. relevant lore, quest and design documents

## Priority order

1. establish or repair the actual KR2/SRHD mod toolchain;
2. fix reproducible packaging/install/compatibility failures;
3. complete unfinished mod content already present in `master`;
4. add one high-value original quest/content/system extension supported by the confirmed modding path;
5. improve tooling, validation and documentation that directly supports the mod.

## Capability rule

Before coding a feature, classify its implementation path as:

- native reuse;
- supported extension;
- tool-assisted extension;
- unverified;
- unsupported.

Do not implement an unverified capability as though it were supported. Research it first.

## Legacy WebGL rule

`game/webgl/` is a legacy prototype/mechanics lab. It is not the shipping runtime.

Do not add a new standalone WebGL feature merely because it is easier than implementing the real mod feature. Use WebGL only for preservation, extracting existing design logic, or narrowly scoped prototyping that directly informs the mod.

## One-run contract

One autonomous pass must produce at most one small coherent increment. Examples:

- document one verified mod format;
- add one validator;
- create one minimal mod package component;
- implement one original quest/event;
- fix one packaging/compatibility bug.

Run the relevant checks before committing directly to `master`. Never create parallel branches unless explicitly requested.

## Legal/provenance constraint

Never commit proprietary base-game binaries/assets or third-party mod material without verified permission/license. Prefer original content and transformation/build tooling that operates against a legally installed copy of the game.

## Current target

Complete **M1 Modding Capability Audit**, then build the smallest installable `Children of Eltan` mod skeleton.
