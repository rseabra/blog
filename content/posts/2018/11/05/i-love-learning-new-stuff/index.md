---
title: "I love learning new stuff"
date: "2018-11-05"
categories: 
  - "me"
---

Really! Learning new stuff is always good to improve yourself, even when it's something so boring as accounting (well, this one I need to help myself believe it).

This is definitely not news for many people, but I always wondered how failban was blocking an ip.ad.dre.ss when I couldn't find any of the banned IPs with iptables-save | grep ip.ad.dre.ss

I always left it for another time and boy did it pass long and quickly, with other things more important.

But no more! This past weekend I finally learned how [fail2ban](https://www.fail2ban.org/) manages IP block lists with Firewalld: it uses [ipset](http://ipset.netfilter.org/) and then creates iptables multiport matches on **that** defined ipset!

Boy, was I happy... May come in useful in the future, and in the past it was definitely very useful at times, rather than other workarounds.

Still... nice. I must thrive to make time to learn new stuff at least every weekend.
