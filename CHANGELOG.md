[Back to Home](README.md)

<img src="assets/GSOPs_horizontal_light.png" width="240" />

# Changelog

All notable changes to GSOPs are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/); versions match the
`gsop_release_vX.Y.Z.tox` build numbers. Formal changelog tracking begins at
**0.1.61** (2026-07-20) — earlier `0.1.x` patch releases predate this file and
are not itemized.

## [Unreleased]

### Changed
- **Minimum TouchDesigner version is now 2025.33060** (up from 2025.32820). Built
  and tested on the current official 2025 release.

## [0.1.61] — 2026-07-20

_Baseline entry — notable features present as of this release; formal changelog
tracking starts here._

### Added
- **Default splat on drop** — a freshly-dropped Splat Scene loads a TouchDesigner
  sample splat automatically, so you see content immediately instead of an empty op.
- **Automatic SPZ handling** — Splat Scene generators auto-detect `.spz` files.
- **FAQ page** in the docs.

### Changed
- **Release versioning** is now sourced from `gsop_config.json` (`family.version`)
  and can no longer regress or overwrite an existing release. (Internal/dev.)

### Fixed
- Release builds no longer surface harmless-but-confusing file-sync errors to users.
- External file reference bug on load.
