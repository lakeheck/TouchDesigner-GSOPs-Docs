[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Splat Particles Scene

`gsop_splat_scene_particles` · IO · Generator

Usage is similar to `gsop_splat_scene`, with a few additions. It allows mixing between splats: set a Splat A Index and a Splat B Index, then use the Mix parameter to smoothly blend between them. When Blending Any to Any is on, the Mix parameter blends between the A and B splats. When it is off, a texture input determines the splat instead: the texture's 0-1 range is remapped to 0 to (number of splats loaded), and the texture value at each location determines which splat is rendered at that place on screen.

Splat Transform Mode bypasses all animation in the chain so you can visualize the splat itself -- most helpful when doing the initial transform and positioning of a splat.

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
| Blending Any to Any (`Blendinganytoany`) | When on, the Mix parameter blends between the A and B splats. When off, a texture input determines the splat. |
| Splat Transform Mode (`Splatxformmode`) | Bypasses all animation in the chain so you can visualize the splat itself. |
| Splat A Index (`A`) | The index of the "A" splat (the A side of the A/B mix). |
| Splat B Index (`B`) | The index of the "B" splat (the B side of the A/B mix). |
| Mix (`Mix`) | Smoothly mixes between the A and B splats. |
| Splats (`Splats`) | A list of sequential parameters that all share the fields below. |
| Gaussian splat PLY (`Splats0gaussiansplat`) | A direct reference to the splat PLY (or SPZ) file in your filesystem. |
| Reload (`Splats0reload`) | Reloads the file from disk. |
| SPZ (`Splats0spz`) | Toggle flagging whether the input file is SPZ or not. |
| T (`Splats0tx`, `Splats0ty`, `Splats0tz`) | Translate for this specific splat. |
| R (`Splats0rx`, `Splats0ry`, `Splats0rz`) | Rotate for this specific splat. |
| Uniform Scale (`Splats0scale`) | Applied to the splat as a uniform scale. |
| Cam Preset Index (`Splats0sequence`) | Scrubs through preset camera transforms. |

## Dynamics

| Parameter | Description |
|-----------|-------------|
| Scale Distance Threshold (`Scaledistancethreshold`) | Distance from home at which the splat becomes full scale. Generally 2-5. |
| Splat Size (`Splatsize`) | Global multiplier on splat size. Generally 1-2. |
| Scale from Disthome Strength (`Scalefromdisthomestrength`) | Additional scaling based on distance from home. |
| Global Turb (`Globalturb`) | Amplitude of turbulence applied to splats. |
| Turb Speed (`Turbspeed`) | How quickly the turbulence moves. |
| Turb Period (`Turbperiod`) | Period of the global turbulence. |
| Seek Home (`Seekhome`) | Weight of the force returning each splat to its home position. Generally around 2. |
| Vel Gain (`Velgain`) | Multiplier on splat velocity every frame. |
| Dampening (`Dampening`) | Inverse multiplier on velocity every frame. |
| Max Speed (`Maxspeed`) | Global max-speed constraint on the particle system. |

## Optimization

| Parameter | Description |
|-----------|-------------|
| Global Rotation and Scale (`Persplattransformrot`) | Apply global rotation and scale to all splats. |
| Master Splat Uniform Scale (`Mastersplatuniformscale`) | Overrides per-splat uniform scale when Global R&S is on. |
| Master Splat Rot (`Mastersplatrot1`, `Mastersplatrot2`, `Mastersplatrot3`) | Overrides per-splat rotation when Global R&S is on. |
| Lock Replicants (`Lockreplicants`) | Locks replicated splat networks for performance. |
| Enable Occlusion Bounding Box (`Bypass`) | Pre-bounding box applied before the particle system. |
| Bounding Type (`Type`) | Sphere or box. |
| Scale2 (`Scale2x`, `Scale2y`, `Scale2z`) | Scale of the bounding box. |
| Translate (`Translatex`, `Translatey`, `Translatez`) | Translation of the bounding box. |
| Rotate (`Rotatex`, `Rotatey`, `Rotatez`) | Rotation of the bounding box. |
