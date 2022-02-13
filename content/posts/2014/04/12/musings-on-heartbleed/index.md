---
title: "Musings on #Heartbleed"
date: "2014-04-12"
categories: 
  - "free-sw"
tags: 
  - "free-sw"
  - "heartbleed"
  - "musings"
  - "security"
---

Several thoughts have been on my mind about [#heartbleed](https://www.google.pt/search?q=heartbleed+bug). You may have heard similar thoughts about it, but I'd like to add my own.

Ah... nothing like checking the news in the morning, feels like... ah... a bug in OpenSSL, let's check it out... OMFG... By 10:00 I was already applying patches to vulnerable (and exposed) servers all around, processes be damned!

#### Is Free Software security tarnished?

Absolutely not!

Let me start by the first thing you should take in mind: **you're better off than with proprietary software and this bug proves it**, few could have said as well as [Sam Tuke of FSF Europe did](http://blogs.fsfe.org/samtuke/?p=718), there are also a few words from [Simon Phipps](http://www.infoworld.com/t/open-source-software/stop-laying-the-blame-heartbleed-open-source-240434) and [Eric Raymond](http://esr.ibiblio.org/?p=5665).

In a gist, there are several instances of just as serious bugs, and many much more serious, on proprietary software. Even in the field of network security. And those are just the tip of the iceberg, those that were guessed and not found.

This bug had patches available within few hours of being published available to those affected.

Several documented flaw finding studies have been made, guess who turned out better **in every single one of them** in average? Yes, Free Software. Proprietary software has constantly been found to have, in average, more bugs, more security bugs, more delayed patch releases, etc..

Update (2014/04/13): Also, an even such as this one prompted an [independent audit review from the OpenBSD](http://undeadly.org/cgi?action=article&sid=20140415093252&mode=expanded&count=2) people, [here's another bug in OpenSSL that has been fixed there](http://ftp.openbsd.org/pub/OpenBSD/patches/5.4/common/008_openssl.patch), proving once again how Free Software works to make software more secure:

1. you can do independent and public audit reviews
2. you can push fixes for what you found publicly on the Internet
3. anyone can take advantage of those changes thus maximizing the effect

Now imagine such a bug happened in Microsoft's crypto...

1. you can't do independent audit reviews
2. you can't push fixes for what you found publicly on the Internet
3. nobody but Microsoft can make a fixes Microsoft crypto library

Replace Microsoft by whomever you prefer above, they're just an easy target. ;)

#### Exposure

Here's the most [detailed timeline of public information on the bug](http://m.smh.com.au/it-pro/security-it/heartbleed-disclosure-timeline-who-knew-what-and-when-20140414-zqurk.html) that I found.

Yes, the code was there for about two years, but the exposure was **not** that big. It was big, about a fifth of the "_secure_" web. Unfortunately, **lots of very popular websites were exposed**, so the general recommendation is: don't assume they're safe, **change your passwords everywhere**.

Why wasn't it bigger? Because not everyone runs the latest releases, lots of GNU/Linux distributions have more conservative approaches to running recent software. Take in point Red Hat Enterprise Linux and it's derivate distributions.

Only since the 6.5 release, released in late November last year, did **updated** Red Hat (and derivatives) installations become exposed. CentOS followed a about a couple of weeks later.

Ironically, this bug affected the most efficient system administrators who had kept their systems updated :)

But many run their services in, for instance, Red Hat Enterprise Linux 5 (and derivatives) which is completely unaffected by this bug. Same for other software.

Even those who run the major 6.5 release could be totally unaffected, if they used NSS instead of OpenSSL with Apache, for instance.

In short: it was big, but not catastrophically big.

#### Also affects proprietary software!

What? How could this be? Isn't OpenSSL Free Software? Well, yes, yes it is, but it is licensed in such a way that permits proprietary derivative versions.

They should be safer, right? Hi [Cisco and Juniper](http://online.wsj.com/news/articles/SB10001424052702303873604579493963847851346?mod=djemalertNEWS)... I'm sure there are others. I wonder if they'll be at least honest enough with us... I urge people to check their ultra-expensive and highly proprietary  Web Application Firewalls, Load Balancers, Proxies... etc...

#### All your keys are belong to US!

[9 out of 10 SSL certificates are under indirect control of the US Government](http://lorddoig.svbtle.com/heartbleed-should-bleed-x509-to-death). Think Patriot, NDAA, National Security Letters, Secret Courts with Secret Interpretations, people and companies coerced under threat of being formally accused of treason if they don't cooperate or if they talk about it.

Even if [#heartbleed can **really** lead vulnerable  software to leak the private keys](https://www.cloudflarechallenge.com/heartbleed), you should renew your certificates under a non-american CA.

Really, don't make it easy for them, they don't deserve that, your customers don't deserve that, your friends and family don't deserve that.

#### Change management be damned!

If you ever have an axe to grind about ISO 20000, ITIL or similar _brain dead_ efficiency killers, **specially when implemented by complete and utter idiots**, now you can have some revenge.

It is a bug of such seriousness that I recommend to screw the change management processes. Update now if you are affected or change your career because you either are managed by complete and utter idiots or you don't take it seriously enough.

Places that have enough good sense will allow you to run the Emergency Change process by your ECAB after the fact for such serious situations.

Take advantage of that, this is such a case.

#### Conspiracy theories

Unlike some suggested, it appears to be an honest mistake that neither the developer nor his reviewers did spot, and they felt quite embarrassed:

> The author of the bug, Robin Seggelmann,[\[78\]](http://en.wikipedia.org/wiki/Heartbleed_bug#cite_note-78) stated that he "missed validating a variable containing a length" and denied any intention to submit a flawed implementation.[\[79\]](http://en.wikipedia.org/wiki/Heartbleed_bug#cite_note-79)

[Theo de Raadt, OpenBSD's founder, said](http://article.gmane.org/gmane.os.openbsd.misc/211963) «_OpenSSL is not developed by a responsible team_», but I doubt they'll bother implementing a new SSL library. I wonder what they'll do though... but are likely [making an independent review](http://undeadly.org/cgi?action=article&sid=20140415093252&mode=expanded&count=2).

#### Prophecy come true!

Poul Henning-Kamp's hilarious ending [keynote of FOSDEM 2014](http://phk.freebsd.dk/_downloads/FOSDEM_2014.pdf) pretending to be an NSA agent speaking of _Operation Orchestra_, calling it a crown jewel:

> - Crown jewel: OpenSSL
> - Go-to library for crypto services
> - API is a nightmare
> - Documentation is deficient and misleading
> - Defaults are deceptive

We need to ask him where he has found spice... he certainly seemed like he had blue eyes and #Heartbleed was truly a Crow Jewel for...

#### ...The NSA

_**N**_o _**s**_uch _**a**_gency had such a duty to find a serious bug like this one and responsibly proceed to get it fixed ASAP as it was affecting its nation like the National Security Agency had.

There are [innuendos that the NSA knew about heartbleed for a long time](http://www.bloomberg.com/news/2014-04-11/nsa-said-to-have-used-heartbleed-bug-exposing-consumers.html). They certainly have the expertise and the budget to have found it, but [they did deny any](http://www.forbes.com/sites/larrymagid/2014/04/11/report-nsa-knew-about-and-exploited-heartbleed-for-years/) knowledge or exploit for years, in fact that they didn't know about it before April.

Of course, no one can trust the NSA anymore because they have been proven invested into breaking security for everyone, so they could be lying in order to cover their asses after such a monumental fail in protecting their own country's security.

Or they could have just been doing it for less than two years, like one year and 364 days, not yet **years** (plural), right?

One never can tell, and that's symptomatic of a very botched organization.

#### Is Microsoft involved?

I don't know. It's certainly fishy that:

- The publication date coincides with the _death_ of Windows XP. It could be called a distraction manouver, so that people get scared of moving away from Windows XP into a GNU/Linux... it certainly has been effective at crying wolf in big media outlets
- Codenomicon is run by a Microsoftie, well, ex Chief Security Officer of Microsoft, but those kinds of people tend to leave the companies with strong lobbying and partnership relations in their next ventures with the big mothership
- It is documented that Microsoft has been a faithful collaborator of the NSA for many years, even to the point of maybe having a dedicated backdoor

Maybe it's just coincidence. _Maybe_...

#### OpenSSL is grossly unappreciated

They **few** OpenSSL developers are highly dedicated people that don't exactly live well off of it. In fact, the importance of OpenSSL is disproportionately unappreciated, specially in a financially rewarding form.

Fortunately, the devlopers do it more out of other rewarding factors, like [responsibility and pride.](http://veridicalsystems.com/blog/of-money-responsibility-and-pride/)

#### Conclusions

- It's one of the most serious security bugs in the history of the Internet
- Use any of the available mitigations if you're affected (upgrade, recompile disabling the feature, downgrade, change software)
- More people (specially corporate companies making money with OpenSSL) should donate mone to the OpenSSL Software Foundation
- I don't remember writing such a long post, it's probably very flawed, I accept patches, comment below ;)
