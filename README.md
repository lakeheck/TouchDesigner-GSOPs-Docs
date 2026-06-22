# GSOPs: Gaussian Splat Operators for TouchDesigner

Developed by [Lake Heckaman](https://www.lakeheckaman.com)

Custom operators for loading, editing, rendering, and animating 3D Gaussian Splats in TouchDesigner.

## Installation

**ALPHA TESTING PACKAGE**: https://www.dropbox.com/scl/fo/mw9tx22jrwx23072ipn5f/AH8I_rzrkiDOZn1DHB1Ylx8?rlkey=17hvywd6u6m2s4p7lmj1kzicw&dl=0
- `tox/GSOPs`: folder with all operators and TDFam manifests
- `gsops.toe`: example network file (bring your own splats)
- `TDFam_create`: Drop this into any TD project and make sure the path points to the GSOP download location (probably c/p into the project directory for now)

GSOPs uses [TDFam](https://github.com/dotsimulate/TDFam) v1.0.1, a community framework for packaging custom operator families into TouchDesigner's TAB/OP Create menu (developed by Lyell Hintz / dotsimulate and Dan Molnar / Function Store).

1. Open your TouchDesigner project
2. Place the `TDFam_create.tox` component from `TDFam-1.0.1/`
3. Set the family's `Opfolder` parameter to point at the `tox/GSOP/` directory (or wherever you have it downloaded, if the relative path is different)
4. Toggle `Install` on — GSOPs will appear as a new family in the OP Create dialog

### Usage Notes

1. Tested on Windows 11, Intel i9 14900, RTX 4090 24GB VRAM. Splats consume VRAM — save often.
2. Should work on macOS — please report issues (some feature limitations may apply).
3. Intended for use with a Commercial license for full features, but most operators work on Non-Commercial too.
4. When adding GSOPs, you might notice frame drops. These should be transitory and are due to VRAM re-allocation when dropping new operators.

## Architecture

Many GSOPs are view-dependent and require a Camera COMP reference. All operators in a single splat render setup should reference the same Camera COMP.

`gsop_splat_scene` serves as the root for a render pipeline — it loads a splat file and holds camera/render references. Scene-dependent operators (like `gsop_frustum_delete`, `gsop_splat_geo`) reference it for camera data.

## Operator Categories

| Category | Description |
|----------|-------------|
| **IO** | Load and save splat files (PLY/SPZ formats) |
| **Edit** | Spatial modifications — bounding boxes, region constraints |
| **Optimization** | Performance operators — frustum culling, thinning, blowout |
| **Animation** | Particle systems, splat blending, dynamics |
| **Render** | Geometry generation, materials, post-effects |
| **UI** | Control panels and HUDs |

## Operators

### IO

| Operator | Type | Description |
|----------|------|-------------|
| [Splat Scene](operators/gsop_splat_scene.md) | Generator | Loads a single splat file with camera and render pipeline |
| [Splat Particles Scene](operators/gsop_splat_scene_particles.md) | Generator | Loads multiple splats with particle system and blending |
| [Load Splat](operators/gsop_load_splat.md) | Generator | Loads a .ply or .spz file for the render pipeline |
| [Write Splat PLY](operators/gsop_write_splat_ply.md) | Generator | Writes splat to .ply file |

### Edit

| Operator | Type | Description |
|----------|------|-------------|
| [Bounding Box](operators/gsop_bounding_box.md) | Filter | Constrains splats to a bounding region |
| [Convert to ParticleSystem](operators/gsop_particle_system.md) | Filter | Converts splats into a particle system |

### Optimization

| Operator | Type | Description |
|----------|------|-------------|
| [Frustum Delete](operators/gsop_frustum_delete.md) | Filter | Culls splats outside the camera frustum |
| [Thin Splat](operators/gsop_thin_splat.md) | Filter | Reduces point count by percentage |
| [Blowout](operators/gsop_blowout.md) | Filter | Adds space between splats |

### Render

| Operator | Type | Description |
|----------|------|-------------|
| [Splat Geo](operators/gsop_splat_geo.md) | Filter | Generates renderable geometry with sorting and material |
| [Refractive](operators/gsop_refractive.md) | Filter | Refractive post-effect from POP geometry |

### UI

| Operator | Type | Description |
|----------|------|-------------|
| [Control Panel](operators/gsop_control_panel.md) | Filter | HUD for working with GSOPs |

## Examples

Pre-built example networks for common GSOPs workflows — with screenshots and videos.

**[Browse Examples →](examples/README.md)**

---

## License

Copyright (c) 2025-2026 Lake Heckaman. All rights reserved.

GSOPs is available via Patreon subscription at **[patreon.com/lakeheckaman](https://patreon.com/lakeheckaman)**:

| Tier | Who it's for |
|------|-------------|
| **Integrate** | Individual artists and freelancers — personal and commercial use |
| **Studio** | Studios and teams — commercial use across an organization |

No redistribution, reverse engineering, or sublicensing permitted. **[Full License →](license.md)**

## Third-Party Licenses

Deployed via [TDFam](https://github.com/dotsimulate/TDFam), an open-source TouchDesigner operator-family framework created by Lyell Hintz / dotsimulate and Dan Molnar / function.str. Licensed under the Apache License 2.0.
