[Back to Examples](README.md)

# Chroma Key

Use color to select which splats are rendered. You can try it out in the interactive viewer window of the example .tox.

<video src="videos/gsop_chroma_key.mp4" controls width="100%"></video>

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo` (×2 in this example)
4. renderTOP

## Process

1. Use the Chroma Key parameter to set the color, then use the Key Distance slider to apply. A Key Distance of 1 will have no effect, a Key Distance of 0 will show only splats matching the selected color exactly.

## Notes

Use the "Open Color Picker" pulse to open an interactive viewer where you can click around to select colors.

In this example, two `gsop_splat_geo` ops with different keys are used to toggle between two versions of the same splat.
