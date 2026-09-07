# Children of Eltan — Mod Architecture

## Status

This document is the canonical technical architecture for the project after the transition from standalone KR3/WebGL development to a **Space Rangers 2 / Space Rangers HD mod-first project**.

If an older document says that `game/webgl/` is the canonical shipping runtime, this document supersedes that technical statement.

## Product definition

**Shipping target:** an installable mod for Space Rangers 2 / Space Rangers HD named **«Дети Эльтана» / Children of Eltan**.

**Base runtime:** the installed original game.

**Repository responsibility:** original mod content, data, scripts, tooling, documentation, validation and packaging that can be legally distributed.

## Core architecture

```text
SR2 / SRHD installation
    ├─ original engine and executable
    ├─ original game systems
    └─ supported mod loading path
             ↓
Children of Eltan mod package
    ├─ manifest / metadata
    ├─ quests and text adventures
    ├─ scriptable events
    ├─ original data overrides/additions
    ├─ balance/equipment additions
    ├─ story and faction content
    ├─ optional original media
    └─ compatibility metadata
             ↓
Repository tooling
    ├─ validate source data
    ├─ build/package mod
    ├─ detect missing dependencies
    ├─ produce reproducible release archive
    └─ smoke-test install layout
```

## Canonical directories — target state

The repository may migrate gradually toward this layout:

```text
mod/
  children_of_eltan/
    manifest/
    data/
    quests/
    scripts/
    text/
    media/
    compatibility/

tools/
  build/
  validate/
  convert/

docs/
  MOD_ARCHITECTURE.md
  ROADMAP.md
  MODDING_RESEARCH.md
  compatibility/

legacy/
  webgl/              # eventual archival destination, only after a deliberate migration
```

Until migration is complete, existing `quests/`, `data/`, `scripts/` and `game/webgl/` remain where they are. Do not perform a destructive mass move merely to match this diagram.

## Legacy WebGL policy

`game/webgl/` is now a **legacy prototype and mechanics laboratory**.

It may be used to:

- inspect already-designed mechanics;
- prototype original systems before expressing them in a KR2-compatible form;
- recover balancing ideas, UI flows, race/class logic and narrative structure;
- preserve project history.

It must not be treated as:

- the main release target;
- evidence that a feature exists in the KR2 mod;
- a reason to reimplement a base-game KR2 mechanic from scratch;
- the default destination for autonomous development.

No deletion of the WebGL tree is authorized by this architecture.

## Modding evidence rule

Before implementing any feature, classify it:

1. **Native reuse** — KR2 already provides the mechanic; mod only supplies content/data.
2. **Supported extension** — documented mod format/script path can extend it.
3. **Tool-assisted extension** — requires a known external editor/loader/toolchain.
4. **Unverified** — technically plausible but not yet confirmed.
5. **Unsupported** — not achievable through the accepted modding path without binary patching or prohibited redistribution.

Only categories 1–3 should normally lead directly to implementation. Category 4 requires research first. Category 5 requires design adaptation rather than pretending the capability exists.

## Provenance and legal boundary

The repository must contain only material we can legitimately distribute.

Allowed by default:

- original code and tooling created for this project;
- original quests, text, lore, balance data and art;
- metadata describing how to install against a legally obtained base game;
- patches or transformations that do not redistribute protected original assets, where legally and technically appropriate.

Do not vendor:

- proprietary KR2 binaries;
- extracted protected art/music/text from the base game;
- code/assets from third-party mods without a compatible license or explicit permission.

External modding repositories may be used as technical evidence, but their code/assets must not be copied unless licensing is verified.

## Build philosophy

The future production build should be reproducible from repository-owned source files and produce a clean mod package without bundling the original game.

Preferred eventual command shape:

```bash
python tools/build/build_mod.py
python tools/validate/validate_mod.py dist/children-of-eltan
```

The exact commands are intentionally not locked until the real SR2/SRHD modding toolchain is confirmed.

## Migration order

### M0 — Concept reset

- reframe README and roadmap;
- define mod architecture;
- stop autonomous WebGL expansion;
- preserve all legacy work.

### M1 — Modding capability audit

Document:

- target base-game edition/version;
- supported mod directories/formats;
- quest/text-adventure formats;
- data/config override mechanisms;
- script/event capabilities;
- packaging/install procedure;
- compatibility with common community mod frameworks;
- licensing constraints of any required tooling.

### M2 — Minimal mod skeleton

Create the smallest installable Children of Eltan package that changes one safe, reversible, original piece of content and can be removed cleanly.

### M3 — First vertical slice

Prefer one meaningful original slice, for example:

- a Children of Eltan text quest;
- a new event chain;
- an original equipment/content entry;
- a small narrative arc tied to existing KR2 sandbox systems.

### M4 — Systemic campaign expansion

Only after the skeleton and validation path are stable, expand toward the larger story, diplomacy, faction consequences and late-game conflict.

## Autonomous agent rules

Every agent must:

1. read this document before changing game architecture;
2. inspect current `master` and recent commits;
3. verify the intended capability against real KR2/SRHD modding evidence;
4. prefer native engine reuse over reimplementation;
5. make one coherent increment;
6. keep changes reversible;
7. test/validate using the current mod toolchain;
8. never silently revive standalone WebGL as the shipping target.

## Definition of Done

A mod feature is done only when:

- it exists in the actual mod source/package, not merely the legacy WebGL prototype;
- the relevant mod format validates;
- install/package layout is correct;
- it is compatible with the declared target base-game version;
- required third-party tools/dependencies are documented;
- the documentation does not overstate runtime verification.

## Current next step

Perform the **M1 Modding Capability Audit** and then create the minimal installable mod skeleton. Until that is complete, major new standalone game systems are out of scope.
