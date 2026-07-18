WorkingFloorAL for MikuMikuDayo
================================

Files:
- WorkingFloorAL.fxdayo : HLSL Shader Model 6.x postprocess effect.
- WorkingFloorAL.pmx    : controller PMX with morph sliders.

Default behavior:
- FloorSizeX morph value 1.0 = 10 MMD units.
- FloorSizeZ morph value 1.0 = 10 MMD units.
- FloorSizeX/FloorSizeZ slider range is 0.1 to 10.0, so the floor can be 1 to 100 MMD units.
- The grid interval is fixed at 10 MMD units.
- Reflectivity 0.0 = no reflection, 1.0 = 100% screen-space reflection.

Controller morphs:
- FloorSizeX
- FloorSizeZ
- Reflectivity
- off

Install:
- Put WorkingFloorAL.fxdayo and WorkingFloorAL.pmx in the same folder.
- Load WorkingFloorAL.pmx in MikuMikuDayo. The matching .fxdayo starts as a postprocess.

Internal defaults:
- Grid thickness = 0.018
- Grid opacity = 0.0
- Edge feather = 0.75 MMD units

Notes:
- This is a MikuMikuDayo YRZFX postprocess. It receives the final color buffer and approximates
  the reflective floor with a simple screen-space mirror around the projected world origin on y=0.
- The floor area itself is calculated from the camera ray intersection with the world y=0 plane,
  so the reflection origin is stable when camera distance changes.
- Reflectivity 1.0 keeps the mirrored screen sample at full strength. SSR ray marching is not used
  because it can pick up walls, furniture, and depth noise, causing chaotic reflection artifacts.
- If MikuMikuDayo exposes depth, camera matrices, or a mirrored scene render target in your local
  build, those can be added later for physically correct floor placement.
- The PMX controller is intentionally tiny and visually unobtrusive. Its morph names are intended
  to be used by MikuMikuDayo's controller-to-effect parameter binding.
