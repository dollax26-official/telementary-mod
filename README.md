# Fern

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Paper](https://img.shields.io/badge/Fabric-1.21.11-orange.svg)](#requirements)
[![Java](https://img.shields.io/badge/Java-21-blue.svg)](#requirements)
[![Build](https://github.com/ftbxx1/Fern/actions/workflows/build.yml/badge.svg)](https://github.com/ftbxx1/Fern/actions/workflows/build.yml)

A production-quality, highly configurable performance optimization framework for
Minecraft 1.21.11 on Fabric. Every optimization ships with a safety class, a
documented rationale, and a live toggle — nothing is forced on you.

> **Motto: makes Minecraft faster, not different.**

## Features

- **Block entity frustum culling** — skips render-state work for block entities
  provably outside the camera frustum (with a configurable margin). Every
  potentially-visible block entity still renders.
- **Server tick profiler allocation elimination** — removes per-entity, per-tick
  lambda allocations in the server entity tick loop when the vanilla in-game
  profiler is inactive. Identical behavior, less garbage.
- **Server TPS tracking** — measures real server tick durations for accurate
  TPS / tick-time reporting (measurement only, never changes simulation).
- **Client frame-time tracking** — records frame durations and computes FPS,
  1% and 0.1% lows.
- **Memory / GC / allocation diagnostics** — heap, garbage collection, and
  total allocated bytes since start.
- **Built-in sampling and instrumented profilers** with `/fern
  profile start/stop/report`.
- **Adaptive background scheduling** — a bounded, priority-ordered worker pool
  that yields to the game when it is under frame/tick pressure.
- **Live configuration** — JSON5 config file, profile presets, an in-game GUI,
  and a `/fern` command. Mixins read settings live, so toggles apply
  without restarting.

## Requirements

- Minecraft **1.21.11**
- Fabric Loader **>= 0.19.3**
- Fabric API (the command API is used; the whole API is a hard dependency)
- Java **21**

## Installation

1. Install the Fabric Loader for Minecraft 1.21.11.
2. Drop `fern-0.1.0.jar` into your `mods` folder.
3. Launch the game. A default `config/fern.json5` file is created on
   first run.

## Quick start

- `/fern status` — what is active and why.
- `/fern stats` — measured TPS, frame times, memory, GC, allocation.
- `/fern profile start 30` then `/fern profile report`.
- `/fern gui` (client) or open the config screen via the mod settings
  entry if your mod menu provider exposes it.
- `/fern reload` — reload the config file from disk.

See [docs/COMMANDS.md](docs/COMMANDS.md) for full command reference and
[docs/CONFIGURATION.md](docs/CONFIGURATION.md) for every option and profile.

## Configuration

The config file lives at `config/fern.json5`. It is written once on
first run with per-option comments and is round-trippable (safe to hand-edit).
See [docs/CONFIGURATION.md](docs/CONFIGURATION.md).

## Safety model

Every optimization is classified:

| Class | Meaning |
| --- | --- |
| `SAFE` | Behaviorally identical to vanilla, only avoids wasted work. |
| `COMPATIBLE` | Same rendering/simulation result, may interact with other mods. |
| `EXPERIMENTAL` | May alter behavior; off by default (none ship in this release). |

If a conflicting optimization mod (such as Sodium) is detected and
`compatibility.autoDisableConflicts` is enabled (default), this mod
disables its overlapping rendering optimizations automatically. See
[docs/COMPATIBILITY.md](docs/COMPATIBILITY.md).

## Building

```sh
./gradlew build
```

The mod jar is produced at `build/libs/fern-<version>.jar`.

## License

MIT — see [LICENSE](LICENSE).
