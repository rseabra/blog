---
title: "XBMC for Fedora 11"
date: "2009-06-11"
categories: 
  - "free-sw"
tags: 
  - "fedora"
  - "leonidas"
  - "xbmc"
---

Ok, not yet RPMS but these instructions should work flawlessly as is on Fedora 11.

Firstly, you should [add the rpmfusion repositories](http://rpmfusion.org/Configuration) to your machine, then install a _few_ packages so your build will work:

sudo yum -y install \\
        SDL\* glew glew-devel libmad-devel tre tre-devel \\
        libogg libogg-devel libvorbis libvorbis-devel \\
        boost boost-devel bzip2-devel bzip2-libs fribidi\* \\
        lzo lzo-devel mysql-libs mysql-devel jasper jasper-devel \\
        faac faac-devel enca enca-devel hal hal-devel hal-libs \\
        cmake gperf nasm libXmu-devel fontconfig-devel \\
        freetype-devel libXinerama-devel pcre-devel gcc-c++ \\
        sqlite-devel curl-devel libsamplerate-devel libcdio-devel \\
        pulseaudio-libs-devel avahi-devel ffmpeg-devel libmad-devel \\
        a52dec-devel libdca faad2-devel libmpeg2-devel libass-devel \\
        libvorbis-devel libogg-devel libmpcdec-devel flac-devel \\
        wavpack-devel python-devel subversion

This will allow for a lot of the dependencies to be made external, which is a good thing!

Now, to fetch the repository of XBMC (well, let's use the latest, but theses instructions should work with a stable release source package):

mkdir ~/svn ; cd ~/svn
svn co http://xbmc.svn.sourceforge.net/svnroot/xbmc/branches/linuxport/ xbmc

It will take a short while to fetch everything, depending on your connection, you may even be better off having a coffee or some tea.

Now you should go into the  ~/svn/xbmc/XBMC/ directory and run configure. My run installs xbmc on /opt/xbmc and enables some external dependencies. Unfortunately, even with the required dependencies some of the options need changes not yet available in the official packages, so we'll be using some internal versions instead. Don't worry about it, we'll just specify the ones which will be external.

Unfortunately, mysql-libs doesn't supply a "generic" path for the shared object file, so we'll also need to "hack" its existence before running xbmc's configure:

sudo ln -s /usr/lib/mysql/libmysqlclient.so.16.0.0 /usr/lib/libmysqlclient.so

./configure --prefix=/opt/xbmc \\
  --enable-external-libmad \\
  --enable-external-liba52 \\
  --enable-external-libmpeg2 \\
  --enable-external-libass \\
  --enable-external-libvorbis \\
  --enable-external-libogg \\
  --enable-external-libmpcdec \\
  --enable-external-libflac \\
  --enable-external-libwavpack \\
  --enable-external-python \\

This will result in the following output, at the end:

\------------------------
  XBMC Configuration:
------------------------
  Debugging:    Yes
  Profiling:    No
  Optimization: Yes
  OpenGL:       Yes
  VDPAU:        No
  Joystick:     Yes
  XRandR:       Yes
  PCRE Support: Yes
  MID Support:  No
  ccache:       No
  PulseAudio:   Yes
  FAAC:         Yes
  DVDCSS:       Yes
  Avahi:        Yes
  External Libraries:   No
  External FFmpeg:      No
  External libmad:      Yes
  External liba52:      Yes
  External libdts:      No
  External libfaad:     No
  External libmpeg2:    Yes
  External libass:      Yes
  External libvorbis:   Yes
  External libogg:      Yes
  External libmpcdec:   Yes
  External libflac:     Yes
  External libwavpack:  Yes
  External Python:      Yes
  prefix:       /opt/xbmc
------------------------

Unfortunately, make failed due to some problem with accessing libjpeg internals. The official package doesn't contain all you need, so you have to use hack XBMC's code in order to force using the internal version of libjpeg:

make
In file included from tif\_ojpeg.c:35:
/usr/include/jpeglib.h:1096:55: error: jpegint.h: No such file or directory
tif\_ojpeg.c: In function ‘OJPEGPreDecode’:
tif\_ojpeg.c:1414: error: dereferencing pointer to incomplete type
tif\_ojpeg.c:1424: error: dereferencing pointer to incomplete type
tif\_ojpeg.c:1425: error: dereferencing pointer to incomplete type
tif\_ojpeg.c:1426: error: dereferencing pointer to incomplete type
tif\_ojpeg.c:1428: error: ‘DSTATE\_INHEADER’ undeclared (first use in this function)
tif\_ojpeg.c:1428: error: (Each undeclared identifier is reported only once
tif\_ojpeg.c:1428: error: for each function it appears in.)
tif\_ojpeg.c:1508: error: dereferencing pointer to incomplete type

Even though it looks awful, just [fix tif\_ojpeg with this patch file](http://files.1407.org/2009/06/11/fix_tif_ojpeg.patch) and run make again.

After this, you run **make install** to install into /opt/xbmc, and if you want to have an X session that launches XBMC automatically, then you can also add

sudo ln -s /opt/xbmc/share/xsessions/XBMC.desktop /usr/share/xsessions/

Now you can create a guest account and launch the computer automatically into that user, running XBMC.
