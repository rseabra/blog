---
title: "HOWTO: pump.io behind Apache"
date: "2013-09-03"
categories: 
  - "free-sw"
tags: 
  - "pump-io"
  - "tips"
---

[Pump.io](http://pump.io/) is very interesting, but it used to be very hard to put to work behind a frontend, mostly because of web sockets and being designed to be directly connected.

This means that your nodejs-enabled pump.io consumed an IP:port pair and since pump.io is an https oriented application (can be run in http but you really don't want that) that means your https port (who has more than one IP either at home or his VPS?) is now BUSY with one single application... **sucks** and I gave up for some time and wasted my connection's IP address at the standard https port.

Meanwhile... Good news, everyone!

I recently came up a new Apache module for web sockets: [mod\_proxy\_wstunnel](http://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html).

Searching for pump.io and wstunnel... it turns out my _irrational_ friend Mark Jaroski also [published a note about that](https://i.rationa.li/mark/note/2TWATCchRQGyMA0RlvZSQA)! Please note that you may not need to build the module, if you have a recent enough Apache 2.4.x version it may already be there, check your bundled modules!

So here's my setup: the OpenWRT router forwards port 443 incoming into a frontend KVM guest running Apache httpd which then forwards to some of my sites, one of which is my pump at [https://p.1407.org/](https://p.1407.org/)

The frontend's web site looks like this:

<VirtualHost \*:443>
        ServerName p.1407.org
        CustomLog logs/https-p.1407.org-access\_log common
        ErrorLog logs/https-p.1407.org-error\_log
        DocumentRoot /var/www/html/default

        SSLEngine On
        SSLCertificateFile conf/ssl.crt/p.1407.org.crt
        SSLCertificateKeyFile conf/ssl.key/p.1407.org.key
        SSLCertificateChainFile conf/ssl.crt/startssl-chain.crt
        SSLCACertificateFile conf/ssl.crt/startssl-chain.crt

        SSLProxyEngine On

        <Location /main/realtime/sockjs>
                ProxyPass wss://192.168.x.y/main/realtime/sockjs
                ProxyPassReverse wss://192.168.x.y/main/realtime/sockjs
        </Location>

        <LocationMatch ".\*\\.(jpg|png|gif)$">
                CacheEnable disk
        </LocationMatch>

        ProxyPreserveHost On

        ProxyPass               /       https://192.168.x.y/
        ProxyPassReverse        /       https://192.168.x.y/
</VirtualHost>

And at my pump.io KVM guest, 192.168.x.y, I have...

{
    "driver":  "redis",
    "noweb":  false,
    "site":  "1407 Pump",
    "owner":  "Rui Seabra",
    "ownerURL":  "https://blog.1407.org/",
    "port":  443,
    "hostname":  "p.1407.org",
    "nologger":  false,
    "serverUser":  "pumpio",
    "key":  "/etc/pump.io/p.1407.org.key",
    "cert":  "/etc/pump.io/unified-p.1407.org.crt",
    "uploaddir": "/opt/pump.io/uploads",
    "logfile": "/var/log/pump.io/activity.json",
    "debugClient": false,
    "firehose": "ofirehose.com",
    "disableRegistration": true,
    "requireEmail": false,
    "smtpserver": "put.your.own.here",
    "smtpuser": "aLoginAtYourServer",
    "smtppass": "some good password",
    "smtpusetls": true,
    "smtpport": 587,
    "smtpfrom": "pump@1407.org",
    "secret": "some good secret"
}

So there you go...
