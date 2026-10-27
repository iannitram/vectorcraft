# VectorCraft code map (our fork)

Ours, not upstream's. Built 2026-10-26 from the Cargo workspace (`crates/*`, `apps/*`, `xtask`) and each crate's `Cargo.toml` description; line counts are Rust lines on `main` that day. Upstream's own architecture notes: [`docs/architecture.md`](architecture.md) where present, and `AGENTS.md`. When a crate is added or split, update this table.

## Crates

| Path | What it owns | Uses (internal) | Platforms | Size |
|---|---|---|---|---|
| `crates/affinity` | Bounded reader for native Affinity documents: archive, object stream and document model | — | portable | ~6,974 |
| `crates/brush` | VectorCraft brushes: calligraphic, scatter, art, pattern and bristle brush definitions and stroke geometry | `color`, `doc`, `geom` | portable | ~3,133 |
| `crates/cad` | VectorCraft CAD interchange: a hand-written ASCII DXF writer (R12 to 2018) | `brush`, `color`, `doc`, `effects`, `geom`, `pathops`, `text` | portable | ~6,637 |
| `crates/color` | VectorCraft color | — | 2 file(s) with per-OS or wasm code | ~8,488 |
| `crates/doc` | VectorCraft document model: artboards, layers, objects, appearance (pure data + serde) | `color`, `geom` | 3 file(s) with per-OS or wasm code | ~27,887 |
| `crates/effects` | VectorCraft live effects evaluated to geometry | `color`, `doc`, `geom`, `pathops`, `plugins`, `text`, `three-d` | portable | ~21,708 |
| `crates/engine` | VectorCraft engine: sessions, history, selection, the command registry | `affinity`, `brush`, `cad`, `color`, `doc`, `eps`, `format`, `geom`, `metafile`, `pathops`, `pdf`, `plugins`, `render`, `scriptcheck`, `svg`, `testkit`, `text`, `tools`, `trace` | 29 file(s) with per-OS or wasm code | ~184,827 |
| `crates/eps` | VectorCraft Encapsulated PostScript: a hand-written EPS writer (PostScript Level 2 and 3) with TIFF previews | `brush`, `color`, `doc`, `effects`, `geom`, `metafile`, `pdf`, `render`, `testkit`, `text` | portable | ~28,448 |
| `crates/format` | VectorCraft native .vectorcraft format (versioned JSON, embedded images) | `doc`, `geom`, `testkit` | 2 file(s) with per-OS or wasm code | ~3,367 |
| `crates/geom` | VectorCraft geom | `testkit` | 1 file(s) with per-OS or wasm code | ~3,863 |
| `crates/mcp` | VectorCraft MCP server: JSON-RPC 2.0 over stdio, driving a running app or a headless session | `doc`, `engine`, `format`, `geom`, `render`, `svg`, `testkit`, `tools` | 1 file(s) with per-OS or wasm code | ~8,824 |
| `crates/metafile` | VectorCraft Windows metafiles: hand-written EMF and WMF writers and readers | `brush`, `color`, `doc`, `effects`, `geom`, `text` | portable | ~4,389 |
| `crates/pathops` | VectorCraft path operations: booleans (Pathfinder), shape builder regions, offset, outline stroke, simplify | `geom`, `testkit` | portable | ~7,277 |
| `crates/pdf` | VectorCraft PDF export and import | `brush`, `color`, `doc`, `effects`, `geom`, `testkit`, `text` | portable | ~27,321 |
| `crates/plugins` | Sandboxed WebAssembly plug-ins for VectorCraft: a resource-limited wasmi host for object filters and live effects | `color`, `doc`, `geom` | 2 file(s) with per-OS or wasm code | ~3,486 |
| `crates/render` | VectorCraft renderer: document to pixels (vello_cpu backend) | `brush`, `color`, `doc`, `effects`, `geom`, `plugins`, `testkit`, `text` | 4 file(s) with per-OS or wasm code | ~26,271 |
| `crates/scriptcheck` | Static checker for scripts written for the reference app: what a script uses, without running it | — | portable | ~6,159 |
| `crates/svg` | VectorCraft SVG import and export | `brush`, `color`, `doc`, `effects`, `geom`, `testkit`, `text` | 2 file(s) with per-OS or wasm code | ~16,697 |
| `crates/testkit` | VectorCraft test helpers: fixtures, generators, render comparison, geometry assertions | `color`, `doc`, `engine`, `format`, `geom`, `render`, `svg` | 1 file(s) with per-OS or wasm code | ~2,194 |
| `crates/text` | VectorCraft text: font database, shaping, layout, glyph outlines | `doc`, `geom` | 6 file(s) with per-OS or wasm code | ~22,146 |
| `crates/three-d` | Portable 3D effect geometry (revolve, extrude and bevel, inflate, rotate) and projected vector shading | `geom`, `pathops` | portable | ~4,664 |
| `crates/tools` | VectorCraft tool state machines: pointer events in, commands and overlays out | `color`, `doc`, `effects`, `geom`, `pathops`, `text` | 2 file(s) with per-OS or wasm code | ~40,755 |
| `crates/trace` | VectorCraft Image Trace: raster to vector tracing (quantize, boundary follow, polygon, Bezier fit) | `geom` | 1 file(s) with per-OS or wasm code | ~16,314 |
| `crates/ui-egui` | VectorCraft egui frontend (menus, panels, tools and canvas); swappable — nothing below depends on it | `brush`, `cad`, `color`, `doc`, `effects`, `engine`, `eps`, `format`, `geom`, `pdf`, `plugins`, `render`, `svg`, `testkit`, `text`, `three-d`, `tools` | 35 file(s) with per-OS or wasm code | ~155,853 |
| `apps/vectorcraft` | (no description in Cargo.toml) | `engine`, `text`, `ui-egui` | 13 file(s) with per-OS or wasm code | ~10,511 |
| `apps/vectorcraft-cli` | VectorCraft command line: MCP server (stdio) and headless batch runs | `color`, `doc`, `engine`, `format`, `geom`, `mcp`, `render`, `svg`, `testkit`, `text` | 3 file(s) with per-OS or wasm code | ~2,378 |
| `apps/vectorcraft-web` | VectorCraft in the browser (eframe web runner, WebGPU with WebGL2 fallback) | `engine`, `format`, `text`, `ui-egui` | 3 file(s) with per-OS or wasm code | ~1,824 |
| `xtask` | Build and check tasks (`cargo xtask ci`, parity reports) | — | portable | — |

## How they interlink

The engine owns the session, undo and the command registry; every user action is a command. The `ui-egui` front end sits on top and is swappable: nothing below it depends on it. The desktop, CLI and web apps are thin shells over the engine and the front end. The MCP crate drives the engine headless or through the running app.

- `affinity` is used by `engine`.
- `brush` is used by `cad`, `engine`, `eps`, `metafile`, `pdf`, `render`, `svg`, `ui-egui`.
- `cad` is used by `engine`, `ui-egui`.
- `color` is used by `brush`, `cad`, `doc`, `effects`, `engine`, `eps`, `metafile`, `pdf`, `plugins`, `render`, `svg`, `testkit`, `tools`, `ui-egui`, `vectorcraft-cli`.
- `doc` is used by `brush`, `cad`, `effects`, `engine`, `eps`, `format`, `mcp`, `metafile`, `pdf`, `plugins`, `render`, `svg`, `testkit`, `text`, `tools`, `ui-egui`, `vectorcraft-cli`.
- `effects` is used by `cad`, `eps`, `metafile`, `pdf`, `render`, `svg`, `tools`, `ui-egui`.
- `engine` is used by `mcp`, `testkit`, `ui-egui`, `vectorcraft`, `vectorcraft-cli`, `vectorcraft-web`.
- `eps` is used by `engine`, `ui-egui`.
- `format` is used by `engine`, `mcp`, `testkit`, `ui-egui`, `vectorcraft-cli`, `vectorcraft-web`.
- `geom` is used by `brush`, `cad`, `doc`, `effects`, `engine`, `eps`, `format`, `mcp`, `metafile`, `pathops`, `pdf`, `plugins`, `render`, `svg`, `testkit`, `text`, `three-d`, `tools`, `trace`, `ui-egui`, `vectorcraft-cli`.
- `mcp` is used by `vectorcraft-cli`.
- `metafile` is used by `engine`, `eps`.
- `pathops` is used by `cad`, `effects`, `engine`, `three-d`, `tools`.
- `pdf` is used by `engine`, `eps`, `ui-egui`.
- `plugins` is used by `effects`, `engine`, `render`, `ui-egui`.
- `render` is used by `engine`, `eps`, `mcp`, `testkit`, `ui-egui`, `vectorcraft-cli`.
- `scriptcheck` is used by `engine`.
- `svg` is used by `engine`, `mcp`, `testkit`, `ui-egui`, `vectorcraft-cli`.
- `testkit` is used by `engine`, `eps`, `format`, `geom`, `mcp`, `pathops`, `pdf`, `render`, `svg`, `ui-egui`, `vectorcraft-cli`.
- `text` is used by `cad`, `effects`, `engine`, `eps`, `metafile`, `pdf`, `render`, `svg`, `tools`, `ui-egui`, `vectorcraft`, `vectorcraft-cli`, `vectorcraft-web`.
- `three-d` is used by `effects`, `ui-egui`.
- `tools` is used by `engine`, `mcp`, `ui-egui`.
- `trace` is used by `engine`.
- `ui-egui` is used by `vectorcraft`, `vectorcraft-web`.

## Mac, PC and Linux (R04)

- Ships for macOS, Windows and Linux (plus FreeBSD and the web) from upstream's release workflow.
- Per-OS code sits mostly in the engine, the `ui-egui` front end and the desktop app (the "Platforms" column counts files with `cfg(target_os…)`, `cfg(windows|unix)` or wasm code). Everything else is portable Rust.
- Upstream CI (`ci.yml`) calls `storytold/craft-common-actions` `gate.yml` with its default `os` input, `["ubuntu-24.04"]`: pull requests are tested on Linux only. Release, FreeBSD, Nix, print, Windows ARM64 and Windows 7 have their own workflows.
- A build issue that touches per-OS code carries a `platform:*` label and says which OS it was built and checked on.
