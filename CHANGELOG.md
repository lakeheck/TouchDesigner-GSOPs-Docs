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
- **Internal operators hidden from the OP Create menu.** `gsop_load_splat`,
  `gsop_particle_system`, and `gsop_control_panel` are embedded in the scene
  generators (`gsop_splat_scene` / `gsop_splat_scene_particles`) and are no
  longer offered as standalone drops in the TAB menu. They still ship in the
  family and update normally; reach them by diving into the scene component.

### Added
- **Splat Geo Equirectangular** (`gsop_splat_geo_equirectangular`) — renders the
  splat scene as a single-pass 360°×180° equirectangular panorama: the fast 360
  mode for immersive rooms, domes, sphere/skybox mapping, and 360 video.
  [Docs](operators/gsop_splat_geo_equirectangular.md).
- **Splat Geo Cubemap** (`gsop_splat_geo_cubemap`) — renders the splat scene as a
  cube map (six 90° faces in one Render TOP): the highest-quality 360 mode. Exact
  per-ray opacity evaluation (`RAY_EVAL 1`) means no seams between faces, no polar
  artifacts, and thin structures stay continuous; feeds Environment Lights directly
  or converts to equirectangular via a Projection TOP. ~1.3× the cost of classic
  evaluation, with a classic (EWA) fallback mode.
  [Docs](operators/gsop_splat_geo_cubemap.md).
- **Attribute Blur docs** (`gsop_attr_blur`) — documentation page for the
  Animation-group attribute blur operator, plus a new Animation section in the
  operator reference. [Docs](operators/gsop_attr_blur.md).
- **Example pages for the three new operators** — Attribute Blur, Cubemap Render,
  and Equirectangular Render each get a walkthrough with video and stills, plus
  matching `.tox` demos in `tox/examples/`. Listed in the
  [example index](examples/README.md).

### Fixed
- **Equirectangular render** — fixed a transposed Jacobian in the
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
- **New operators were missing from the OP Create menu.** `gsop_splat_geo_cubemap`,
  `gsop_splat_geo_equirectangular`, and `gsop_attr_blur` had complete entries in
  `gsop_config.json` but no generated sidecar manifest, so TDFam auto-discovered
  them into the "Other" group with default labels, no color, and no doc link. The
  release build now regenerates the sidecars itself (`BuildRelease` →
  `GenerateManifests`) before baking manifests into the `.tox`, so a newly added
  operator can no longer ship unregistered.
- **Operator versions no longer drift from the family version.** Nothing
  propagated `family.version` into the per-operator `op_version` during a
  TouchDesigner build, so every operator advertised `0.1.77` while the family had
  moved on — making TDFam's update comparison unreliable. The build now stamps
  both from a single writer shared by the TD build and `build_release.py`.
- **Manifest sync now reads the sidecar `.json` from disk** rather than the
  `manifest_src` DAT text. The DATs went stale between builds, and one was
  deliberately locked with its file path cleared to suppress a recurring import
  error — freezing its manifest permanently. Ops with no sidecar still fall back
  to the DAT.

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
