---
layout: default
title: GSOPs Documentation
---

# GSOPs: Gaussian Splat Operators for TouchDesigner

Developed by [Lake Heckaman](https://www.lakeheckaman.com)

Custom operators for loading, editing, rendering, and animating 3D Gaussian Splats in TouchDesigner.

## Installation

GSOPs uses [TDFam](https://github.com/dotsimulate/TDFam) v1.0.1, a community framework for packaging custom operator families into TouchDesigner's TAB/OP Create menu (developed by Lyell Hintz / dotsimulate and Dan Molnar / Function Store).

1. Open your TouchDesigner project
2. Place the `TDFam_create.tox` component from `TDFam-1.0.1/`
3. Set the family's `Opfolder` parameter to point at the `tox/GSOP/` directory
4. Toggle `Install` on — GSOPs will appear as a new family in the OP Create dialog

### Usage Notes

1. Tested on Windows 11, Intel i9 14900, RTX 4090 24GB VRAM. Splats consume VRAM — save often.
2. Should work on macOS — please report issues (some feature limitations may apply).
3. Intended for use with a Commercial license for full features, but most operators work on Non-Commercial too.
4. When adding GSOPs, you might notice frame drops. These should be transitory and are due to VRAM re-allocation when dropping new operators.

## Architecture

Many GSOPs are view-dependent and require a Camera COMP reference. All operators in a single splat render setup should reference the same Camera COMP.

`gsop_splat_scene` serves as the root for a render pipeline — it loads a splat file and holds camera/render references. Scene-dependent operators (like `gsop_frustum_delete`, `gsop_splat_geo`) reference it for camera data.

## Operator Categories

| Category | Description |
|----------|-------------|
| **IO** | Load and save splat files (PLY/SPZ formats) |
| **Edit** | Spatial modifications — bounding boxes, region constraints |
| **Optimization** | Performance operators — frustum culling, thinning, blowout |
| **Animation** | Particle systems, splat blending, dynamics |
| **Render** | Geometry generation, materials, post-effects |
| **UI** | Control panels and HUDs |

## Operators

| Operator | Category | Type | Description |
|----------|----------|------|-------------|
| [Splat Scene](#gsop_splat_scene) | IO | Generator | Loads a single splat file with camera and render pipeline |
| [Splat Particles Scene](#gsop_splat_scene_particles) | IO | Generator | Loads multiple splats with particle system and blending |
| [Load Splat](#gsop_load_splat) | IO | Generator | Loads a .ply or .spz file for the render pipeline |
| [Write Splat PLY](#gsop_write_splat_ply) | IO | Generator | Writes splat to .ply file |
| [Bounding Box](#gsop_bounding_box) | Edit | Filter | Constrains splats to a bounding region |
| [Convert to ParticleSystem](#gsop_particle_system) | Edit | Filter | Converts splats into a particle system |
| [Frustum Delete](#gsop_frustum_delete) | Optimization | Filter | Culls splats outside the camera frustum |
| [Thin Splat](#gsop_thin_splat) | Optimization | Filter | Reduces point count by percentage |
| [Blowout](#gsop_blowout) | Optimization | Filter | Adds space between splats |
| [Splat Geo](#gsop_splat_geo) | Render | Filter | Generates renderable geometry with sorting and material |
| [Refractive](#gsop_refractive) | Render | Filter | Refractive post-effect from POP geometry |
| [Control Panel](#gsop_control_panel) | UI | Filter | HUD for working with GSOPs |

---

## Operator Reference

### gsop_splat_scene

**Splat Scene** · IO · Generator

`gsop_splat_scene` is a generator. It loads in a single splat file with an associated camera and render pipeline. Sequential parameters allow you to load in multiple splats and switch through them smoothly and easily. You can load SPZ or PLY files using the toggle flag.

Splats are loaded via the sequential parameters. Inside `gsop_splat_scene` there is a `gsop_load_splat` for every splat loaded in. Inside each `gsop_load_splat` you can use the XForm cam to set the transforms applied to that splat as a pre-transform — like adjusting a camera, but a bit easier. You can also add sequential camera presets that you scrub through with the Cam Preset Index parameter. This is a static load: it loads the splat only.

#### Gaussian Splat

| Parameter | Description |
|-----------|-------------|
| Render TOP (`Rendertop`) | A reference to the Render TOP that is being used to render the Gaussian splat. |
| Camera (`Camera`) | Read-only. Auto-filled based on the Render TOP selected. |
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

#### Optimization

| Parameter | Description |
|-----------|-------------|
| Global Rotation and Scale (`Persplattransformrot`) | When enabled, a global rotation and scale is applied to all splats loaded in this component. |
| Master Splat Uniform Scale (`Mastersplatuniformscale`) | Only enabled if Global Rotation and Scale is on. Overrides any uniform scale applied to the specific splat. |
| Master Splat Rot (`Mastersplatrot1`, `Mastersplatrot2`, `Mastersplatrot3`) | Only enabled if Global Rotation and Scale is on. Overrides any rotation applied to the specific splat. |
| Lock Replicants (`Lockreplicants`) | Locks the replicated splat networks inside this component after they are created. |

---

### gsop_splat_scene_particles

**Splat Particles Scene** · IO · Generator

Usage is similar to `gsop_splat_scene`, with a few additions. It allows mixing between splats: set a Splat A Index and a Splat B Index, then use the Mix parameter to smoothly blend between them. When Blending Any to Any is on, the Mix parameter blends between the A and B splats. When it is off, a texture input determines the splat instead: the texture's 0-1 range is remapped to 0 to (number of splats loaded), and the texture value at each location determines which splat is rendered at that place on screen.

Splat Transform Mode bypasses all animation in the chain so you can visualize the splat itself — most helpful when doing the initial transform and positioning of a splat.

#### Gaussian Splat

| Parameter | Description |
|-----------|-------------|
| Render TOP (`Rendertop`) | A reference to the Render TOP that is being used to render the Gaussian splat. |
| Camera (`Camera`) | Read-only. Auto-filled based on the Render TOP selected. |
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

#### Dynamics

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

#### Optimization

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

---

### gsop_load_splat

**Load Splat** · IO · Generator

`gsop_load_splat` is used inside both scene generators (`gsop_splat_scene` and `gsop_splat_scene_particles`), and can also be used standalone. Its main purpose is to provide an interface for using the camera to bake in a pre-transform for the splat through a convenient UI.

Its parameters mirror the per-splat fields documented under gsop_splat_scene (Gaussian splat PLY, Reload, SPZ, T, R, Uniform Scale, Cam Preset Index).

---

### gsop_write_splat_ply

**Write Splat PLY** · IO · Generator

Writes splat data to a .ply file. Currently does NOT support spherical harmonics.

No custom parameters — operates on input splat data.

---

### gsop_particle_system

**Convert to ParticleSystem** · Edit

Used inside the particle system scene generator (`gsop_splat_scene_particles`) to convert splats into a particle system.

| Parameter | Description |
|-----------|-------------|
| Mix Texture (`Mixtexture`) | The texture used to determine which splat is drawn to screen, in screen space. |

---

### gsop_frustum_delete

**Frustum Delete** · Optimization · Filter

Deletes splats outside the camera frustum. Requires reference to gsop_splat_scene. Use before gsop_splat_geo.

| Parameter | Description |
|-----------|-------------|
| Splat Scene (`Splatscene`) | A reference to the splat scene generator. |

---

### gsop_thin_splat

**Thin Splat** · Optimization · Filter

Thins the input splat by percentage to reduce point count.

| Parameter | Description |
|-----------|-------------|
| Bypass (`Bypass`) | Enables or disables the component. |
| Thin Pct (`Thinpct`) | The percent of splats that are culled. As it approaches 1, the entire splat is culled. |

---

### gsop_blowout

**Blowout** · Optimization · Filter

Adds Z-space between every splat. Very sensitive. Used for optimization.

| Parameter | Description |
|-----------|-------------|
| Bypass (`Bypass`) | Turns the component on and off. |
| Blowout (`Blowout`) | Determines the value of space added between each splat. |

---

### gsop_bounding_box

**Bounding Box** · Edit · Filter

A general-use bounding box for constraining splats to a region. This does not copy the geometry back to the CPU — it simply limits which points get passed further down the chain.

| Parameter | Description |
|-----------|-------------|
| Bypass (`Bypass`) | Turns the component on and off. |
| Bounding Type (`Type`) | The type of bounding box (sphere or box). |
| Scale (`Scalex`, `Scaley`, `Scalez`) | The scale of the bounding box. |
| Rotate (`Rotatex`, `Rotatey`, `Rotatez`) | The rotation of the bounding box. |
| Translate (`Translatex`, `Translatey`, `Translatez`) | The translation of the bounding box. |

---

### gsop_splat_geo

**Splat Geo** · Render · Filter

The rendering workhorse for GSOPs, containing all the render-time logic and features, including:
- Sorting based on camera perspective
- Adding render-time attributes to the splat
- Material-based effects like Chroma Key, Relighting, Bokeh, and Motion Blur

**Notes:**
- On operator create, a small script back-traces your chain and attempts to find the `gsop_splat_scene` component. If this fails, you will be asked to drag-and-drop it manually.
- **Detail Bias** is a key quality control: it scales splat opacity by distance-from-camera and screen-space scale, so larger/further splats fade out.
- Render params like **Alpha Mix** and **Detail Bias** can be applied globally, or driven per-region by a texture.
- **Bokeh** can be driven globally or per-region from a texture. **Bokeh Alpha Reduction** ties bokeh scale to alpha — pairs well with Detail Bias and animating the focal length.
- **Relighting:** enable **Use TD Lighting** to have standard TouchDesigner Light COMPs drive the shader.

| Parameter | Description |
|-----------|-------------|
| Splat Scene (`Splatscene`) | A reference to the GSOP generator at the beginning of the chain. |
| Auto Populate Splat Scene COMP (`Autopopulatesplatscenecomp`) | Pulse to search backward through operator wiring to find the Splat Scene. |
| Splat Size (`Splatsize`) | Global multiplier on the size of each splat. |
| Scale Distance Threshold (`Scaledistancethreshold`) | Distance from home at which the splat becomes full scale. Generally 2-5. |
| Scale from Disthome Strength (`Scalefromdisthomestrength`) | Additional scaling based on distance from home. |
| Cull Travelling Splats (`Culltravellingsplats`) | When on, splats beyond Scale Distance Threshold from home are not drawn. |
| Motion Blur (`Motionblur`) | Strength of motion blur applied at render time. |
| Alpha Render Params from Texture (`Alpharenderparamersfromtexture`) | When on, Alpha Mix and Detail Bias are driven by a texture. |
| Alpha Mix Texture (`Alphamixtexture`) | Texture that determines Alpha Mix and Detail Bias values. |
| Alpha Mix (`Alphamix`) | At 0, full color. At 1, only alpha value drawn for RGB. |
| Detail Bias (`Detailbias`) | Scales opacity by distance and screen-space scale, increasing perceived detail. |
| Alpha Discard Threshold (`Alphathreshold`) | Pixels below this alpha are not rendered. |
| Output Depth (`Outputdepth`) | Draws depth to a second render buffer. |
| Depth Rolloff (`Depthrolloff`) | Controls depth texture range from black to light. |
| Quantize Rot Angle (`Quantizerotangle`) | Quantizes rotation angle. At 1, fully quantized to 90 degrees. |
| Blend to Constant Quat (`Blendtoconstantquat`) | Uses a single constant quaternion for every splat. |
| Quantize Conic (`Quantizeconic`) | Screen-space quantization for visual effects. |
| Quantize NDC (`Quantizendc`) | Screen-space quantization for visual effects. |
| Bokeh From Texture (`Bokehfromtexture`) | When on, texture input drives bokeh data. |
| Bokeh Texture (`Bokehtexture`) | Texture used for bokeh data. |
| Bokeh Strength (`Bokehstrength`) | How strong the bokeh effect is. |
| Bokeh Focal Length (`Bokehfocallength`) | Distance from camera where splat is perfectly in focus. |
| Bokeh Band Width (`Bokehbandwidth`) | Range around focal length that stays in focus. |
| Bokeh Vignette Falloff (`Bokehvignettefalloff`) | At 1, center of screen has no bokeh applied. |
| Bokeh Alpha Reduction (`Bokehalphareduction`) | Uses bokeh scale to also reduce alpha. |
| Bokeh Plane (`Bokehplane1`, `Bokehplane2`, `Bokehplane3`) | X/Y/Z plane for distance calculation. (0,0,1) uses camera-Z-space. |
| Chroma Key (`Chromakeyr`, `Chromakeyg`, `Chromakeyb`) | RGB value to key out. |
| Key Distance (`Keydistance`) | Chroma key tolerance. 1 means no keying. |
| Use TD Lighting (`Usetdlighting`) | Enable standard TD Light COMPs for relighting. |
| Color Correction (`Colorcorrection`) | Enable screen-space color correction. |
| Hue (`Hue`) | Shifts the hue. |
| Diffuse Color (`Diffusecolorr`, `Diffusecolorg`, `Diffusecolorb`) | Diffuse color for relighting. |
| Specular Color (`Specularcolorr`, `Specularcolorg`, `Specularcolorb`) | Specular color for relighting. |
| Temperature (`Temperature`) | Color temperature adjustment. |
| Ambient Color (`Ambientcolorr`, `Ambientcolorg`, `Ambientcolorb`) | Ambient color for relighting. |
| Saturation (`Saturation`) | Color saturation. |
| Brightness (`Brightness`) | Overall brightness. |
| Gamma (`Gamma`) | Gamma response. |
| Contrast (`Contrast`) | Contrast. |
| Reset Color Correction (`Resetcolorcorrection`) | Resets color-correction parameters to defaults. |

---

### gsop_refractive

**Refractive** · Render · Filter

A post-effect that uses a second render pass to create a refractive layer from any input POP geometry. The refracting object is lit with a blend of standard TD lights (Phong), a PBR term (driven by Metallic and Roughness), and environment lights — each with its own intensity control — and refracts the underlying render with adjustable strength and chromatic aberration. It replaces the Render TOP as the final output.

| Parameter | Description |
|-----------|-------------|
| Render Top (`Rendertop`) | The Render TOP being used; gsop_refractive replaces it as the final output. |
| Lighting Intensity (`Lightingintensity`) | Overall lighting intensity. |
| Phong Light Intensity (`Phonglightintensity`) | Intensity of Phong lights. |
| PBR Light Intensity (`Pbrlightintensity`) | Intensity of the PBR term. |
| Env Light Intensity (`Envlightintensity`) | Effect of environment lights. |
| Refraction (`Refraction`) | How much refraction. Higher is more. |
| Chromatic Aberration (`Chomaticabberation`) | Refraction expressed across RGB channels. |
| Metallic (`Metallic`) | Metallic input to PBR. |
| Opacity (`Opacity`) | Overall opacity of the refracting object. |
| Roughness (`Roughness`) | Roughness input to PBR. |

---

### gsop_control_panel

**Control Panel** · UI · Filter

A small, lightweight UI for easier interaction with GSOPs. It lets you view some of the parameters for your splat scene, see the final output, do camera positioning for each splat, and set up camera presets.

| Parameter | Description |
|-----------|-------------|
| Open (`Open`) | Opens the viewer. Can also be triggered with Shift+Ctrl+O on Windows. |
| TDGS Component (`Tdgscomponent`) | Points to your splat scene generator. |
| Parameter Operator (`Op`) | Points to your splat scene generator. |

---

## Third-Party Licenses

GSOPs includes [TDFam](https://github.com/dotsimulate/TDFam) by Lyell Hintz and Dan Molnar, licensed under the Apache License 2.0. See `TDFam-1.0.1/LICENSE` and `TDFam-1.0.1/NOTICE` for full license text and attribution.
