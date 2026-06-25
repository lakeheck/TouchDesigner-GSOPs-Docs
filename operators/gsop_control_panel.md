[Back to Operators](../README.md)

<img src="../assets/GSOPs_horizontal_light.png" width="240" />

# Control Panel

`gsop_control_panel` · UI · Internal

> **Note:** The Control Panel is embedded inside `gsop_splat_scene` and `gsop_splat_scene_particles`. It is not placed separately — access it through those operators.

A small, lightweight UI for easier interaction with GSOPs. It lets you view some of the parameters for your splat scene, see the final output, do camera positioning for each splat, and set up camera presets.

You can also easily record movie file outputs. 

** Keyboard Shortcuts: **
ctrl.shift.o -> Open Viewer 
ctrl.alt.s -> Save Still

## Parameters

| Parameter | Description |
|-----------|-------------|
| Open (`Open`) | Opens the viewer. Can also be triggered with Shift+Ctrl+O on Windows. |
| Find Splat Scene (`Findsplatscene`) | Auto-locate your splat scene generator from other operators on the same network level. |
| Splat Scene (`Splatscene`) | Points to your splat scene generator. |
| Viewer Panel (`Viewerpanel`) | Points to the TOP you want to see in the Control Panel GUI. Defaults to the renderTOP associated with your splat scene generator. |
| Video Outputs (`Videooutputs`) | Folder in which to save video recordings. |
| Still Outputs (`Stilloutputs`) | Folder in which to save video recordings. |

