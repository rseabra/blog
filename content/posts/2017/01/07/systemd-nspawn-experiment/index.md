---
title: "Simple experiment with systemd-nspawn containers"
date: "2017-01-07"
categories: 
  - "how-to"
tags: 
  - "free-sw"
  - "nspawn"
  - "systemd"
---

For this test I used Fedora 25. Your mileage might vary in other operating systems, some things may be the same, some may not be.

**WARNING**: you'll need to disable selinux so to me this was merely an interesting experiment and it lead to increasing my knowledge, specially in relation to selinux + containers. Bad mix, no security, containers don't contain, etc.

**Many thanks** to the nice people from #fedora and #selinux that graciously lent their time to help me when I was trying to use nspawn with selinux enabled. With their help, specially Grift from #selinux, we were actually able to run it, but only in a way I'm so uncomfortable with that I ultimately considered this experiment to  be a #fail as I'm definitely not going to use them like that any time soon: there's still a lot of work to do in order to run containers with some security. I hope the Docker infatuation leads to an universal solution towards security + containers from the good engineers at Red Hat and others involved in that work.

But it certainly was a success in terms of contributing to more experience beyond a quickly expiring benefit of familiarity with OpenVZ.

Enough words, here's how simply it was...

**Firstly**, let's setup a template from which we're going to copy to new instances. As I'm using Fedora 25, I used DNF's capability to install under a directory:

dnf --releasever=25 \\
 --installroot=/var/lib/machines/template-fedora-25 \\
 -y install systemd passwd dnf fedora-release \\
 iproute less vi procps-ng tcpdump iputils

You'll only need the first three lines, though, the fourth was just a few more packaged I preferred to have in my template.

**Secondly**, you'll probably like to do further customization in your template, so you'll enter your container just like it was (well, is) an enhanced chroot:

cd /var/lib/machines
systemd-nspawn -D template-fedora-25

Now we have a console, and the sky is the limit for what you can setup, like for instance defining a default pasword for root with **passwd** (but maybe you'll not want to do this in a production environment).

For some weird reason, passwd constantly failed manipulating authentication tokens, but I solved it quickly by merely reinstalling passwd (_dnf -y reinstall passwd_). Meh...

I also ran dnf -y clean all before exiting the container in order to clean up unnecessary space wasted with package meta data that will be expired quickly.

When you're done customizing, exit the container with **ctrl + \]\]\]** in about a second.

**Finally**, we're ready to preserve the template:

cd template-fedora-25
tar --selinux --acls --xattrs czvf \\
    ../$(basename $( pwd ) )-$(date +%Y%m%d).tar.gz .
cd ..

**We're now ready** to create a test container and launch it in the background:

mkdir test
cd test
tar --selinux --acls -xattrs xzvf \\
    ../template-fedora-25-20170701.tar.gz
cd ..
machinectl start test

This container will probably not be able to run services exposed outside without help but you can login into its console with **machinectl login test**

You'll also have _automagic_ name resolution from your host computer to the containers it runs if you change the hosts entry in /etc/nsswitch.conf placing **mymachines** between files and dns (or as you see fit if otherwise in your setup):

hosts: files mymachines dns myhostname

If you had enable ssh in your container, you'd be able to do **ssh test** from the host machine. Or access a web server you installed in it. Who knows.

As you saw, despite a lot of words trying to explain every step of the way, it's excruciatingly simple.

The next article ([Simple experiment with systemd-networkd and systemd-resolved](https://blog.1407.org/2017/01/07/systemd-networkd-resolved/)) expands this example with a bridge in the host machine in order to allow your containers to talk directly with the external world.

Happy hacking!
