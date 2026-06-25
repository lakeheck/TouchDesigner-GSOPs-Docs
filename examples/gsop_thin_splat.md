[Back to Examples](README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Thin Splat Optimization

Easily reduce the splat count to improve render optimization.

<video src="videos/gsop_thin_splat_example.mp4" controls width="100%"></video>

<a href="videos/gsop_thin_splat_example.mp4" target="_blank">↗ Open video in new tab</a>

![Thin Splat Optimization](images/gsop_thin_splat_example.png)

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo`
4. renderTOP
5. `gsop_thin_splat`

## Process

1. Add the `gsop_thin_splat` operator between the `gsop_splat_scene` and `gsop_splat_geo` to use a slider to reduce splats by X pct

## Notes

Often helpful to engage when you are switching between scenes and want the splat to be much more lightweight while it is 'in the background'.
