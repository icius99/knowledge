---
tags:
  - Blender
  - resource
Area: "[[3D Modeling]]"
---

Try using a [displace modifier](https://docs.blender.org/manual/en/latest/modeling/modifiers/deform/displace.html) with a [procedural texture](https://docs.blender.org/manual/en/latest/render/blender_render/textures/types/procedural/voronoi.html):

1. Add a cube (⇧ ShiftA)
    
2. Add a subsurf modifier (⎈ Ctrl5) (where 5 refers to the number of viewport subdivisions.)
    
3. Add a displace modifier, and click _New texture_:
    
    ![enter image description here](https://i.stack.imgur.com/p7rKV.png)
    
    Then click the _properties_ icon on the far right of the button to go to the texture settings for the new texture.
    
4. Set the _type_ to _Voronoi_:
    
    ![enter image description here](https://i.stack.imgur.com/ldQTM.png)
    
    I found that using _Distance squared_ gives more rounded looking puffs, which might be what you want.
    
5. Back in the modifiers panel, reduce the strength of the displace modifier to some negative value so that the puffs are convex instead of concave.
    
    ![enter image description here](https://i.stack.imgur.com/TnXMH.png)
    
6. Optionally model the cube into a shape approximately how you want the wool to be, and add a second displace modifier for larger displacements (you can use _object_ coordinates and a scaled empty to make the texture larger):
    
    ![enter image description here](https://i.stack.imgur.com/5Olpm.png)