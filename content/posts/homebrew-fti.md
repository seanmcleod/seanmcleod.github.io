---
title: "Homebrew FTI"
date: 2018-02-17T23:50:07+02:00
---

I first got involved in designing FTI equipment in 2008 when TFASA (Test Flying Academy of South Africa) 
asked me to design some FTI equipment to be used in a Hawker Hunter jet that they were using for a course 
they were running. I did a write-up on this work in - [Geeks and Fast Jets](https://seanmcleod.github.io/2008/06/geeks-and-fast-jets/).

Subsequent to that work I developed a couple of follow up FTI units that TFASA have used over the years on 
various types of aircraft when running test pilot training courses.

The first FTI unit in the Hawker Hunter used a ruggedized PC as the FTI unit to collect data and log it 
from various sensors and to provide a real display in the cockpit.

For the follow-up unit which needed to be installed on much smaller aircraft where space, weight and 
power requirements were smaller I switched to a simple SBC (Single Board Computer) called the Fez Rhino. 
The Fez Rhino ran a small embedded version of the .Net (Common Language Runtime - CLR) runtime.

![image alt text](/images/homebrew-fti/fezrhino.png)

Sensors were connected via a combination of serial inputs and analog inputs. For a later iteration I switched 
to the Fez Hydra which was similar in terms of running an embedded version of .Net just with a slightly more 
powerful CPU and a different physical connector setup.

![image alt text](/images/homebrew-fti/fezhydra.png)

Here is a photo of one of the Fez Hydra based FTI units with a test harness to test the 16 analog inputs, 
6 digital inputs and 3 serial ports.

![image alt text](/images/homebrew-fti/fezhydrafti.png)

The one serial port was always connected to a Rockwell-Collins ADAHRS unit as shown below. The unit provided 
air data in terms of airspeed and pressure altitude plus attitude and heading (AHRS) information from a set 
of 3-axis gyros, accelerometers and magnetometers and in addition GPS information.

![image alt text](/images/homebrew-fti/rockwellcollinsadahrs.png)

Data was logged to an SD card for downloading after the flight and in-flight one of the serial ports could be 
connected to a Windows CE device called the Oudie to display real-time data and graphs to the test pilot instructor 
and student.

![image alt text](/images/homebrew-fti/oudie.png)

For the third and current iteration of the FTI package we wanted a more portable system that didn't need as much 
wiring to the ADAHRS+GPS sensor and not having to get power from the aircraft. This enables us to quickly install 
and remove the system from different aircraft.

Instead of using an off-the-shelf SBC like the Fez Hydra I contracted the design of a custom SBC from John Baxter 
who I knew via mutual work colleagues. He designed a custom PCB with an Amtel micro-CPU plus a battery charging 
circuit and a WiFi module.

The unit includes the Rockwell-Collins ADAHRS+GPS unit mounted inside our case on top of a lead plate plus 
rechargeable batteries and the custom SBC.

The portable FTI unit mounted in a Cessna C-172.

![image alt text](/images/homebrew-fti/portableftiunit.png)

The updated in-cockpit application now running on an Android based tablet receives the data via the WiFi connection to 
display the real-time data including graphs and to record the data for processing and playback after landing on a PC.

Some screenshots of the FTI app running on a tablet.

![image alt text](/images/homebrew-fti/portableftiapp1.png)

![image alt text](/images/homebrew-fti/portableftiapp2.png)

