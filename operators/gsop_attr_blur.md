[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Attribute Blur

`gsop_attr_blur` · Animation · Filter

Blurs a point attribute across neighboring splats. Each point gathers nearby neighbors and combines their values, smoothing the attribute spatially — useful for softening color, opacity, scale, or any custom attribute across a region of the splat.

## Parameters

| Parameter | Description |
|-----------|-------------|
| Type (`Type`) | Data type of the attribute to blur (float, vec2, vec3, vec4). |
| Attr (`Attr`) | Name of the attribute to blur. Case sensitive. |
| Mode (`Mode`) | How neighbor values are combined: average, minimum, or maximum. |
| Max Neighbor Distance (`Maxneighbordistance`) | Maximum distance to search for neighboring points. |
| Max Neighbors (`Maxneighbors`) | Maximum number of neighbors each point gathers. |
| Passes (`Passes`) | Number of blur iterations. More passes spread the blur further. |
| Blend to Input (`Blendtoinput`) | Blends the blurred result back toward the original attribute values, recovering the pre-blur input. |
| Bypass (`Bypass`) | Turns the component on and off. |
| Start (`Start`) | Pulse to reset the blur to its initial state. |
| Feedback Active | When On, will blur attribute progressively using a feedback loop