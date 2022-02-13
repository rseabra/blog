---
title: "So elmdentica works with https!"
date: "2010-02-14"
categories: 
  - "elmdentica"
  - "free-sw"
tags: 
  - "elmdentica"
  - "openmoko"
---

It seems the problem with those weird libcurl errors when you enabled the secure option (basically https) is that the ca certificate bundle is missing in SHR's OE build (perhaps it's on all OE builds, don't know).

There is, fortunately, an easy way to fix it (as mentioned in the openmoko [communiy list](http://lists.openmoko.org/pipermail/community/2010-February/060203.html)).

All you need to do is copy your own ca certificate bundle (in Fedora it's **/etc/pki/tls/certs/ca-bundle.crt** ) into the proper place for OE's path: **/etc/ssl/certs/ca-certificates.crt**

So now you can enable secure, rather than faster :)
