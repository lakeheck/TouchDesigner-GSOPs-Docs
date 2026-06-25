[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal.png" width="240" />

# Bounding Box

`gsop_bounding_box` · Edit · Filter

A general-use bounding box for constraining splats to a region. This does not copy the geometry back to the CPU -- it simply limits which points get passed further down the chain.

## Parameters

| Parameter | Description |
|-----------|-------------|
| Bypass (`Bypass`) | Turns the component on and off. |
| Bounding Type (`Type`) | The type of bounding box (sphere or box). |
| Scale (`Scalex`, `Scaley`, `Scalez`) | The scale of the bounding box. |
| Rotate (`Rotatex`, `Rotatey`, `Rotatez`) | The rotation of the bounding box. |
| Translate (`Translatex`, `Translatey`, `Translatez`) | The translation of the bounding box. |
