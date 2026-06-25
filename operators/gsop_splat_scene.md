[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal.png" width="240" />

# Splat Scene

`gsop_splat_scene` · IO · Generator

`gsop_splat_scene` is a generator. It loads in a single splat file with an associated camera and render pipeline. Sequential parameters allow you to load in multiple splats and switch through them smoothly and easily. You can load SPZ or PLY files using the toggle flag.

Splats are loaded via the sequential parameters. Inside `gsop_splat_scene` there is a `gsop_load_splat` for every splat loaded in. Inside each `gsop_load_splat` you can use the XForm cam to set the transforms applied to that splat as a pre-transform — like adjusting a camera, but a bit easier. You can also add sequential camera presets that you scrub through with the Cam Preset Index parameter. This is a static load: it loads the splat only.

## Gaussian Splat

| Parameter | Description |
|-----------|-------------|
| Render TOP (`Rendertop`) | A reference to the Render TOP that is being used to render the Gaussian splat. |
| Camera (`Camera`) | Read-only. Auto-filled based on the Render TOP selected. |
| Init Splat Render Network (`Initsplatrendernetwork`) | Pulse to auto-create the rest of the render pipeline — `gsop_splat_geo`, a `gsop_camera_viewport`, and a Render TOP — wired and ready to go. |
| Open GUI (`Opengui`) | Opens the positioning and camera GUI for this operator. |
| Resetpulse (`Resetpulse`) | Master reset for the operator. |
| Recreate All Operators (`Recreateall`) | Pulses the "recreate all" option on the replicator that loads each splat file. |
| Reset Parameters to Default (`Resetparameterstodefault`) | Currently has no effect for this operator. |
| Splat Index (`A`) | The index selected from the sequential parameters you set up. |
| Splats (`Splats`) | A list of sequential parameters that all share the fields below. |
| Gaussian splat PLY (`Splats0gaussiansplat`) | A direct reference to the splat PLY (or SPZ) file in your filesystem. |
| Reload (`Splats0reload`) | Reloads the file from disk. |
| SPZ (`Splats0spz`) | Toggle flagging whether the input file is SPZ or not. |
| T (`Splats0tx`, `Splats0ty`, `Splats0tz`) | Translate for this specific splat. Auto-set if you use the camera to position your splat, or adjust manually. |
| R (`Splats0rx`, `Splats0ry`, `Splats0rz`) | Rotate for this specific splat. Auto-set if you use the camera to position your splat, or adjust manually. |
| Uniform Scale (`Splats0scale`) | Applied to the splat as a uniform scale. |
| Cam Preset Index (`Splats0sequence`) | If preset camera transforms are defined for your splat, this parameter scrubs through them. |

## Optimization

| Parameter | Description |
|-----------|-------------|
| Global Rotation and Scale (`Persplattransformrot`) | When enabled, a global rotation and scale is applied to all splats loaded in this component. |
| Master Splat Uniform Scale (`Mastersplatuniformscale`) | Only enabled if Global Rotation and Scale is on. Overrides any uniform scale applied to the specific splat. |
| Master Splat Rot (`Mastersplatrot1`, `Mastersplatrot2`, `Mastersplatrot3`) | Only enabled if Global Rotation and Scale is on. Overrides any rotation applied to the specific splat. |
| Lock Replicants (`Lockreplicants`) | Locks the replicated splat networks inside this component after they are created. |
