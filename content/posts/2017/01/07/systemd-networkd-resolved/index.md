---
title: "Simple experiment with systemd-networkd and systemd-resolved"
date: "2017-01-07"
categories: 
  - "how-to"
tags: 
  - "free-sw"
  - "networkd"
  - "resolved"
  - "systemd"
---

In my previous post, I wrote about how simple it was to create [containers with systemd-nspawn](https://blog.1407.org/2017/01/07/systemd-nspawn-experiment/).

But what if you wanted to expose to the outside network to a container? The rest of the world can't add mymachines to /etc/nsswitch.conf and expect it to work, right?

And what if you were trying to reduce the installed dependencies in an operating system using systemd?

Enter **systemd-networkd** and **systemd-resolved**...

**Firstly**, this Fedora 25 host is a kvm guest so I added a new network interface for "service" were I created the bridge (yes, with nmcli, why not learn it as well on the way?)

nmcli con add type bridge con-name Containers ifname Containers
nmcli con add type ethernet con-name br-slave-1 ifname ens8 master Containers
nmcli con up Containers

**Then**, in container test, I configured a rule to use DHCP (and left in a modicum of a template for static addresses, no... that's not my network) and replaced /etc/resolve.conf with a symlink to the file systemd-resolved manages:

cat <<EOF > /etc/systemd/network/20-default.network
\[Match\]
Name=host0

\[Network\]
DHCP=yes
# or swap the above line by the lines below:
#Address=192.168.10.100/24
#Gateway=192.168.10.1
#DNS=8.8.8.8
EOF

rm /etc/resolv.conf
ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

**Finally**, I enabled and started networkd and resolved:

systemctl enable systemd-networkd
systemctl enable systemd-resolved
systemctl start systemd-networkd
systemctl start systemd-resolved

A few seconds later...

\-bash-4.3# ip addr list dev host0
2: host0@if29: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state LOWERLAYERDOWN group default qlen 1000
 link/ether 06:14:9c:9e:ac:ca brd ff:ff:ff:ff:ff:ff link-netnsid 0
 inet 192.168.10.92/24 brd 192.168.10.255 scope global host0
 valid\_lft forever preferred\_lft forever

-bash-4.3# cat /etc/resolv.conf 
# This file is managed by systemd-resolved(8). Do not edit.
#
# This is a dynamic resolv.conf file for connecting local clients directly to
# all known DNS servers.
#
# Third party programs must not access this file directly, but only through the
# symlink at /etc/resolv.conf. To manage resolv.conf(5) in a different way,
# replace this symlink by a static file or a different symlink.
#
# See systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 192.168.10.1

Happy hacking!
