---
tags:
  - resource
Area: "[[3D Printing]]"
---
# A Step-by-step Guide for the Perfect Bed Adhesion and Removing Elephant Foot on a Resin 3D Printer

[February 7, 2022](https://blog.honzamrazek.cz/2022/02/a-step-by-step-guide-for-the-perfect-bed-adhesion-and-removing-elephant-foot-on-a-resin-3d-printer/) | [Jan Mrázek](https://blog.honzamrazek.cz/author/yaqwsx/)

Share via

Facebook Twitter LinkedIn Reddit

In my [recent blog post](https://blog.honzamrazek.cz/2022/01/prints-not-sticking-to-the-build-plate-layer-separation-rough-surface-on-a-resin-printer-resin-viscosity-the-common-denominator/), I showed you that the resin viscosity and printer’s poor construction are the main reasons why people observe print failures. I also highlighted that the same phenomenon causes the elephant foot. However, I did not give you a step-by-step guide on how to work around it. I’ll fix this in this blog post, where I show you how to use UVTools to post-process your sliced files in order to get the perfect bed adhesion and no elephant foot on your prints.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/intro.jpg)

I will show you how to get perfect results every time.

If you haven’t read the blog post, read it. If you are in hurry and you just want to quickly “solve all your problems™”, I give you a brief recap.

## Why Is There Elephant Foot?

Most people claim that it is caused by overexposure. However, that is not entirely true. Some of the elephant foot is caused by overexposure, however, people observe much large elephant foots that it is possible only by overexposing. Also, the elephant foot seems to be larger on the larger printer.

The main reason is that the printer is squeezing out resin during the exposure. To squeeze resin into a 50 µm layer takes a lot of force. Unfortunately, most of the printers have relatively weak construction (do you remember people going crazy about Mars 3 Z-wobble?) therefore, when the build plate moves into the resin, the printer flexes. Therefore, the resulting layer is thicker and even when the exposure starts, the build plate pushes down and squeezes resin. Since the resin is already curing, bits of partially cured resin get squished out, and thus, you get a big elephant foot.

So the goal here is to start the exposure once the build plate settles in position. In that case, no resin is squished out, the layer has a correct height and therefore, you need lower curing time for the bottom layer and you get no elephant foot. Easy as that.

Without any feedback on whether the build plate is moving (e.g., using sensors like I did in my blog post), we have only one option – just wait. There is already a resting time feature in the slicer, however, it has one problem – when you set to all layers, your prints will take an eternity to print. You only need to set it to the first millimeter of your print. And you can’t do that in Lychee nor in Chitu slicer.

## What is Wrong with Slicer Compensation?

You might object that slicers already have compensation for that built-in. So why bother? Well, if I omit the fact that having thick base layers causes layer adhesion, the compensation is not perfect. And it cannot be. You will always lose details. You cannot print nice and thin features with the compensation.

One viable approach would be multi-exposure, i.e., first, expose the inner, heavily compensate layer. The layer has an offset of 1 mm, so no squished resin gets beyond the intended perimeter. Then, without lifting, expose a second, precise pattern with regular exposure to get the precise perimeter. However, the current slicers and formats are not able to do multi-pattern exposure.

## The Goal

To recap what we need to achieve in our sliced file in order to stick properly and have no elephant foot:

- 1-3 base layers with high exposure (1.5-3× the normal exposure) and long rest times before starting the exposure (20+ seconds). We discuss the length of the rest time in a moment.
- 20 layers with normal exposure and long rest times
- rest of the layers with normal exposure and no rest times

You can clearly see that nor Chitu, nor Lychee can do this. They only distinguish between the base and normal layers. Fortunately, [UVTools](https://github.com/sn4k3/UVtools) will save us!

There is one aspect of leveling the build plate. To make the whole process work nicely if you have precise layer height. That means that you should level against empty resin vat. No resin inside (as it will push the build plate away), no leveling paper. Leveling cards are snake oil introduced by the printer sellers: people called for it, so the manufacturer gave them something. People are happy and nobody cares that the whole procedure is just wrong. The same goes for setting Z=0, there is no need to do so whatsoever. You just need precise layer height. That’s all. Also, there is no need to relevel in my experience unless I change the LCD.

The rest times are based on my observation of forces during printing (as described here) for Saturn. Smaller printers can probably work with less time, bigger ones will probably need more. Similarly, resin viscosity plays a role. A thick resin will probably need bigger rest times. I can get away with about 5 second rest times with Siraya Tech Simple, I need 40+ seconds for Siraya Tech Sculp or Mayer makes resin. Colder environments yield thicker resin, so they also increase the rest time needed. Feel free to experiment here.

## The Manual Way and What’s Wrong with It

In the original post, I introduced a procedure for manual adjustment. I set a high light-off delay in the slicer, let the printer print for 1 or 2 millimeters and then I change the light-off manually via the gear icon on the printer. I was notified by my readers that the procedure doesn’t work. Indeed, it does not. I was running my Saturn with ancient firmware using the old Chitu format. Once I upgraded my Saturn to the newest firmware, so I can use it with Chitubox 1.9, the gear icons stopped working. Also, it seems that the new firmware completely started to ignore the rest times for the first layer – the most important one! Therefore, there is a need for the automated procedure…

## Automatic Post Processing with UVTools

There is a tool called [UVTools](https://github.com/sn4k3/UVtools) developed by [Tiago Conceição](https://github.com/sn4k3). It is a wonderful tool that supports many file formats for resin printers and allows you to modify them, e.g., merge multiple files, adjust exposure without the need to reslice, and more. You should give it a try.

**08/2022 UPDATE: The functionality is part of the UVTools 3. The guide below doesn’t work in it. Please, follow the [updated guide](https://blog.honzamrazek.cz/2022/07/step-by-step-guide-on-perfect-bed-adhesion-and-elephant-foot-removal-in-uvtools-3/).**

I reached out to Tiago and he wrote a plugin for UVTools that can adjust the rest times just as we need. The usage is pretty simple (there is an image step-by-step guide below).

- Download and install UVTools from [https://github.com/sn4k3/UVtools/releases](https://github.com/sn4k3/UVtools/releases)
- Prepare a slicer profile:
    - set 2-3 base layers
    - set base exposure to 1.5-3× the normal exposure
    - use no transition layers
    - set wait mode to rest times
    - set all rest times to 0
- Slice your model
- Open the sliced file in UVTools
- Go to Tools -> Scripting and select the following script (you have to dowload): [ScriptZDebanding.cs](https://raw.githubusercontent.com/sn4k3/UVtools/master/UVtools.ScriptSample/ScriptDebandingZSample.cs)
- Enter the parameters and hit the “Scripting” button
    - I usually use the safe debanding height of 1 mm
    - Rest time before cure on the debanding area to 20-40 seconds
    - I set no or 1 second rest times for the normal layers
- Save the file and you are ready to print!

Note that UVTools adds a first, empty, layer to overcome the limitation of the printer where all rest times are ignored for the first layer. So if your printer moves down, blicks, and moves up, that is all right.

Here’s the promised step-by-step image guide:

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial1.png)

These are the settings in the Chitu Slicer. Be sure to select wait mode to rest time and set it to 0. I also suggest you to increase the lift distance - I have installed a special film instead of FEP, thus, my lift distances can be smaller. You can do so similarly in Lychee. Slice the files and save it.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial2-1024x555.png)

This is the basic window of UVTools

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial3-1024x554.png)

Open the sliced file.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial4-1024x554.png)

It takes a while.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial5-1024x557.png)

Once it is loaded you can see the layers preview.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial6-1024x556.png)

Go to the menu a select scripting.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial7-1024x557.png)

Load the debanding script you downloaded earlier.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial8-1024x555.png)

Set the desired parameters and hit "Scriptng"

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial9-1024x556.png)

The first layer is dark - this is OK. UVTools adds an extra base layer to overcome some firmware limitations.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/tutorial10-1024x558.png)

If you move one layer up, everything is there. Now save it and print it.

Note that debanding will prolong your print by roughly 15 minutes. This is the time spent waiting in the first millimeter. That’s all you pay for this solution.

## The Results

I use this procedure for a quite long time and it works perfectly. No problems with sticking, no problems with elephant foot, no problems with having a hard time removing the prints when they stick too much.

I have picked a few examples that demonstrate how effective the procedure is. First, I can print parts with a tiny base directly on the build plate. They stick just enough – the prints are nicely straight and removing them gives you real pleasure. The base is 35 mm × 1.3 mm which is more than enough. Printed in Siraya Tech Fast White, 2.6 seconds normal exposure, 7 seconds base layer. The first millimeter was debanded with 30 seconds on my Elegoo Saturn.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/inserts1-1024x576.jpg)

The prints are attached to the build plate only via a small surface. Yet they all turn out perfect.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/inserts2-1024x576.jpg)

More perfection

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/inserts3-1024x576.jpg)

See - no elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/inserts4-1024x576.jpg)

See - no elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/inserts5-1024x741.jpg)

See - no elephant foot.

This is how satisfactory is to remove the prints from the build plate:

Second, I picked the recently famous articulated dragon model. People go crazy on TikTok, Youtube and Facebook groups with how hard is it to print it correctly, they claim it is impossible to print it on build plate remove it in a single piece. Well… it is certainly possible. This model is printed at 60% scale – therefore all tolerances and clearances are much tighter than intended by the designer. There is no elephant foot. Removing is quite easy. I was afraid of breaking the fingernails, so I was careful, but there wasn’t a single problem. I could have removed it more drastically. Everything moves nicely – except for the legs, where choosing Siraya Tech Fast Gray wasn’t the wisest choice as it has a tendency to cross-layer curing, therefore, it bridges badly. But after a careful push, even the legs started to move.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon1-1024x601.jpg)

60% scale of the dragon

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon2-1024x532.jpg)

Printed directly on the bed

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon3-1024x631.jpg)

No elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon4-906x1024.jpg)

No elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon5-768x1024.jpg)

No elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon6-1024x691.jpg)

No elephant foot.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/dragon7-732x1024.jpg)

Removing it from the build plate was easy.

Here’s the removal procedure:

The last demonstration of removing the elephant foot, and the most notable one, is the demonstration of a simple M1 spur gear (Lego size). You can see the big difference between the standard procedure and the procedure with included rest times. The elephant foot is gone. Both gears were otherwise printed with the exact same settings.

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/gears1-1024x645.jpg)

The gears side-by-side - one with elephant foot one without

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/gears2-1024x521.jpg)

The gears side-by-side - one with elephant foot one without

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/gears3-1024x773.jpg)

Gear with debanding on the build plate

![](https://blog.honzamrazek.cz/wp-content/uploads/2022/02/gears4-1024x660.jpg)

Gear without debanding on the build plate

## Conclusion

I am confident enough, that the long-existing phenomenon of elephant foot on resin printers was solved. I have to admit, that all my previous attempts were just wrong (they basically implement the same approach today’s slicers use – see the old blog post and the other [one](https://blog.honzamrazek.cz/2020/01/does-dark-build-plate-on-an-sla-printer-reduce-exposure-bleeding/)). I hope the procedure above helps you to get even better resin prints.

There is still room for improvement. The script above is just pretty dumb. I plan to tackle blooming in the next iteration by adding delays to layers where a box is closed or a large cross-section is nearby. However, to do so I need to first gather some data in order to make the procedure as efficient, as possible.

If you like my research not only that I ask you to consider supporting me via the means stated below, but I also ask you to support Tiago – he did a ton of useful work on the UVTools. You can support him [on GitHub](https://github.com/sponsors/sn4k3) or [directly via PayPal.](https://paypal.me/SkillTournament)