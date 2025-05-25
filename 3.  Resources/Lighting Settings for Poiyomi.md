---
tags:
  - Unity
  - Poiyomi
  - resource
Area: "[[3D Modeling]]"
---

Make sure you set Probes --> Anchor Override to "chest"

![[Pasted image 20231014111235.png]]


##### Base Pass Lighting

![[Pasted image 20231014111448.png]]

###### Grayscale Lighting

This sets the effect of color from base pass lighting.  Set to 1 it completely ignores color from the lighting.  Set to 0 it receives all the color from the lighting 

Recommended:  0.4


###### Min Brightness

This determines how dark your model can get.  If it set to 0 then if a world goes completely dark, so will your model.  This is personal choice, but a value of  0.05 will keep  your model from going completely black.


##### Base Pass Shading


![[Pasted image 20231014112250.png]]

###### Lighting Type

Set to "Multilayer Math".

###### Layer 1 --> Color

This is the color that  your shadows will appear if you set it to Ignore Indirect  Shadow Color

###### Ignore Indirect Shadow Color

This is personal preference.  At 0 your shadows will take their color from whatever world you are in.  At 1 it will completely ignore the world and use Layer 1 --> Color for your shadows.  

##### Add Pass Lighting

![[Pasted image 20231014112802.png]]

###### Max Brightness

This the maximum intensity your model will receive from a "single" point light.  However,  multiple point lights will stack and your model can still get blown out if there are enough of them. 

Recommended:  1.25 - 1.3

A little above 1 will make sure that you still see some effect from Point lights if your model is already in a bright setting.

You can limit it to the absolute value regardless of the number of point lights by setting Rendering --> Blending --> Additive Blending --> RGB Blend Op to "Max"

![[Pasted image 20231014113207.png]]

##### Add Pass Shading

![[Pasted image 20231014113657.png]]

In "Toon" mode, this setting affects how the shadow line from a point light looks on your model . 

At 0:1 it will be a smooth transition from dark to light
At 0.5: 0.5  it will be a hard line like cell shading
At 1:1 there will be no shadow line at all