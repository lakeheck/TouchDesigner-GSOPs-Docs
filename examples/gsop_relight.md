[Back to Examples](README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Relighting

Use TouchDesigner LightCOMPs with your splat.

<video src="videos/gsop_relight.mp4" controls width="100%"></video>

<a href="videos/gsop_relight.mp4" target="_blank">↗ Open video in new tab</a>

![Relighting](images/gsop_relight.png)

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo`
4. renderTOP

## Process

1. Drop the operators into your network - you will note the camera and `gsop_splat_geo` auto-find their respective renderTOP and splat scene components
2. Point `gsop_splat_scene` to a `.ply` or `.spz` file
3. Open the GUI on `gsop_splat_scene` and use the camera positioning window to orient the splat
4. Add more splats to the scene if desired using the sequential parameters and follow the same process to pre-transform each
5. Toggle on the 'Use TD Lighting' parameter on the `gsop_splat_geo` component
