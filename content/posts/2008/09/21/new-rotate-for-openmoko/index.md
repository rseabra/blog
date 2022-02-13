---
title: "New Rotate for OpenMoko"
date: "2008-09-21"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

As said before, since I'm not entirely happy with the previous version of Rotate for OpenMoko, also using it as a way to learn how to write programs for it, I'm [writing a new version](http://blog.1407.org/2008/09/21/getting-ready-for-rotate-rewrite/) of Rotate for OpenMoko.

I'm now announcing the first results: [release 0.1.0](http://files.1407.org/openmoko/rotate/rotate-0.1.0.tar.gz) is out ([signature](http://files.1407.org/openmoko/rotate/rotate-0.1.0.tar.gz.asc))! The tar.gz file contains both source and a binary suited to run on Om200x.y (at least 2008.9 should work).

Be careful, it bytes.. :)

$ cat ChangeLog
2008-09-21 - 0.1.0 - First release.
	Current Features:
	\* makes some rotations

	Known Issues:
	\* reading from the accelerometer hangs after X time/reads
	\* some heuristic values may need finetunning (specially when
	  laying around, turned up)

	Near Future:
	\* don't rotate when screen is locked
	\* change profile to silent/meeting when phone is turned down
	  and revert when it is turned back up
