---
title: "Portuguese dictionary for OpenMoko’s Illume keyboard"
date: "2008-10-13"
categories: 
  - "free-sw"
tags: 
  - "dictionary"
  - "openmoko"
  - "portuguese"
---

Hi, taking advantage of a [word list composed from one million words of a Portuguese newspaper](http://www.linguateca.pt/acesso/tokens/formas.cetempublicoprmi.txt), I filtered, and filtered and filtered the garbage (and I have a strong idea it still has a lot of garbage), to generate a Portuguese dictionary for OpenMoko's Illume keyboard.

Since UTF-8 support is still borked, I have replaced special characters like **é** with a plain **e**. Yeah, it's like using an US keyboard for writing Portuguese, but one's gotta work with the eggs one has in order to make an omelet.

Enjoy: [Portuguese (ASCII).dic](http://files.1407.org/openmoko/portuguese/Portuguese%20(ASCII).dic-0.1.0.bz2)

Just do:

bunzip2 "Portuguese (ASCII)-0.1.0.dic.bz2"
scp "[Portuguese (ASCII)-0.1.0.dic"](http://files.1407.org/openmoko/portuguese/Portuguese%20(ASCII).dic-0.1.0.bz2) root@192.168.0.202:Portuguese\\ \\(ASCII\\).dic
ssh root@192.168.0.202
mv Portuguese\\ \\(ASCII\\).dic \\
   /usr/lib/enlightenment/modules/illume/dicts/Portuguese\\ \\(ASCII\\).dic

With a lot of thanks to Alberto Simões for pointing me to [http://www.linguateca.pt/ACDC/](http://www.linguateca.pt/ACDC/) and Rasterman for the hints about the (quite simple) file format.
