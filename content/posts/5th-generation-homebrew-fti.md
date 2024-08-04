---
title: "5th Generation Homebrew FTI"
date: 2022-03-26T19:23:40+02:00
---

The very first generation was described in my [Geeks and Fast Jets](https://seanmcleod.github.io/2008/06/geeks-and-fast-jets/)
post. Generations 2, 3 and 4 were described in the [Homebrew FTI](https://seanmcleod.github.io/2018/02/homebrew-fti/) post.
This post describes the 5th generation of the FTI system.

One of the reasons for a new generation was because the price of the Rockwell-Collins ADAHRS+GPS unit had
shot up from an original price of $5,500 to $12,000 in the intervening years since the 4th generation
unit was developed. One of the potential replacement AHRS+GPS units we looked at was the 
[VectorNav VN-200](https://www.vectornav.com/products/detail/vn-200) unit. These units were used in the
Red Bull Air Race aircraft. Unlike the Rockwell-Collins unit they don't include air data inputs. So a 
separate air data unit would need to have been sourced and integrated.

## iLevil 3 AW

In the end we ended up using a customised version of the [iLevil 3 AW](https://shop.levil.com/products/ilevil-3-aw)
unit. 

![image alt text](/images/5th-generation-homebrew-fti/ilevil.png)

The iLevil 3 AW unit includes the following components:

- AHRS
- Air Data
- GPS
- Serial ports
- WiFi

The data is transmitted over WiFi, with the AHRS data and air data at 14Hz and the GPS data at 5Hz. We received a customised
version of the iLevil software that outputs some of the sensor data that the iLevil unit doesn't typically output, 
e.g. angular rate data from the gyros, and also packages up all the output data into a single packet.

Before switching to using the iLevil unit we did some test flights with both the iLevil unit and the Rockwell-Collins
unit mounted in an Extra-300 aircraft at the same time and compared their output.

![image alt text](/images/5th-generation-homebrew-fti/ilevil-vs-rockwell-collins.png)

## DAQ Unit

In order to include the measurement of other FTI data like control positions, control forces etc. we developed a custom
DAQ (Data Acquisition Unit) which supports 16 analog channels and 4 discrete channels and a serial port. Liam Clark designed
and developed the DAQ unit. The analog and discrete channels are sampled by the DAQ unit and the data is then bundled
in a data packet and sent to the iLevil unit via a serial connection. The iLevil unit then broadcasts this data packet
via it's WiFi Access Point (AP). 

The DAQ unit includes a second serial connection allowing the connection of other sensors that output digital serial data.
This data is then also forwarded to the iLevil unit for broadcast via the WiFi AP.

The photo below shows a DAQ unit on my desk connected to the test harness board which includes 16 analog potentiometers and
4 discrete inputs for testing, in addition to providing access to the serial input option and all connected to the 
iLevil unit.

![image alt text](/images/5th-generation-homebrew-fti/hardware-setup.jpg)

DAQ unit up close, using an STM32F405RGTx MCU and an Analog Devices AD7490 16-channel 12-bit ADC.

![image alt text](/images/5th-generation-homebrew-fti/daq-upclose.jpg)

## Portable FTI

An updated portable FTI application was developed to run on iPhone and iPad devices. The application connects to the iLevil's
WiFi AP and records the data packets transmitted and provides the ability to design custom FTI displays for use in the cockpit
during test flights.

The test pilot and/or flight test engineer can design multiple displays, customised for particular types of tests. Starting
off with a blank display a combination of graphical gauges, line graphs and digital displays can be added, positioned via
dragging and sized. A particular parameter can then be selected from the set of available parameters from both the ADAHRS+GPS
data as well as from the configured analog and discrete inputs.

##### Sample Displays

![image alt text](/images/5th-generation-homebrew-fti/portable-fti-display-0.png)

![image alt text](/images/5th-generation-homebrew-fti/portable-fti-display-1.png)

Rotary gauge configured for a couple of different sensor inputs showing a number of the configuration options in terms of
tick marks, colour segments, bug display and the option to display min/max values recorded.

![image alt text](/images/5th-generation-homebrew-fti/rotary-gauges.png)

##### Configuration and Calibration

For each aircraft that the DAQ unit is installed in the test pilot needs to configure and calibrate the analog inputs
that have been installed in the particular aircraft.

![image alt text](/images/5th-generation-homebrew-fti/configuration-calibration.png)

## Overall Schematic

![image alt text](/images/5th-generation-homebrew-fti/fti-overview-schematic.png)

