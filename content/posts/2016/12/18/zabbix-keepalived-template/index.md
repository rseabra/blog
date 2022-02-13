---
title: "Zabbix Keepalived template"
date: "2016-12-18"
categories: 
  - "how-to"
tags: 
  - "free-sw"
  - "keepalived"
  - "zabbix"
---

I'm cleaning up some templates I've done for Zabbix and publishing them [over here](https://github.com/rseabra/zabbix-templates). The [first one is Keepalived](https://github.com/rseabra/zabbix-templates/tree/master/keepalived) **as a load balancer**.

This template...

- requires no scripts placed on the server
- creates an application, Keepalived
- collects from the agent:
    - if it is a master
    - if it is an IPv4 router
    - the number of keepalived processes
- reports on
    - state changes (from master to backup or the reverse) as WARNING
    - backup server that's neither a router or has keepalived routing as HIGH (your redundancy is impacted)
    - master server that's neither a router nor has keepalived routing as DISASTER (your service will be impacted if there's an availability issue in one real server as nothing else will automatically let IPVS know of a different table)

I still haven't found a good way to report on the cluster other than creating triggers on hosts, though. Any ideas?

Up next is Postfix and, hopefully, IPVS Instance (not sure it can be done without scripts or writing an agent plugin, though. I haven't done it yet).
