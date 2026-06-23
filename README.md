# GSOPs: Gaussian Splat Operators for TouchDesigner

Developed by [Lake Heckaman](https://www.lakeheckaman.com)

Custom operators for loading, editing, rendering, and animating 3D Gaussian Splats in TouchDesigner.

## Quick Start

<video src="examples/videos/gsops_quick_start.mp4" controls autoplay loop muted width="100%"></video>

0. Download the latest GSOPs release from **[patreon.com/collection/1565627](https://www.patreon.com/collection/1565627)**, unzip it and drop the .tox `gsop_release_vX.X.X` into your network
1. Drop a **GSOP Splat Scene** or **GSOP Splat Scene Particles** into your network
2. Set the splat file path parameter to your `.ply` or `.spz` file
3. Click **Init Splat Render Network** — auto-creates a Splat Geo, GSOP Splat Camera, and Render TOP
4. Done — you have a working render pipeline

---

## Installation

**Prerequisite:** TouchDesigner 2025.32820 or later (see Usage Notes below)

Download the latest release from **[patreon.com/collection/1565627](https://www.patreon.com/collection/1565627)**. The zip contains:

- `gsop_release_v{version}.tox` — drag-and-drop installer, all operators included
- `gsop_examples.toe` — example networks (bring your own splats)

GSOPs uses [TDFam](https://github.com/dotsimulate/TDFam) v1.0.1, a community framework for packaging custom operator families into TouchDesigner's TAB/OP Create menu (developed by Lyell Hintz / dotsimulate and Dan Molnar / Function Store).

1. Open your TouchDesigner project
2. Drag `gsop_release_v{version}.tox` into your network
3. GSOPs will appear as a new family in the TAB/OP Create dialog
4. I recommend you save this as a custom startup file by saving the .toe, then going to Edit > Preferences > Custom Startup File and pointing it to the .toe with GSOPs

To explore examples, open `gsop_examples.toe` separately.

### Usage Notes

1. Tested on Windows 11, Intel i9 14900, RTX 4090 24GB VRAM. Splats consume VRAM — save often.
2. Should work on macOS — please report issues (some feature limitations may apply).
3. Intended for use with a Commercial license for full features, but most operators work on Non-Commercial too.
4. When adding GSOPs, you might notice frame drops. These should be transitory and are due to VRAM re-allocation when dropping new operators.
5. Be careful as you develop. Gaussian splats and therefore GSOPs eat up VRAM, which can cause TD to crash. 
    - Monitor your VRAM usage with `nvidia-smi` in the terminal or using the "GPU" icon next to FPS in the TouchDesigner menu

## Architecture

Many GSOPs are view-dependent and require a Camera COMP reference. GSOPs solves this requirement with a `Splatscene` tag on the `gsop_splat_scene` or `gsop_splat_scene_particles` generator GSOPs. 

These `Splatscene` generators serve as the root for a render pipeline — normally you should only have one per renderTOP (you may still load in as many splats as possible via sequential parameters). It loads a splat file and holds camera/render references that propograte through the pipeline. 

Scene-dependent operators (like `gsop_frustum_delete`, `gsop_splat_geo`) must reference a `Splatscene` or they will throw errors. These operators all have a pulse parameter to auto-find a splat scene in the network (at the same level), but you can manually assign too via drag and drop.

**If you have any errors in rendering, first check that the `Splatscene` param references are all valid and correct**

## Examples

Pre-built example networks for common GSOPs workflows — with screenshots and videos.

**[Browse Examples →](examples/README.md)**

---

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

---

## License

Copyright (c) 2025-2026 Lake Heckaman. All rights reserved.

GSOPs is available via Patreon subscription at **[patreon.com/collection/1565627](https://www.patreon.com/collection/1565627)**:

| Tier | Who it's for |
|------|-------------|
| **Integrate** | Individual artists and freelancers — personal and commercial use |
| **Studio** | Studios and teams — commercial use across an organization |

No redistribution, reverse engineering, or sublicensing permitted. **[Full License →](license.md)**

## Third-Party Licenses

Deployed via [TDFam](https://github.com/dotsimulate/TDFam), an open-source TouchDesigner operator-family framework created by Lyell Hintz / dotsimulate and Dan Molnar / function.str. Licensed under the Apache License 2.0.
