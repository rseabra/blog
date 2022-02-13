---
title: "OpenMoko NewRotate 0.5.0 ‘Lazy Edition’ is out!"
date: "2008-11-19"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

Hi,

I've just release a [new version of omnewrotate](http://omnewrotate.googlecode.com/files/omnewrotate-0.5.0.tar.gz) ([OpenPGP signature](http://omnewrotate.googlecode.com/files/omnewrotate-0.5.0.tar.gz.asc)), the 'Lazy Edition' because it uses so much less CPU than any version I did before. Oh, I forgot to mention it in the release commit, but at least with [FSO](http://wiki.openmoko.org/wiki/FSO) [M4](http://wiki.openmoko.org/wiki/OpenmokoFramework/Status_Update_5) I'm getting a very stable rotation BUT if the screen looks garbled, please wait a few seconds until the graphic user interface adjusts to the screen changes. I don't think I can do much about that...

From the [ChangeLog](http://code.google.com/p/omnewrotate/source/browse/tags/release-0.5.0/ChangeLog?r=12):

2008-11-19 - 0.5.0 - Lazy edition
        \* uses a second thread for reading the accellerometer packets
        \* drops Fabian's changes (not that they weren't good, just not
          needed any more)
        \* adds flags (look at display\_help() or ./rotate -h)
        \* drops packets with 0 value coordinates (I got bogus packets
          like that so I decided to drop them, if you feel you get good
          packets with 0 value, you can use '-0' as an argument to take
          them in account).
        \* top -d 1 -p PID shows 0.0% CPU usage (of omnewrotate) even
          during rotation
        \* seems to waste a little too much memory (some stuff could be
          done with one number and bitwise operations instead of several
          numbers, I wonder how much that will improve and if it's worth
          the effort...)
        \* only output outside of debug mode are real errors
