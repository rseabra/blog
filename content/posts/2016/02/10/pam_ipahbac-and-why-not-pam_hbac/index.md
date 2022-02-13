---
title: "pam_ipahbac (and why not pam_hbac)"
date: "2016-02-10"
categories: 
  - "free-sw"
  - "pam-ipa-hbac"
tags: 
  - "freeipa"
---

[![ipahbac](images/ipahbac.png)](/category/pam-ipa-hbac)Those implementing [FreeIPA](https://www.freeipa.org/) (possibly in the _enterprise ready_ version called [Red Hat Identity Management](https://access.redhat.com/products/identity-management-and-infrastructure#getstarted)) in a hybrid environment (meaning... not just recent GNU/Linux operating systems but particularly including AIX and Solaris) may have noticed the lack of support of an essential component in AIX and Solaris: Host Based Access Control (HBAC).

Without HBAC support, when you join a server to a real **every single enabled user** will be able to login into that server, which just _might not be_ what you want, specially in more """"_enterprise_"""" (please **do notice the several quotes**) environments with different servers having different access roles (developers can go into development servers but not into application life-cycle, operations people not having to logon to developement servers, system administration teams, security officers, etc...).

Some applications _sort of_ implement HBAC by letting you restrict the users that can log into them, but that is definitely not elegant as it defeats the purpose of HBAC: a centralized place where one can define such access rules.

Being a PAM module it needed to have a few features:

1. KISS: it doesn't have to do much more than get the rules, give success on the first match or just deny for any other reason
2. be secure: be not fancy, worry not about UNICODE, do not worry about supporting the kitchen sink, etc. This means:
    1. most AIX and Solaris environments **do not have special characters** like ç or ó or µ, and actually user logins are **short** in length, so a design strategy was to make this module extremely restrictive about the character set it allows, UNICODE is awesome but it's also a sea of unexpected security issues;
    2. do not over-engineer in libraries and sub-files, just implement the PAM groups it needs, do a simple ldap query, navigate through the results, reply to PAM with allowed or denied
    3. I definitely do not mean to imply pam\_hbac is not secure, only that it's a critical focus on pam\_ipahbac

If in the future such _fancy_ use cases that need these things come up, then it can be re-evaluated. It's not set in stone. Just not the focus. Priorities and such.

And this is why [pam\_ipahbac](https://github.com/rseabra/pam_ipahbac) was born rather than working with [pam\_hbac](https://github.com/jhrozek/pam_hbac/).

I believe jhrozek's module to be much more advanced, but I also believe in the above principles, and the primary focus of this module is to work in AIX and Solaris so those plagued with those systems can at least use the awesome Free Software that FreeIPA is.

Also, because it's fun to father some code.

Happy hacking!
