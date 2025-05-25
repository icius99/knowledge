---
tags:
  - resource
  - Blender
Area: "[[3D Modeling]]"
---


Kit Bashing Site

https://booth.pm/en/items/3738752

#### Quick tip for modeling skin-tight clothes in blender

With this setup you only need to care that the vertices of your low-poly mesh for the clothes are outside of the model you are fitting the clothes on.

The modifiers for the mesh of the clothes are in the order as followed. (Settings I didn’t mention are left default):

1.  Mirror modifier, clipping enabled
    
2.  Subdivision Surface Modifier,  
    1 subdivision
    
3.  Shrinkwarp modifier,  
    Target [Your Target], Offset 0.01 (Offset is important, a different value might work better for you)
    
4.  Another Subdivision Surface Modifier,  
    2 subdivisions
    
5.  Solidify modifier,  
    Thickness 0.005'