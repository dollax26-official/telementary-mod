# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-08-09

### Added

- **Rendering**
  - Block entity frustum culling with a configurable safety margin
    (`rendering.blockEntityCulling`, `rendering.blockEntityCullMargin`).
  - Overlapping rendering optimizations auto-disable when a major optimization
    mod (e.g. Sodium) is detected (`compatibility.autoDisableConflicts`).
- **Ticking**
  - Elimination of per-entity per-tick lambda allocations in the server entity
    tick loop when the vanilla in-game profiler is inactive
    (`ticking.serverProfilerAllocations`).
- **Diagnostics**
  - Server TPS / tick-time tracking (`diagnostics.tpsTracking`).
  - Client frame-time tracking with FPS, 1% and 0.1% lows
    (`diagnostics.frameTimeTracking`).
  - Heap, GC and total-allocation reporting
    (`diagnostics.sampleIntervalMs`).
- **Profiling**
  - Instrumented `Profiler` and stack-sampling `SamplingProfiler` with
    `/fern profile start|stop|report`.
- **Scheduling**
  - Bounded, priority-ordered background worker pool with adaptive headroom
    backoff (`scheduling.adaptive`, `scheduling.backgroundWorkerCount`).
- **Configuration**
  - JSON5 config file with per-option documentation comments.
  - Profiles: `SAFE`, `BALANCED`, `PERFORMANCE`, `EXTREME`, `CUSTOM`.
  - In-game configuration screen (`/fern gui`).
  - `/fern status`, `stats`, `reload` server commands.
- **Compatibility**
  - Detects major optimization mods and reports them in `/fern status`.

### Notes

- No `EXPERIMENTAL` options ship in this release; the class exists for future use.
