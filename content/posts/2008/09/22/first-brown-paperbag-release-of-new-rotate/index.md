---
title: "First brown paperbag release of new Rotate"
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

Oops, heuristics were bad, very bad. Still has quirks, but at least now they're not so shameful.

There's a new release: [0.1.1](http://files.1407.org/openmoko/rotate/rotate-0.1.1.tar.gz) ([signature](http://files.1407.org/openmoko/rotate/rotate-0.1.1.tar.gz.asc))

$ head -2 ChangeLog 
2008-09-21 - 0.1.1 - First brown paper bag release
	\* improves heuristics
$ cat KNOWN\_ISSUES 
Known Issues:
	\* reading from the accelerometer hangs after X time/reads
	\* some heuristic values may need finetunning (specially when
	  laying around, turned up)
