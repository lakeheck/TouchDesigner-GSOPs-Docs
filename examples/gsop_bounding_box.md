[Back to Examples](README.md)

# Bounding Box

Remove splats based on a bounding box, with some options.

![Bounding Box](images/gsop_bounding_box.png)

<video src="videos/gsop_bounding_box.mp4" controls width="100%"></video>

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo`
4. renderTOP
5. `gsop_bounding_box`

## Process

1. Add the `gsop_bounding_box` operator between the `gsop_splat_scene` and `gsop_splat_geo`, and set its bounding box params as desired

## Notes

Can be either a bounding sphere or box.
