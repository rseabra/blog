---
title: "OpenMoko Rotate now using libxrandr"
date: "2008-09-20"
categories: 
  - "free-sw"
  - "omnewrotate"
tags: 
  - "code"
  - "free-sw"
  - "openmoko"
  - "rotate"
---

As I peeked into the code of OpenMoko's [Rotate](http://wiki.openmoko.org/wiki/Rotate) (a program that rotates the screen acording to the current tilt), I noticed it made use of _system_ to launch the xrandr program with appropriate arguments.

Well, system costs a lot in terms of processing power, not to mention launching another program, and that means even less battery time. I didn't like that, so I wrote a [patch](http://files.1407.org/2008/09/20/rotate_libxrandr.patch) that alters the current [rotate.c](http://github.com/cjb/freerunner-rotate/tree/master/rotate.c?raw=true) into a new [rotate.c](http://files.1407.org/2008/09/20/rotate.c) in order to use librandr and get it to rotate the screen without the costly system+xrandr duo from hell.

I also built a [binary of rotate](http://files.1407.org/2008/09/20/rotate), which you can download from this link and place on your OpenMoko Neo Freerunner with 2008.8 or 2008.9 (I haven't the foggiest idea if it works on other versions).

Hopefully, you might want to verify the sha1sums:

\-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

afc833b7cd2c874c1c815a0cb9f7c38a65998ff5  rotate
efcc6277080b2aadc3306a000a97ab202ca2bece  rotate.c
c1eb847d05cd36e0e9f31b5e5f6eb9337f730d0f  rotate\_libxrandr.patch
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.6 (GNU/Linux)

iD8DBQFI1ES1o+C50no0+t4RAjSrAJ41N0KpD7JaY3WfiRViexn4CvQw7QCePNr3
G8Z3ejIwprpK7J7unjMaS1A=
=anNm
-----END PGP SIGNATURE-----

I realise the way I wrote didn't make it very obvious, so here's a listing of the files:

- [rotate](http://files.1407.org/2008/09/20/rotate)
- [rotate.c](http://files.1407.org/2008/09/20/rotate.c)
- [rotate\_libxrandr.patch](http://files.1407.org/2008/09/20/rotate_libxrandr.patch)
- [sha1sums.asc](http://files.1407.org/2008/09/20/sha1sums.asc)
