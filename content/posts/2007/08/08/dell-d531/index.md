---
title: "Dell D531"
date: "2007-08-08"
tags: 
  - "free-sw"
---

Este artigo segue em inglês para o propor para inclusão no [TuxMobile](http://www.tuxmobile.org/), e refere-se à instalação de um GNU/Linux, neste caso o Fedora 7, num Dell D531.

**UPDATE**: sound works now, graphics card too is for really Real Soon Now!

[![Article listed at TuxMobil - Linux on Laptops, Notebooks, PDAs and Mobile Phones](images/WritingPenguin_left.png)](http://tuxmobil.org/dell.html) So I got this Dell D531, it's got a dual core AMD Turion™ 64 X2 Mobile Technology TL-60 CPU, an ATI X1200, bluetooth support, a wifi card, etc. Since I chose to only use [Software Livre](http://www.fsf.org/philosophy/free-sw.html), I had to figure out how to make it work best without using proprietary drivers. The other option was an HP virtually fully supported laptop, but since HP had some problems to give my employer over 20 laptops, suddenly Dell won, and I got one that has so-so support. AMD has bought ATI, though, and promised to help make things better, but if it isn't releasing the ATI drivers... then it's a worthless promise. and after a bit more than one year, [the specs have been published](http://www.x.org/docs/AMD/). Here's to a fully working card with the RadeonHD driver, real soon now! :)

Anyways, I had some trouble finding a popular distribution optimized for AMD64 which could be installed, I firstly tried Ubuntu, but for some reason only Gutsy Tribe 2 installed. It was in a too early development period, and I really need a working, reasonably stable laptop. Also, the native wifi card isn't well supported with the bcm43xx drivers and seems to need some voodoo firmware, so I decided to turn it off in the BIOS.

Fedora 7 for AMD64 did install properly, although it had some quircks... and so starts the technical part of this story.

### Obtaining install media

This was an adventure in itselft. It appears Fedora 7 Live for AMD64 doesn't fit on 800MB CDs. Fortunately [it can be loaded onto a pen-drive](http://fedoraproject.org/wiki/FedoraLiveCD/LiveCDHowTo#head-70a9d63d4db991d7d27890ae137e817efa552c98), and then boot and install from it. It's actually much faster than from CD, so I definitely recommend pen-drives for install media.

### Installing

Fedora 7's install process is quite simple, as most modern GNU/Linux distrubutions, and you will have a reasonably straightforward and pain-free installation if you merely clear the whole disk and install (which is what I did since I don't want closed Windows around).

One big advantage over Gutsy Tribe 2 is that it did detect the graphics card. Although, ATI X1200 is not fully supported, but the VESA driver was adequately loaded and I had a 1024x768 desktop. Yeah, it sucks, the display is for 1280x800 so things are a bit streched out, but hey, complain to ATI. They're the culprits. Here's to hoping the aforementioned promise isn't worthless!

### What Works

- Suspend to memory sometimes works
- Suspend to disk has always worked for me, so far
- Bluetooth is supported
- Ethernet wired card is supported
- My older ralink PCMCIA wifi-card is supported
- Virtualization support in CPU works
- Burning CDs (alas, no DVD writing support in the optical drive \*sigh\*)
- Sound works since [alsa-driver 1.0.15rc1](ftp://ftp.alsa-project.org/pub/driver/alsa-driver-1.0.15rc1.tar.bz2). It doesn't work on most distributions yet since they have the latest stable version (1.0.14), but end of the 2007 onwards distributions should work out of the box
- Most 2D support (full resolution, RandR 1.2, etc... but no acceleration)

### What DOESN'T work

- Suspend to memory in a reliable form (but [maybe that's Linux's fault](http://www.google.com/search?q=kernel+trap+linux+suspend))
- The natife wifi-card
- Full 2D and 3D graphics card support (I'd be happy with full 2D support)
- Battery life is shorter, my colleagues at work claim almost 8 hours when idle, I got a little more than 6 hours when idle. Still, a huge improvement, since the previous laptop only lasted about 2 hours on the first 6 months :)

### Expectations

AMD has promised to help solving the ATI issue. I hear there's a huge internal war, but the loss of big contracts (hundreds of thousands of computers) that has already happened because AMD laptops with ATI aren't fully supported with Software Livre is probably a significant incentive for things to change in the near future.

The hda-intel Azalia sound card has had many patches recently so, hopefully, when Fedora rebases to 2.6.23 Linux I might have sound.

It seems some successful work is going on with the bcm43xx driver, so maybe in the future I won't need the ralink PCMCIA card (one major problem is less battery life as PCMCIA cards drain more power).

There's a lot of recent work on power efficiency. Even though it's focused on Intel computers, I'm sure a lot of it will also benefit AMD based computers.

### Conclusion

All in all it's a good (and nice looking) laptop, but has some major problems if you only want to use Software Livre like I do. Things may improve, though, and I may revise this article in the future.
