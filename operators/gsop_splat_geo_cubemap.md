[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Splat Geo Cubemap

`gsop_splat_geo_cubemap` · Render · Filter

Renders the splat scene as a **cube map** — six 90° views in one Render TOP — the
**highest-quality 360 mode**. Splat opacity is evaluated exactly per pixel ray, so
there are no seams between cube faces, no artifacts at the zenith/nadir, and thin
structures (wires, branches, railings) stay continuous across the whole sphere.

The cube map output drops directly into TouchDesigner's environment tools
(Environment Light, reflection maps, skyboxes), or converts to a standard 2:1
equirectangular image with a **Projection TOP**.

## Usage

**Cubemap rendering does not yet support relighting, bokeh, or motion blur - you will notice those parameters are greyed out. Sorry.**

- Wire it exactly like [Splat Geo](gsop_splat_geo.md): it needs a `Splatscene`
  reference (auto-found on create, or drag-and-drop).
- On the Render TOP, enable **Render Cube Map** and use a **square resolution**
  (1024 or higher recommended — this is the size of each face).
- The camera's **position** is the viewpoint; its orientation sets the cube's
  facing. FOV is ignored — faces are always 90°.
- For a 2:1 panorama, feed the render into a **Projection TOP** set to
  Cube Map → Equirectangular.
- For splat-lit scenes, feed the raw cube map into an **Environment Light**.

## Performance

- Cost scales with face resolution squared — each step down (1024 → 896 → 768)
  is a large saving if you can spare the sharpness.
- [Thin Splat](gsop_thin_splat.md) and [Blowout](gsop_blowout.md) reduce splat
  count/overlap and pay off directly here.
- Raising **Alpha Discard Threshold** slightly (e.g. 0.001 → 0.005) trims the
  soft edges of every splat and can recover meaningful GPU time in both modes.

## Parameters

Parameters match [Splat Geo](gsop_splat_geo.md) — see that page for the full
reference. Differences in this mode:

| Difference | Detail |
|-----------|--------|
| **Motion Blur** | Not supported in this mode (parameter has no effect). |
| **Bokeh** (all parameters) | Not supported in this mode. |
| **Use TD Lighting / Relighting** | Not supported in this mode. |

Alpha rendering (Alpha Mix, Detail Bias, Alpha Discard Threshold), Chroma Key,
Quantize effects, Color Correction, and Depth Output all work as in Splat Geo.
