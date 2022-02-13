---
title: "Mind your webserver's timeout! #owncloud"
date: "2014-08-07"
categories: 
  - "free-sw"
tags: 
  - "owncloud"
---

When [Owncloud](https://owncloud.org/) 7.0.0 came out I tried to upgrade my 6.0.4 instance and failed miserably and silently.

When 7.0.1 came out, the same thing happened, but this time I happened to notice the HTTP Result Code 502, timout... that was happenning in the frontend and not in the instance, for some reason I didn't think of looking there first (maybe because I only did it very late both times).

So I increased Apache's TimeOut directive to a safe 900 seconds and now everything went fine.

Meanwhile, Björn Schießle from Owncloud gave me a very nice tip, for those who control the server and can ssh into it, one can do the upgrade with:

> ./occ upgrade

So there you go, nice and useful tips, two in one post. :)
