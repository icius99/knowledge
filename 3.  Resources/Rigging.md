---
tags:
  - resource
  - Blender
Area: "[[3D Modeling]]"
---

### Tips and Tricks

Ctrl+R in Edit mode to Rotate Bone Axis.

For Blender Symmetrize:

Examples of valid separators:

	(nothing): handLeft –> handRight
	“_” (underscore): hand_L –> hand_R
	“.” (dot): hand.l –> hand.r
	“-” (dash): hand-l –> hand-r
	” ” (space): hand LEFT –> hand RIGHT

### Steps

1. Add  your mesh and add a bone
![[Pasted image 20230501190028.png]]
   
2.  Make sure the bones are "In Front":
   
   ![[Pasted image 20230501190202.png]]
3. Name the Bones
   
   ![[Pasted image 20230501190701.png]]
4.   Select the Body and then the Armature.  Use Ctrl+P and select "Armature Deform"
   
   ![[Pasted image 20230501191007.png]]
5. Here is the resulting hierarchy:
   
   ![[Pasted image 20230501191122.png]]
6. Select the Armature and then the Body and go to Weight Paint mode:
   
   ![[Pasted image 20230501191636.png]]

7. Use the following settings:
   
   Weight: 1.000
   Strength: 1.000
   Paint Mask: Off
   Vertex Selection: Off
   Brush-->Blend: Add
   Brush-->Advanced-->Front Faces Only: Off
   Falloff: Projected

8. When  using LMB select mode,  you must use CTRL+LMB to select bones!!!

9. Select the bone you want and paint the weights for it.