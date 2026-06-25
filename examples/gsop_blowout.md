[Back to Examples](README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Blowout Optimization

Add space between splats to reduce overlapping geometry in render and improve efficiency.

<video src="videos/gsop_blowout.mp4" controls width="100%"></video>

<a href="videos/gsop_blowout.mp4" target="_blank">↗ Open video in new tab</a>

![Blowout Optimization](images/gsop_blowout.png)

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo`
4. renderTOP
5. `gsop_blowout`

## Process

1. Add the `gsop_blowout` operator between the `gsop_splat_scene` and `gsop_splat_geo` to use a slider to increase blowout

## Notes

Often helpful to engage when you are switching between scenes and want the splat to be much more lightweight while it is 'in the background'.

Useful in combination with `gsop_thin_splat`.
