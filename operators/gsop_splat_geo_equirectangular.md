[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Splat Geo Equirectangular

`gsop_splat_geo_equirectangular` · Render · Filter

Renders the splat scene as a full **360° × 180° equirectangular panorama in a single
pass** — the fast 360 mode. The output maps directly onto a standard 2:1 equirect
image, ready for immersive rooms, dome pipelines, sphere/skybox mapping, and 360
video export.

For maximum quality (seam-free, best zenith/nadir), see
[Splat Geo Cubemap](gsop_splat_geo_cubemap.md) — same scene wiring, higher GPU cost.

## Usage

- Wire it exactly like [Splat Geo](gsop_splat_geo.md): it needs a `Splatscene`
  reference (auto-found on create, or drag-and-drop).
- The camera's **position** is the panorama viewpoint and its **orientation** sets
  which direction lands at the center of the image. The camera's FOV is ignored —
  the shader always renders the full sphere.
- Set the Render TOP resolution to **2:1** (e.g. 4096×2048) for a standard
  equirectangular image.

## Notes

**Equirectangular rendering does not yet support relighting, bokeh, or motion blur - you will notice those parameters are greyed out. Sorry.**

- **Wrap seam:** content that crosses the left/right edge of the panorama (directly
  *behind* the camera's facing) can show a visible seam, most noticeable on large,
  close objects. Rotate the camera so the seam lands in a low-detail direction
  (open sky, distant foliage). A seam-free mode is planned; the
  [Cubemap](gsop_splat_geo_cubemap.md) renderer has no seam today.
- **Zenith / nadir:** sharpness straight up and straight down is limited by what the
  scan actually captured — most 360 scans have a hole at the nadir where the camera
  rig stood. This is a data artifact, not a render setting.
- Splats are depth-sorted radially around the viewpoint automatically — no extra
  sorting operators needed.

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
