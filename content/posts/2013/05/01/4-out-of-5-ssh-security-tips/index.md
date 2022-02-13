---
title: "4 (out of 5) ssh security tips"
date: "2013-05-01"
categories: 
  - "free-sw"
tags: 
  - "security"
  - "ssh"
  - "tips"
---

There are some security tips for your sshd\_config at [http://www.debian-tutorials.com/5-steps-to-secure-your-ssh-server](http://www.debian-tutorials.com/5-steps-to-secure-your-ssh-server "5 Steps to Secure your SSH Server") however the third one, [Change the SSH Port on the server](http://www.debian-tutorials.com/5-steps-to-secure-your-ssh-server#3_Change_the_SSH_Port_on_the_server "Change the SSH Port on the server"), is a lot of hot air.

> "By changing the default port you will make SSH server more secure. By changing the default port you will reduce the amount of brute force attacks."

Only the second phrase of this statement is truthful, but still, not by a wide margin...

Security by obscurity never works, it's better to follow the other 4 advices and use fail2ban or something similar.
