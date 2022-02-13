---
title: "Starting OMNewRotate automatically"
date: "2008-11-26"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "openmoko"
  - "rotate"
  - "tips"
---

Following a [question from Leonti Bielski](http://lists.openmoko.org/pipermail/community/2008-November/036490.html) in the [OpenMoko Community Mailing List](http://lists.openmoko.org/mailman/listinfo/community), here's a tip on how to start OMNewRotate (or any other _rotate_ for that matter). Just execute the following (from the phone's terminal or from an SSH connection), and restart the xserver:

> echo '/home/root/rotate&' > /etc/X11/Xsession.d/89rotate
> chmod a+rx /etc/X11/Xsession.d/89rotate

[My first reply has a bug](http://lists.openmoko.org/pipermail/community/2008-November/036495.html), so maybe you should trust the above version better. I think Leonti caught it, since [it worked for him](http://lists.openmoko.org/pipermail/community/2008-November/036498.html) :)
