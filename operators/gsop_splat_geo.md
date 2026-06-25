[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Splat Geo

`gsop_splat_geo` · Render · Filter

The rendering workhorse for GSOPs, containing all the render-time logic and features, including:
- Sorting based on camera perspective
- Adding render-time attributes to the splat
- Material-based effects like Chroma Key, Relighting, Bokeh, and Motion Blur

## Notes

- On operator create, a small script back-traces your chain and attempts to find the `gsop_splat_scene` component. If this fails, you will be asked to drag-and-drop it manually.
- **Detail Bias** is a key quality control: it scales splat opacity by distance-from-camera and screen-space scale, so larger/further splats fade out.
- Render params like **Alpha Mix** and **Detail Bias** can be applied globally, or driven per-region by a texture.
- **Bokeh** can be driven globally or per-region from a texture. **Bokeh Alpha Reduction** ties bokeh scale to alpha -- pairs well with Detail Bias and animating the focal length.
- **Relighting:** enable **Use TD Lighting** to have standard TouchDesigner Light COMPs drive the shader.

## Parameters

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
