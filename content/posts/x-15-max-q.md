---
title: "X-15 Max Q"
date: 2024-08-12T11:55:31+02:00
hasMath: true
---

I previously wrote about [Max Q - Maximum Dynamic Pressure](https://seanmcleod.github.io/2018/01/max-q-maximum-dynamic-pressure/) 
comparing the Max Q experienced by a SpaceX rocket during launch, the Space Shuttle and a typical airliner. Now let's take a look
at the Max Q that was experienced by the X-15 while it went about setting various speed and altitude records during it's research.

To recap, the dynamic pressure or Q is the product of the air-density and the velocity squared of the object travelling through 
the air.

{{< tex display="Dynamic\ Pressure\ (Q) = \frac{1}{2} \rho V^2 " >}}

The SI unit for pressure is the pascal. One pascal is the pressure exerted by a force of magnitude
of one newton perpendicularly upon an area of one square meter.

The following graph shows how the density and the speed of sound vary in the standard atmosphere over the altitude range that
the X-15 operated in.

![image alt text](/images/x-15-max-q/std-atmosphere.png)

#### X-15 Report

I came across a reference to an X-15 report while watching Ben Dickinson's YouTube video - [X-15 Space Plane - A Review for 6DOF Model Development | Flight Simulation Tutorial - Section 2.1](https://www.youtube.com/watch?v=iQrN6hgh8e0).

The [Design and Operation of the X-15 Hypersonic Research Airplane](https://apps.dtic.mil/sti/tr/pdf/AD0279830.pdf) report includes
two graphs showing a plot of altitude vs time and Mach vs time for the two types of profiles flown. One profile targetting high 
altitude and one profile targetting high speed.

![image alt text](/images/x-15-max-q/x-15-report-graphs.png)

#### Dynamic Pressure Variation

So after digitizing the altitude and Mach data from the two graphs in the X-15 report we can plot how the dynamic pressure varied
during the two flight profiles, and also check when Max Q was achieved and how large Max Q was for each of the two profiles.

![image alt text](/images/x-15-max-q/x-15-altitude-mission.png)

![image alt text](/images/x-15-max-q/x-15-speed-mission.png)

| Mission |    | Time |     | Altitude |     | Mach |     | Max-Q    |
| ---     |--- | ---  | --- | ---      | --- | ---  | --- | ---      |
| Altitude|    | 30s  |     | 52,300ft |     | 1.72 |     | 21.5 kPa |
| Speed   |    | 45s  |     | 69,000ft |     | 2.91 |     | 27.6 kPa |
| SR-71   |    | N/A  |     | 80,000ft |     | 3.5  |     | 23.7 kPa |

For good measure I've added in the SR-71 for comparison. So in all cases the Max-Q is roughly equal to or less than the Max-Q experienced
by airliners. So even though the X-15 was hypersonic, exceeding Mach 5, the hypersonic speeds were achieved at such high altitude where
the air density is so low that it doesn't result in significant dynamic pressure.
