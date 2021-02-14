---
title: "Virtual Earth Media Center Add In"
date: 2005-11-05T21:38:41+02:00
---

I've been playing around with a VirtualEarth HTML add-in for Windows Media Center. 
I've got a number of features lined up but I've been side tracked with other work 
so I've only got the basics implemented so far.

Remote control keys:
 
- **Panning** - use the arrow keys
- **Zooming** - use the channel +- keys
- **Map Style** - use the 1,2,3 keys to toggle map styles between road, aerial and hybrid

In addition since the text labels on the map have been sized for viewing on a regular 
monitor with a 2 foot experience I've added a local zoom option. Use the 4,5,6 remote 
control keys to change the zoom factor, especially if you're running MCE on a CRT TV.

To install download this small [zip file](http://www.thegreenbutton.com/community/download.aspx?id=1912&MessageID=140046).

The zip file contains:
 
- **MapControl.js** - standard VirtualEarth implementation from MSN
- **VirtualEarth.html** - MCE HTML add-in page with handlers for the remote control
- **VirtualEarthLogo.png** - logo to use in MCE
- **VirtualEarth.mcl** - MCE shortcut registration file


To install unzip to:
 
`%Documents and Settings%\All Users\Start Menu\Programs\Accessories\Media Center\Media Center Programs`
 
Or unzip to a directory of your choice and place a shortcut file in the directory above pointing to the VirtualEarth.mcl file.
 
For more details on using the VirtualEarth JavaScript API take a look at the 
[ViaVirtualEarth website](http://www.viavirtualearth.com/).