---
title: "Max Q - Maximum Dynamic Pressure"
date: 2018-01-10T19:47:36+02:00
hasMath: true
---

During a rocket launch the commentator will often call out "Max Q" at a specific point in 
time during the launch. This is the point at which the dynamic pressure acting on the rocket 
will be at it's maximum.

The dynamic pressure or Q is the product of the air-density and the velocity squared of the 
object travelling through the air.

{{< tex display="Dynamic\ Pressure\ (Q) = \frac{1}{2} \rho V^2 " >}}

The SI unit for pressure is the pascal. One pascal is the pressure exerted by a force of magnitude
 of one newton perpendicularly upon an area of one square meter.

SpaceX provide a webcast of their launches which includes a simple telemetry display showing the 
rocket's current speed and altitude.

![image alt text](/spacexjcsat14webcast.png)

Using the International Standard Atmosphere model to lookup the density at each altitude reported in 
the telemetry and using the reported velocity at that point we can calculate the dynamic pressure for 
each telemetry point. Plotting the dynamic pressure for the telemetry points we'll be able to see at 
which point in terms of altitude and velocity the rocket experiences it's maximum dynamic pressure.

Here is a graph based on telemetry data from SpaceX's JCSAT-14 launch.

![image alt text](/spacex-jcsat14-standard-atmosphere.png)

The maximum dynamic pressure (Max-Q) experienced is roughly 30 kPa at an altitude of roughly 11.5 km 
while travelling at a speed of 1500 km/h.

As a comparison here is a graph for the Space Shuttle launch STS-124. The telemetry supplied also 
includes the throttle position, and you'll notice that the main engines of the Space Shuttle are actually 
throttled back significantly to 72% for a couple of seconds.

This is done to limit the maximum dynamic pressure that the Space Shuttle will need to handle during 
a launch.

![image alt text](/nasasts124standardatmosphere.png)

The maximum dynamic pressure experienced by the Space Shuttle is roughly 35 kPa at an altitude of roughly 
10.8 km and travelling at a speed of roughly 1550 km/h. So in the same ballpark in terms of altitude and 
speed and dynamic pressure as the SpaceX rocket.

You'll notice a kink in the velocity squared line at around about the 40 km mark even though the main engine 
throttle percentage doesn't change. This is due to the separation of the two solid rocket boosters.

I thought it would be interesting to compare the maximum dynamic pressure experienced by an airliner. 
So I used some data from the Flightradar24 website that tracks ADS-B broadcast by airliners broadcasting 
their altitude, ground speed etc.

So assuming there isn't any significant wind I'm assuming that the ground speed matches the true airspeed. 
Then again using the International Standard Atmosphere (ISA) we can lookup the density for the specific 
altitude and use that to calculate the dynamic pressure.

![image alt text](/airlinerstandardatmosphere.png)

So it looks like the maximum dynamic pressure is experienced at cruising altitude and cruising speed and 
roughly peaks around 25 kPa. In other words an airliner's maximum dynamic pressure that it experiences is 
roughly in the same ball park as experienced by a SpaceX rocket and the Space Shuttle and the airliner experiences 
it at roughly the same altitude.

To get a feel for how much pressure 25 - 35 kPa is remember it's the equivalent to 25,000 - 35,000 {{< tex "\frac{N}{m^2}" >}}. 
Which is roughly 2,500 - 3,500 kg sitting on a 1 square meter surface.

Now the palm of your hand is roughly 10 x 10 cm, i.e. 0.01 {{< tex "m^2" >}}, so it's the equivalent of holding 25 - 35 kg 
in the palm of your hand.

