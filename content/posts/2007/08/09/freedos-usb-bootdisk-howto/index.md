---
title: "FreeDOS usb bootdisk HOWTO"
date: "2007-08-09"
tags: 
  - "free-sw"
  - "tips"
---

I wanted to upgrade my BIOS, but I only want to use Free Software. Right now, the only exception I have to do is the BIOS for which I don't have much choice there. But I want to avoid MS-DOS if I can, so I investigated how to get FreeDOS to boot on an USB disk. Success! It worked. Here's what I did.

### Partitioning the usb stick

In my case, the USB disk was `/dev/sdb`, so I launched parted in order to prepare the boot disk. Since I have a 64MB usb drive lying around, I'll use it. You may need to replace fat16 by fat32 if you want to use way bigger partitions:

\[root@roque ~\]# parted /dev/sdb mklabel msdos
Warning: The existing disk label on /dev/sdb will be destroyed and all data on
this disk will be lost. Do you want to continue?
Yes/No? yes
New disk label type?  \[msdos\]?
Information: Don't forget to update /etc/fstab, if necessary.

\[root@roque ~\]# parted /dev/sdb print
Model: FlashDis Flash Disk (scsi)
Disk /dev/sdb: 65.5MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start  End  Size  Type  File system  Flags

Information: Don't forget to update /etc/fstab, if necessary.

\[root@roque ~\]# parted /dev/sdb mkpart primary fat16 0 64MB
\[root@roque ~\]# parted /dev/sdb toggle 1 boot

Pay attention that if you see `Partition Table: loop` then beware, since it doesn't support bootable flag, so you really need to run the `mklabel` part in order to change it to msdos. After that, you'll need to make a partition as well.

### Installing a boot loader

While a friend was trying at the same time to use syslinux, I tried grub, but it still needed some help from a syslinux file, memdisk :). Here's how I did it:

mount /dev/sdb1 /mnt
cp -r /boot/grub /mnt
cp /usr/lib/syslinux/memdisk /mnt
cd /mnt/grub
echo '(hd0)     /dev/sda' > device.map
cat < grub.conf
default=0
timeout=10
bootsplash=/grub/splash.xpm.gz
root=(hd0,0)
title FreeDOS
        kernel /memdisk
        initrd /fdodin06.144

EOF
cd ..
wget -c http://odin.fdos.org/fdodin06.bin.zip
unzip fdodin06.bin.zip fdodin06.144 
Archive:  fdodin06.bin.zip
  inflating: fdodin06.144 

Now we need to put grub into the MBR (master boot record), this is how I did it:

grub> find /grub/stage1
find /grub/stage1
 (hd0,0)
 (hd1,0)

There's two of them. That's not good, is it? No, it's in fact quite normal. The first one is from /dev/sda, my main hard disk. You'll have to go to the correct partition though:

grub> root (hd1,0)
root (hd1,0)
 Filesystem type is fat, partition type 0xe
grub> setup (hd1)
setup (hd1)
 Checking if "/boot/grub/stage1" exists... no
 Checking if "/grub/stage1" exists... yes
 Checking if "/grub/stage2" exists... yes
 Checking if "/grub/fat\_stage1\_5" exists... yes
 Running "embed /grub/fat\_stage1\_5 (hd1)"... failed (this is not fatal)
 Running "embed /grub/fat\_stage1\_5 (hd1,0)"... failed (this is not fatal)
 Running "install /grub/stage1 (hd1) /grub/stage2 p /grub/grub.conf "... succeeded
Done.

Now it will boot from the usb drive, and launch grub.

### boot and test

So I guess this is your final stage... place what you need to run in the usb stick, unmount it and there you go!

Now you can use that pesty BIOS upgrade proprietary crap.

### References

- [How to make a USB stick bootable](http://www.mayrhofer.eu.org/Default.aspx?pageindex=6&pageid=45), by Rene Mayrhofer
- [GRUB tips and tricks](http://www.freesoftwaremagazine.com/articles/grub_intro/), by Jeremy Turner
- [FreeDOS images](http://odin.fdos.org/) from Odin
