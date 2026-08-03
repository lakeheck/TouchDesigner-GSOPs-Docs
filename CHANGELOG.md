[Back to Home](README.md)

<img src="assets/GSOPs_horizontal_light.png" width="240" />

# Changelog

All notable changes to GSOPs are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/); versions match the
`gsop_release_vX.Y.Z.tox` build numbers. Formal changelog tracking begins at
**0.1.61** (2026-07-20) — earlier `0.1.x` patch releases predate this file and
are not itemized.

## [Unreleased]

### Added
- **Cubemap splat rendering (in development)** — new
  `dat/GS_MATERIAL/glsl_vert_frag_cubemap_render.glsl`: renders splats as six 90°
  perspective faces (TD Render TOP cube-map mode), reprojectable to equirectangular
  via a Projection TOP. Uses **ray-space evaluation** (`RAY_EVAL 1`): fragment alpha
  is the exact peak density of the 3D Gaussian along each pixel's ray, so adjacent
  faces agree by construction — no face-boundary seams, no polar artifacts, and
  thin structures (wires) stay continuous. Includes ray-space antialiasing
  (0.3 px² world-equivalent dilation) and conservative quad sizing for close splats.
  Shares the radial far-to-near sort with the equirect path.

### Fixed
- **Equirectangular render (WIP operator)** — fixed a transposed Jacobian in the
  equirect covariance projection. The bug compressed splat footprints into thin
  vertical slivers away from the view center, causing comb striping at the poles,
  vertical "curtain" smearing of close-range splats, and general degradation
  outside the forward direction. With the correct layout the polar alpha-fade
  workaround became unnecessary and was removed — near-pole splats now stretch
  into their true wide equirect footprints and cover the zenith/nadir naturally.
- **Equirectangular render sorting** — the splat sort used the sort POP's
  "object" mode, which orders along the camera's view axis, inverting the
  composite order for everything behind the camera (rear hemisphere rendered as
  a milky wash). Switched to proximity sort on the camera's world position
  (expression-driven from the splat scene's Camera matrix CHOP), reversed for
  back-to-front painter's order. The full 360° now renders uniformly sharp
  regardless of camera orientation.

## [0.1.70] — 2026-07-20

Bug fixes and quality-of-life improvements.

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

### Fixed
- Release builds no longer surface harmless-but-confusing file-sync errors to users.
- External file reference bug on load.
