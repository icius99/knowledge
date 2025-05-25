---
tags:
  - resource
Area:
---
Ok I will try to write an understandable instruction:

In my example I print with PLA and want to use PETG as a release liner for the support. As I said it also works the other way around.

**1)** On the “Other” tab, in the “Flush Options” section, disable the “Flush to support objects” function.

[![Other - Flush](https://cdn-forum.bambulab.com/optimized/2X/a/ae5f61a27f46bfdcbe3b96b7288db923e8c935e1_2_226x500.jpeg)

Other - Flush424×934 94.6 KB

](https://cdn-forum.bambulab.com/original/2X/a/ae5f61a27f46bfdcbe3b96b7288db923e8c935e1.jpeg "Other - Flush")

**2)** Then click on “Flushing volumes” in the Filament section to change the flushing volume.

In the video it is set to 800, but I tested it at 300 and it works fine.

This is to safely separate the two types of filament and get a support layer that separates well.

[![AMS Volume](https://cdn-forum.bambulab.com/optimized/2X/7/712acaf1d943dd6d3018ba83d437128ec5fe497b_2_690x329.jpeg)

AMS Volume839×401 79.5 KB

](https://cdn-forum.bambulab.com/original/2X/7/712acaf1d943dd6d3018ba83d437128ec5fe497b.jpeg "AMS Volume")

**3)** Switch to the “Support” tab, where the rest of the settings are made.

- In the “Support” section, set the support style to “Snug”.
    
- In the “Filament for Supports” section, under “Support interface”, select the desired filament for support separation (for PLA prints PETG and for PETG prints PLA).
    
- In the “Advanced” section, set the following: (this ensures that the support and the print object are printed through in one and that a smooth surface is created after removing the support).
    

→ Top Z distance = 0.0 mm  
→ Bottom Z distance = 0.0 mm  
→ Base pattern spacing = 2.0 mm  
→ Top linterface layers = 3 (I only use 2 layers and thus save myself a filament change)  
→ Bottom interface layers = 3 (if present)  
→ Top interface pattern = Rectilinear  
→ Bottom interface pattern= Rectilinear (if present)  
→ Top interface spacing = 0.0 mm  
→ Bottom interface spacing = 0.0 mm (if present)  
→ Support/object xy distance= 0.5 mm

[![advanced](https://cdn-forum.bambulab.com/optimized/2X/6/6befb3ad1aab7761c652953f4c7d10c8ddaca027_2_255x500.jpeg)

advanced419×821 89.8 KB

](https://cdn-forum.bambulab.com/original/2X/6/6befb3ad1aab7761c652953f4c7d10c8ddaca027.jpeg "advanced")

**4)** _(Optional, to save time and material)_ In the “Other” tab, disable Prime Tower.

*I hope I wrote it understandable. My English is not very good, so I will use a translator. If there are mistakes in the translation please correct and apologize.