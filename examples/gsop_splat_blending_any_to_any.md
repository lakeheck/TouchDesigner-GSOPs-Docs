[Back to Examples](README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Particles Scene Blending Any to Any

Load multiple splats and blend from any to any in real time.

<video src="videos/gsop_splat_blending_any_to_any.mp4" controls width="100%"></video>

<a href="videos/gsop_splat_blending_any_to_any.mp4" target="_blank">↗ Open video in new tab</a>

![Particles Scene Blending Any to Any](images/gsop_splat_blending_any_to_any.png)

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene_particles`
3. `gsop_splat_geo`
4. renderTOP

## Process

1. Drop the operators into your network - you will note the camera and `gsop_splat_geo` auto-find their respective renderTOP and splat scene components
2. Point `gsop_splat_scene_particles` to a `.ply` or `.spz` file
3. Open the GUI on `gsop_splat_scene_particles` and use the camera positioning window to orient the splat
4. Add more splats to the scene using the sequential parameters and follow the same process to pre-transform each
5. Use the Splat Index A and B parameters with the Mix parameter to switch between splats
