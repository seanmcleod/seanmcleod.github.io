---
title: "Pixycam Helicopters"
date: 2018-05-20T23:05:27+02:00
---

The standard method of tracking the aircraft's control positions as the pilot moves the 
controls for flight test instrumentation (FTI) purposes is to attach string potentiometers 
(string pots) to the control cables/rods. As the control cable/rod moves based on the pilot's 
inputs a spring loaded thin steel wire is reeled in or out of the string pot. The mechanical 
movement of the reel changes the electrical resistance resulting in a change in voltage output 
which is then measured and recorded by the FTI system.

![image alt text](/images/camera-tracking-of-aircraft-control-positions/stringpot1.png)

In some cases though it would be ideal if you could track the aircraft control positions without 
having to physically attach a wire to the control cable/rod. So I developed a system to track 
the control positions using a computer vision based approach, making use of a [Pixycam](https://pixycam.com/pixy-cmucam5/).

![image alt text](/images/pixycam-helicopters/pixycam.png)

The Pixycam is a small dedicated unit with a microcontroller and camera which is configured to 
track blobs based on hue and report the location of each blob matching the configured hue 
at 50Hz.

The position output is then fed into an FTI unit - [Homebrew FTI](https://seanmcleod.github.io/2018/02/homebrew-fti/)
to display the control position in real-time and to also record it with the rest of the FTI parameters
being recorded by the FTI unit.

So the idea was to find a marker with a distinct hue that we could place on the control inceptors. The 
first course to use this system was a helicopter test pilot course so we needed to mount the markers
on the cyclic and yaw pedals.

We ended up using red Coke caps as the target which you can see mounted on the cyclic and yaw pedals in 
the photo below. A custom enclosure for the Pixycam was made up, and you can see the Pixycam mounted on
the left side of the instrument panel looking down at the yaw pedals. There is a separate Pixycam mounted
on the cockpit ceiling to track the target on the cyclic.

![image alt text](/images/pixycam-helicopters/pixycam-markers1.jpg)

Image showing the markers mounted in another helicopter type, with some live debugging in action.

![image alt text](/images/pixycam-helicopters/pixycam-markers2.jpg)

The test pilot course made use of 3 different helicopter types.

![image alt text](/images/pixycam-helicopters/helicopter-type-1.jpg)

If you look closely you can just make out the Pixycam enclosure mounted on the cockpit ceiling next to
the GoPro camera.

![image alt text](/images/pixycam-helicopters/helicopter-type-2.jpg)

Alouette III, the same type of helicopter my father flew when he was in the airforce.

![image alt text](/images/pixycam-helicopters/helicopter-type-3.jpg)

The biggest challenge was the varying amount of sunlight that fell on the markers as the helicopters flew
around which could affect the hue of the target. If there was too much of a change in the hue then then
the Pixycam would lose track of the target until it's hue changed enough to be close enough to the calibrated
hue.

A couple of years later a second generation version of this concept of using visual markers to track
the aircarft's control positions was developed, see - [Camera Tracking of Aircraft Control Positions](https://seanmcleod.github.io/2018/06/camera-tracking-of-aircraft-control-positions/).


