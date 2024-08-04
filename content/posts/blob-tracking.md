---
title: "Blob Tracking"
date: 2018-05-19T23:05:27+02:00
---

The standard method of tracking the aircraft's control positions as the pilot moves the 
controls for flight test instrumentation (FTI) purposes is to attach string potentiometers 
(string pots) to the control cables/rods. As the control cable/rod moves based on the pilot's 
inputs a spring loaded thin steel wire is reeled in or out of the string pot. The mechanical 
movement of the reel changes the electrical resistance resulting in a change in voltage output 
which is then measured and recorded by the FTI system.

![image alt text](/images/camera-tracking-of-aircraft-control-positions/stringpot1.png)

In some cases though it would be ideal if you could track the aircraft control positions without 
having to physically attach a wire to the control cable/rod. So I developed a system to use
computer vision techniques to track a coloured blob that had been mounted on the inceptor by 
processing a recorded video.

In the video frame below you can see that I've placed a red Coca-Cola cap on top of the helicopter's 
cyclic, while I'm holding a GoPro camera above my head. I've gone through a calibration routine
to mark the center position of the cyclic, the little green cross and I've performed a full 
deflection of the cyclic across it's complete range of motion. Which results in the green box,
depicting the maximum range of the cyclic. Lastly, the yellow rectangle shows the currently 
detected blob.

![image alt text](/images/blob-tracking/gopro-blob1.jpg)

After flight the video is downloaded from the GoPro and the Blob Tracking application is used for
calibration and processing of the video. In order to synchronize the FTI flight data that has been 
recorded with the control positions that are derived from processing the recorded video a time 
synchronization has to be performed. This is done by holding the FTI tablet in front of the camera
before take-off for a couple of seconds while the FTI tablet application displays the current FTI timestamp. 
The video is then paused while it's displaying the current FTI timestamp which is then entered into 
application which uses it to synchornoze the FTI time and the video time.

![image alt text](/images/blob-tracking/blob-calibrate-sync.png)

The Blob Tracking application is also used to set the video tracking parameters based on a min-max
range of HSV values to ideally filter out only the target Coca-Cola bottle cap. A min-max size is also
specified to help in filtering.

During video processing each video frame is converted into the HSV colour space and all the pixels are
filtered based on the min-max HSV values that were specified to return a binary image consisting of white
pixels that match. An OpenCV blob detector is then used to find blobs in the resulting binary image, within 
the maximum control range area in the video that was specified, and finally filtered based on the min-max
blob size.

The screenshot below shows the final combined output combining the FTI data with the processed control positions
that were recovered via the video recording. The video recording can also be displayed in sync with the FTI
data within the FTI Flight Test Playback application.

![image alt text](/images/blob-tracking/blob-playback.png)
