[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Frustum Delete

`gsop_frustum_delete` · Optimization · Filter

Deletes splats outside the camera frustum. Requires a reference to a `gsop_splat_scene` or `gsop_splat_scene_particles`. Place before `gsop_splat_geo` in your chain for best performance — culled splats never enter the render pipeline.

## Parameters

| Parameter | Description |
|-----------|-------------|
| Splat Scene (`Splatscene`) | Reference to the splat scene generator at the start of the chain. |
| Auto Populate Splat Scene COMP (`Autopopulatesplatscenecomp`) | Pulse to search backward through operator wiring to find and assign the Splat Scene automatically. |
