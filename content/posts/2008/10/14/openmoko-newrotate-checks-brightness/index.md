---
title: "OpenMoko newRotate checks brightness"
date: "2008-10-14"
categories: 
  - "free-sw"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

Oscar Casamitja patched the old rotate program to change brightness on rotate in order to better hide xrandr's artifacts. That's actually a **very good idea**.

This new version reads from **actual\_brightness** and set into **brightness**, which you can find in /sys/class/backlight/pcf50633-bl/ , in order to skip packet reading when the screen is dimmed, which is the next best thing to checking wether the screen is locked.

I run into a problem, though: it seems that if I open() actual\_brightness once, I never again read an updated value, which makes me have to read on every loop :(

Enough talk, get it here: [rotate-0.3.0.tar.gz](http://files.1407.org/openmoko/rotate/rotate-0.3.0.tar.gz) ([ascii sig](http://files.1407.org/openmoko/rotate/rotate-0.3.0.tar.gz.asc)) \[now, if only [this bug](https://admin-trac.openmoko.org/trac/ticket/1563) was fixed on [projects.openmoko.org](http://projects.openmoko.org/)...\]

Hope you're enjoying it... :)

$ head -2 ChangeLog
2008-10-14 - 0.3.0
	\* dims while rotating and doesn't rotate if dimmed, sleeping for 5s
$ cat KNOWN\_ISSUES
Known Issues:
	\* I'm not getting updated results if I only open
	  /sys/class/backlight/pcf50633-bl/actual\_brightness once
	  which means I need to open it on every cycle.
	  Since it's in memory and not an actual file, wast should
	  not be too much
	\* some heuristic values may need fine tunning
