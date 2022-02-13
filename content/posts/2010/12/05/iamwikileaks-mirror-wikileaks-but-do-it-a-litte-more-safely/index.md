---
title: "#iamwikileaks Mirror #wikileaks, but do it a litte more safely…"
date: "2010-12-05"
categories: 
  - "society"
tags: 
  - "true-piracy"
  - "wikileaks"
---

[![](images/wlogo.png "wlogo")](http://blog.1407.org/wp-content/uploads/2010/12/wlogo.png)Wikileaks is, in my humble opinion, a laudable cause. [Even if you don't like Wikileaks because of what they do, there are reasons to defend them](http://blogs.computerworlduk.com/simon-says/2010/12/the-internets-voltaire-moment/index.htm) at such a time where they're being attacked by the powers that be.

It is why I decided to also be a mirror of their [mass mirroring project](http://213.251.145.96/mass-mirror.html) for as long as I can hold it. You should too, even if you don't like them :) At this time there are just over 76 sites, but that's actually very few mirrors if you're fighting the almighty owners of ICANN: the USA government.

However their instructions require you to take a huge leap of faith: not only the best way to do this mirror is with rsync via ssh, but also you would have to trust them to manage your Apache installation via a .htaccess file.

This isn't so good, so here's how to help them without surrendering everything...

1. Prepare the (ssh) account for user fubarwl (no, not my real user)
    1. I use OpenSSH with fairly restrictive configuration, but still I used a **Match User** to forbid any kind of forwarding
    2. At **~fubarwl/.ssh/authorized\_keys** I put **no-user-rc** at the beginning, just before their ssh-key
    3. I also did a **chattr -R +i ~fubarwl**
2. Install rssh ([useful hints on the setup here](http://davelozier.com/2008/11/16/chroot-sftp-ubuntu-hardy-amd64/))
    1. I don't use it for anything else, so in it's config I only enabled rsync support (just uncomment the line with **allowrsync**)
    2. I created a filesystem on a file with **dd if=/dev/zero of=wikileaks.img bs=1M count=4096** and mke2fs wikileaks.img and mount it at a designated path (henceforth **CHROOT**) with the following options: **defaults,loop,nodev,noatime,nodiratime**
    3. At this filesystem, I setup the root of rssh's chroot path.
    4. The chroot helper didn't do it's job properly for rsync, so I needed to copy some extra libs into CHROOT**/lib**: **libacl.so.1\*** , **libpopt.so.0\*** and **libattr.so.1\***
    5. Also had to copy **rsync** into CHROOT**/usr/bin**
    6. Created a CHROOT**/home/fubarwl** with permissions for that user
    7. Created a CHROOT**/etc/passwd** with only one entry for that user
3. Now it's possible to rsync files into that directory, and the remote user has no way (short of a chroot bug) to change his ~foobarwl/.ssh
4. Setup Apache
    
    <VirtualHost YourSite:80>
            ServerName YourSite
            ServerAdmin YourAdmin
    
            TransferLog logs/http-YourSite-access\_log
    
            ErrorLog logs/http-YourSite-error\_log
    
            DocumentRoot CHROOT/home/fubarwl
    
            BandWidthModule On
            BandWidth all YourLimit
    
            RewriteEngine On
    
            RewriteRule media/support.html  /support.html \[R=301,L\]
            RewriteRule media/about.html  /about.html \[R=301,L\]
    
            <Directory CHROOT/home/fubarwl>
                    AllowOverride None
            </Directory>
    </VirtualHost>
    
5. Tell wikileaks your hostname, user (fubarwl) and path /home/fubarwl
