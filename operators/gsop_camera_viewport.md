[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal.png" width="240" />

# Camera Viewport

`gsop_camera_viewport` · Render

A CameraViewport COMP pre-configured for Gaussian Splat rendering. When dropped into a network, it auto-detects a renderTOP on the same level and wires itself in as the active camera, automatically associating with the rest of the splat chain.

See the palette's cameraViewport docs for complete documentation: https://docs.derivative.ca/Palette:camera

## Presets

- **Wide FOV and aperture** — optimized for broad splat scene coverage
- **Very far `viewFarDist`** — prevents accidental occlusion of large splats that extend beyond typical camera clip ranges
- **WASD navigation** — keyboard movement enabled out of the box for quick scene exploration

## Parameters

| Parameter | Description |
|-----------|-------------|
| View Far Distance (`Viewfardist`) | Far clip plane. Set large by default to avoid clipping large splats. |
| FOV (`Fov`) | Field of view. Pre-set for wide coverage. |

## Usage

Drop into the same network level as your renderTOP. The operator auto-searches for a renderTOP at that level and sets itself as its camera — no manual wiring required. Can be replaced by any standard TD camera if preferred.
