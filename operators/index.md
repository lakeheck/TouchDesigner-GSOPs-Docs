---
layout: default
title: Operators
nav_order: 2
has_children: true
---

# Operators

| Operator | Category | Type | Description |
|----------|----------|------|-------------|
| [Splat Scene](gsop_splat_scene.md) | IO | Generator | Loads a single splat file with camera and render pipeline |
| [Splat Particles Scene](gsop_splat_scene_particles.md) | IO | Generator | Loads multiple splats with particle system and blending |
| [Load Splat](gsop_load_splat.md) | IO | Generator | Loads a .ply or .spz file for the render pipeline |
| [Write Splat PLY](gsop_write_splat_ply.md) | IO | Generator | Writes splat to .ply file |
| [Bounding Box](gsop_bounding_box.md) | Edit | Filter | Constrains splats to a bounding region |
| [Convert to ParticleSystem](gsop_particle_system.md) | Edit | Filter | Converts splats into a particle system |
| [Frustum Delete](gsop_frustum_delete.md) | Optimization | Filter | Culls splats outside the camera frustum |
| [Thin Splat](gsop_thin_splat.md) | Optimization | Filter | Reduces point count by percentage |
| [Blowout](gsop_blowout.md) | Optimization | Filter | Adds space between splats |
| [Splat Geo](gsop_splat_geo.md) | Render | Filter | Generates renderable geometry with sorting and material |
| [Refractive](gsop_refractive.md) | Render | Filter | Refractive post-effect from POP geometry |
| [Control Panel](gsop_control_panel.md) | UI | Filter | HUD for working with GSOPs |
