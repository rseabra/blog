---
title: "OpenMoko Rotate 0.2.1"
date: "2008-09-22"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

Yes, it's out, release early, release often, yadada yadada. I'm grumpy because of less sleep time than usual, and a whole day of ITIL Foundation V3 lesson (3 more days of it, plus an exam later on).

Get it here: [rotate-0.2.1.tar.gz](http://files.1407.org/openmoko/rotate/rotate-0.2.1.tar.gz) ([signature](http://files.1407.org/openmoko/rotate/rotate-0.2.1.tar.gz.asc))

Anyway, here's the good news:

$ head -5 ChangeLog
2008-09-22 - 0.2.1
        \* more heuristic fixes (hopefully really fix when laying around, and
          turned up)
        \* workaround with alarm() for the accelerometer read-hang problem
        \* sleeping for 100ms seems to get cpu usage quite low (0% to 0.9%)
