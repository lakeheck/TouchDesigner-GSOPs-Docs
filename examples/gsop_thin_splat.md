[Back to Examples](README.md)

# Thin Splat Optimization

Easily reduce the splat count to improve render optimization.

## Operators

1. `gsop_camera_viewport` — or any TD camera (mind FOV and far clip settings)
2. `gsop_splat_scene`
3. `gsop_splat_geo`
4. renderTOP
5. `gsop_thin_splat`

## Process

1. Add the `gsop_thin_splat` operator between the `gsop_splat_scene` and `gsop_splat_geo` to use a slider to reduce splats by X pct

## Notes

Often helpful to engage when you are switching between scenes and want the splat to be much more lightweight while it is 'in the background'.
