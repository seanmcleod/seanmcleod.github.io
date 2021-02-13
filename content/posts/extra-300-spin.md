---
title: "Extra 300 Spin"
date: 2018-05-17T23:36:47+02:00
hasMath: true
---

This is an example of the data collected by my [Homebrew FTI (Flight Test Instrumentation)](https://seanmcleod.github.io/2018/02/homebrew-fti/)
system during a spin in an Extra-300.

![image alt text](/images/extra-300-spin/extraaircraft.jpg)

The control positions were tracked using a camera based tracking system that I developed 
and the output from the camera tracking units were fed into the FTI unit.

Here are a couple of graphs showing the FTI captured during the spin.

This first graph shows the control positions for the rudder and elevator and the roll angle 
during the spin. The spin is entered with full back stick and full right rudder. To stop 
the spin full opposite rudder is applied briefly and then then the rudder and stick are 
returned to neutral.

![image alt text](/images/extra-300-spin/extraspingraph1.png)

The second graph displays the indicated airspeed (IAS) as Vi and the ground speed from the 
GPS as GS in addition to the pitch and roll angles.

![image alt text](/images/extra-300-spin/extraspingraph2.png)

The third graph shows the angular rates for all three axes.

![image alt text](/images/extra-300-spin/extraspingraph3.png)

And lastly a graph showing the accelerations experienced in all three axes in {{< tex "m/s^2" >}}.

![image alt text](/images/extra-300-spin/extraspingraph4.png)

We also had a GoPro camera mounted in the cockpit which we synchronized with the FTI data.

![image alt text](/images/extra-300-spin/extravideo.jpg)

The FTI data and synchronized video in my FTI Playback software.

![image alt text](/images/extra-300-spin/extraftiplayback.png)

