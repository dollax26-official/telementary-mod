# Fern

**A production-quality, highly configurable performance optimization framework for Minecraft 1.21.11. Makes Minecraft faster, not different.**

Fern ships every optimization with a safety class, a documented rationale, and
a live toggle - nothing is forced on you.

## Features

| What | How |
| --- | --- |
| Block entity frustum culling | Skips render-state work for block entities provably outside the camera frustum (with a configurable margin). |
| Server tick profiler allocation elimination | Removes per-entity per-tick lambda allocations when the in-game profiler is inactive. |
| Server TPS tracking | Real tick durations for accurate TPS / tick-time reporting. |
| Client frame-time tracking | FPS, 1% and 0.1% lows. |
| Memory / GC / allocation diagnostics | Heap, garbage collection, total allocated bytes. |
| Profilers | Built-in sampling and instrumented profilers. |
| Adaptive background scheduling | A bounded worker pool that yields to the game under pressure. |
| Live configuration | JSON5 config file, profile presets, in-game GUI, `/fern` command. |

## Safety model

| Class | Meaning |
| --- | --- |
| `SAFE` | Behaviorally identical to vanilla, only avoids wasted work. |
| `COMPATIBLE` | Same rendering/simulation result, may interact with other mods. |
| `EXPERIMENTAL` | May alter behavior; off by default (none ship in this release). |

If a conflicting optimization mod (such as Sodium) is detected, overlapping
rendering optimizations disable automatically.

## Installation

1. Requires **Minecraft 1.21.11**, **Fabric Loader 0.19.3+** and **Java 21+**.
2. Drop `Fern.jar` into your `mods/` folder.
3. Launch the game. A default `config/fern.json5` file is created on first run.

## Quick start

- `/fern status` - what is active and why.
- `/fern stats` - measured TPS, frame times, memory, GC, allocation.
- `/fern profile start 30` then `/fern profile report`.
- `/fern gui` - opens the in-game configuration screen.
- `/fern reload` - reload the config file from disk.

## Documentation

See the [README](https://github.com/ftbxx1/Fern#readme) and the
[docs](https://github.com/ftbxx1/Fern/tree/main/docs) folder.

## Links

- Source & releases: <https://github.com/ftbxx1/Fern>
- Issues: <https://github.com/ftbxx1/Fern/issues>
- License: MIT

Not affiliated with Mojang or Microsoft.
