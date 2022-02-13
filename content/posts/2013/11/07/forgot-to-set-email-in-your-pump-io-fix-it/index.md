---
title: "Forgot to set email in your pump.io? Fix it!"
date: "2013-11-07"
categories: 
  - "mublog"
  - "free-sw"
tags: 
  - "pump-io"
  - "tips"
---

Pump.io is an awesome distributed/federated social network, but it's still green software and has many rough edges. One boring one is that when you're setting up your instance you _may_ run into the pitfall of not setting your email, and then after you posted more than you'd want to loose by resetting it... you can't enable requireEmail anymore because you'll be kept out of your own instance.

Sucks, _innit_? But there's a fix, all you need to do is add the **email** field to your user's data. In my example I'll be using **redis** so your millage may vary according to your choice of databank, but the idea is the same, just figure out what your particular case needs to do to implement the same idea.

You can get your user's data and fix it like this (note, lines broken for blog display):

redis your.ip.addr.ess:6379> get user:RuiSeabra
"{\\"nickname\\":\\"RuiSeabra\\",\\"updated\\":\\"2013-08-15T20:42:58Z\\",
   \\"published\\":\\"2013-08-15T20:42:58Z\\",\\"\_passwordHash\\":\\"haha",
   \\"profile\\":{\\"objectType\\":\\"person\\",
   \\"id\\":\\"acct:RuiSeabra@p.1407.org\\"}}"

redis your.ip.addr.ess:6379> set user:RuiSeabra
"{\\"nickname\\":\\"RuiSeabra\\",\\"updated\\":\\"2013-08-15T20:42:58Z\\",
   \\"published\\":\\"2013-08-15T20:42:58Z\\",\\"\_passwordHash\\":\\"haha",
   \\"profile\\":{\\"objectType\\":\\"person\\",
   \\"email\\":\\"my-rms-email@1407.org\\",
   \\"id\\":\\"acct:RuiSeabra@p.1407.org\\"}}"

So now it's fixed and you can re-enable requireEmail in your pump.io.json:

\[rms@pump ~\]$ sudo grep -i requir /etc/pump.io.json
    "requireEmail": true,
