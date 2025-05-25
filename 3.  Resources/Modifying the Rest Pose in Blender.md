---
tags:
  - Blender
  - resource
Area: "[[3D Modeling]]"
---

Posted on [March 28, 2013](https://nixart.wordpress.com/2013/03/28/modifying-the-rest-pose-in-blender/ "19:43")

36 Votes

  

This procedure supposes that you have already rigged and weight-painted your object so that it deforms correctly. At this point, you simply want a different rest pose for your object. However, when selecting “Apply Pose as Rest Pose”, you do not want to waste your time correcting your mesh and redo the weight painting for your new rest pose. Here is how you can do it:

1. Select your armature and go in “Pose Mode”.
2. Pose your object in your new rest pose.
3. Go in “Object Mode” and select your deformed object.
4. In the object’s “Object Modifiers” stack, copy the “Armature Modifier” by pressing the “Copy” button. You should have two “Armature Modifiers”, one above the other in the stack, with the same parameters. This will deform your object twice, but it is ok. If you go in “Edit Mode”, you will see that the mesh has been deformed in your new rest pose.
5. Apply the first “Armature Modifier” (the top one), but keep the bottom one. The latter will replace the old “Armature Modifier” and will allow to pose your object with respect to your new rest pose. At this point, the object will still be deformed twice. That is because we need to apply the current pose as the new rest pose.
6. Select your armature and go in “Pose Mode”.
7. “Apply Pose as Rest Pose” in the “Pose” menu. This will clear the double deformation and put your object in your new rest pose.