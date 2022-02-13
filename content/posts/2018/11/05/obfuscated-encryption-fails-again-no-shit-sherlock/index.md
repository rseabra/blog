---
title: "Obfuscated encryption fails again... No Shit, Sherlock!"
date: "2018-11-05"
categories: 
  - "hardware"
tags: 
  - "security"
  - "ssd"
  - "wtf"
---

**This is obfuscation, rather than encryption**, for all purposes.

Major hardware vendors are involved, and «**the issue is worse on Windows**». No surprises, then... Glad I don't use that poor excuse for an operating system... :)

It seems a few popular devices with hardware controlled self encryption aren't really doing it good by having master passwords (truly a #WTF) and faulty standards implementations.

«_SSDs from Micron (Crucial) and Samsung are affected. These are SSDs that support hardware-level encryption via a local built-in chip, separate from the main CPU. Some of these devices have a factory-set master password that bypasses the user-set password, while other SSDs store the encryption key on the hard drive, from where it can be retrieved. The issue is worse on Windows, where BitLocker defers software-level encryption to hardware encryption-capable SSDs, meaning user data is vulnerable to attacks without the user's knowledge_»

There's a [paper with all the gory details](https://www.ru.nl/publish/pages/909275/draft-paper_1.pdf) for the hard core guys  and a [report on ZDNet](https://www.zdnet.com/article/flaws-in-self-encrypting-ssds-let-attackers-bypass-disk-encryption/) for the rest.
