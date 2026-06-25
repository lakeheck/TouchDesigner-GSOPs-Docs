[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Refractive

`gsop_refractive` · Render · Filter

A post-effect that uses a second render pass to create a refractive layer from any input POP geometry. The refracting object is lit with a blend of standard TD lights (Phong), a PBR term (driven by Metallic and Roughness), and environment lights -- each with its own intensity control -- and refracts the underlying render with adjustable strength and chromatic aberration. It replaces the Render TOP as the final output.

## Parameters

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
