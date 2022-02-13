---
title: "OMNewRotate 0.5.3 is out!"
date: "2008-12-26"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

Today I released [omnewrotate](http://code.google.com/p/omnewrotate/) 0.5.3, which fixes [issue 4](http://code.google.com/p/omnewrotate/issues/detail?id=4&can=1).

As I was starting to investigate libframeworkd-glib, that dependency was a problem for usage in the [recently released Om2008.12](http://wiki.openmoko.org/wiki/Om_2008.12_Update) (basically, it wouldn't run at all).

As such, I added a "--without-frameworkd" to the ./configure script, which I used for building [the ipk of this release](http://omnewrotate.googlecode.com/files/omnewrotate_0.5.3-r0_armv4t.ipk) ([OpenPGP sig](http://omnewrotate.googlecode.com/files/omnewrotate_0.5.3-r0_armv4t.ipk.asc)).

Another good thing about this release, is that [its tar ball](http://omnewrotate.googlecode.com/files/omnewrotate-0.5.3.tar.gz) ([OpenPGP sig](http://omnewrotate.googlecode.com/files/omnewrotate-0.5.3.tar.gz.asc)) is now the result of make dist. This should be a great bonus for integration with [hackable:1](http://www.hackable1.org/), which is still using a pretty old version of omnewrotate. Just don't forget to include "--without-frameworkd" in the configure process (I plan to have this detection done automatically in the future).

Enjoy!
