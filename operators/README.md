[Back to Docs](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Operator Reference

| Category | Operators |
|----------|-----------|
| **IO** | [Splat Scene](#splat-scene), [Splat Scene Particles](#splat-scene-particles), [Load Splat](#load-splat), [Write Splat PLY](#write-splat-ply) |
| **Edit** | [Bounding Box](#bounding-box), [Convert to Particle System](#convert-to-particle-system) |
| **Optimization** | [Frustum Delete](#frustum-delete), [Thin Splat](#thin-splat), [Blowout](#blowout) |
| **Render** | [Splat Geo](#splat-geo), [Refractive](#refractive), [Splat Geo Equirectangular](#render), [Splat Geo Cubemap](#render) |
| **UI** | [Control Panel](#control-panel), [Camera Viewport](#camera-viewport) |

---

### IO

| Operator | Description |
|----------|-------------|
| [Splat Scene](gsop_splat_scene.md) | Loads a single splat file with camera and render pipeline |
| [Splat Scene Particles](gsop_splat_scene_particles.md) | Loads multiple splats with particle system and blending |
| [Load Splat](gsop_load_splat.md) | Loads a .ply or .spz file for the render pipeline |
| [Write Splat PLY](gsop_write_splat_ply.md) | Writes splat data to a .ply file |

### Edit

| Operator | Description |
|----------|-------------|
| [Bounding Box](gsop_bounding_box.md) | Constrains splats to a bounding region |
| [Convert to Particle System](gsop_particle_system.md) | Converts splats into a particle system |

### Optimization

| Operator | Description |
|----------|-------------|
| [Frustum Delete](gsop_frustum_delete.md) | Culls splats outside the camera frustum |
| [Thin Splat](gsop_thin_splat.md) | Reduces point count by percentage |
| [Blowout](gsop_blowout.md) | Adds space between splats |

### Render

| Operator | Description |
|----------|-------------|
| [Splat Geo](gsop_splat_geo.md) | Generates renderable geometry with sorting and material |
| [Refractive](gsop_refractive.md) | Refractive post-effect from POP geometry |
| [Splat Geo Equirectangular](gsop_splat_geo_equirectangular.md) | Single-pass 360° equirectangular render — the fast panorama mode |
| [Splat Geo Cubemap](gsop_splat_geo_cubemap.md) | Seam-free cube map render — the highest-quality 360° mode |

### UI

| Operator | Description |
|----------|-------------|
| [Control Panel](gsop_control_panel.md) | HUD for working with GSOPs |
| [Camera Viewport](gsop_camera_viewport.md) | Camera viewport overlay |
