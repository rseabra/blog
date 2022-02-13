---
title: "pam_ipahbac, the James Bond release"
date: "2019-10-26"
categories: 
  - "free-sw"
  - "pam-ipa-hbac"
tags: 
  - "aix"
  - "free-sw"
  - "freeipa"
---

So we had another take into joining AIX servers against a FreeIPA / Red Hat Identity Management domain, this time with complete success since IBM has improved a lot certain aspects that allowed a much easier integration:

- IDSLDAP (at least 6.4) now configures properly aginst FreeIPA
- the rpm packages (aixtoolbox) are being maintained allowing for a much more recent sudo with ldap support (we couldn't get sudo\_ids to work, just go for normal sudo)
- sshd is finally a version with support for AuthorizedKeysCommand

So it was time for a new take on the HBAC front, and after not being successful with either [pam\_hbac](https://github.com/jhrozek/pam_hbac) or my own [pam\_ipahbac](https://github.com/rseabra/pam_ipahbac), a new look at the code was needed.

Turns out the issue was OpenLDAP. The integration of pam, sshd, idsldap... basically you now **need** to use idsldap's libraries so... time for a new release.

Being much simpler to change my code rather than adapt pam\_hbac, that's what I did and now configure detects that one is on AIX and no longer requires OpenLDAP. Still you need special compilation flags so it wa smuch easier for me to just let them be setup in the rpm spec.

Anyway, you can go to the [website](https://github.com/rseabra/pam_ipahbac) and [download shiny new binaries for 0.0.7 and tar ball](https://github.com/rseabra/pam_ipahbac/releases/tag/0.0.7) if you want, as well as [read my definitive AIX/FreeIPA integration guide](https://github.com/rseabra/pam_ipahbac/wiki/AIX) (which is also quite relevant).
