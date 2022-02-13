---
title: "pump.io as systemd service"
date: "2013-09-05"
categories: 
  - "free-sw"
tags: 
  - "pump-io"
  - "systemd"
---

So what's wrong with this first very basic attempt to start pump.io as a systemd service?

\[Unit\]
Description=Pump.io
Requires=redis.service
After=redis.service

\[Service\]
Type=simple
ExecStart=/opt/pump.io/pump.io/bin/pump
Restart=on-abort

\[Install\]
WantedBy=multi-user.target

This is what's wrong....

Sep 05 20:49:38 p.1407.org sudo\[17482\]: rms : TTY=pts/1 ; PWD=/opt/pump.io/pump.io ; USER=root ; COMMAND=/bin/systemctl start pumpio.service
Sep 05 20:49:38 p.1407.org systemd\[1\]: Starting Pump.io...
Sep 05 20:49:39 p.1407.org pump\[17485\]: path.js:360
Sep 05 20:49:39 p.1407.org pump\[17485\]: throw new TypeError('Arguments to path.join must be strings');
Sep 05 20:49:39 p.1407.org pump\[17485\]: ^
Sep 05 20:49:39 p.1407.org pump\[17485\]: TypeError: Arguments to path.join must be strings
Sep 05 20:49:39 p.1407.org pump\[17485\]: at path.js:360:15
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Array.filter (native)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Object.exports.join (path.js:358:36)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at getConfig (/opt/pump.io/pump.io/bin/pump:58:23)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at main (/opt/pump.io/pump.io/bin/pump:40:18)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Object.<anonymous> (/opt/pump.io/pump.io/bin/pump:151:1)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Module.\_compile (module.js:456:26)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Object.Module.\_extensions..js (module.js:474:10)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Module.load (module.js:356:32)
Sep 05 20:49:39 p.1407.org pump\[17485\]: at Function.Module.\_load (module.js:312:12)
Sep 05 20:49:39 p.1407.org systemd\[1\]: pumpio.service: control process exited, code=exited status=8
Sep 05 20:49:39 p.1407.org systemd\[1\]: Failed to start Pump.io.
Sep 05 20:49:39 p.1407.org systemd\[1\]: Unit pumpio.service entered failed state.

An ideas why? Starting from the console with sudo /opt/pump.io/pump.io/bin/pump works fine.

Grrr...
