---
tags:
  - resource
  - Blender
Area: "[[3D Modeling]]"
---

#### Blender Setup

As Per: https://studio.blender.org/training/weight-painting

###### Turn on Zero Weight as Black

![[Pasted image 20230707210826.png]]


###### Enable Auto Normalize

![[Pasted image 20230707211103.png]]


######  Remove Unnecessary Brushes

These brushes are shared between Weight Paint and Vertex Paint.  You can thin out the options for Weight Paint.   (instructor only uses Add and Subtract)


![[Pasted image 20230707211335.png]]



######  Double Check Mirroring

If this is not on then it will not mirror with bones.  

![[Pasted image 20230707211904.png]]


######  Extras - Smooth Operator

Use the "Smooth" operator to smooth out difficult areas.  

![[Pasted image 20230707212136.png]]

![[Pasted image 20230707212540.png]]


Set the "Subset" to Deform Pose Bones instead of the default:


![[Pasted image 20230707212303.png]]


Set "Factor" to 1.00 before starting to increase "Iterations".  Iterations can quickly turn your mesh to mush.

![[Pasted image 20230707212333.png]]


######  Extras - Transfer Weights

Useful for transferring weights from body to clothing.

Select Armature-->Source Mesh--Target Mesh

![[Pasted image 20230707212913.png]]


![[Pasted image 20230707213002.png]]


![[Pasted image 20230707213052.png]]




######  Extras - Easy Weight Addon

You can add a shortcut to trigger "Toggle Weight Paint" using the following


![[Pasted image 20230707213251.png]]




1. First block in each bone with a rough influence around it. 
2. Make sure every part of the mesh you are painting is accounted for by some bone (move the root bone around and make sure there is no geometry left behind)

![[Pasted image 20230504191839.png]]


### Automatic Weights Mesh Issues:
Bone heat weighting failed  
Most likely the Laplacian formula has failed because vertices are hidden.

-   intersecting meshes.
    
-   double vertices (remove doubles)
    
-   Must be a manifold object (ck for non-manifold no holes, no doubles, no spare parts, no loose edges, etc)
    
-   Unapplied rotations on scale, location, and rotations with origins not co-located.
    
-   X axis turned on but armature not symmetrical
    
-   Make sure you are using deform bones (you didn’t uncheck deform on all bones did you)
    
-   Are you normals correct? Make sure you have recalculated them and they point outward.
    
-   Do you have modifiers on your mesh? Apply or delete them or save them as the case may be.
    
-   Do you have loose parts on your mesh?
    
-   If a mesh part is not visible to any bone, it will fail.