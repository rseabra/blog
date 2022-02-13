---
title: "Twitter is wrong: should not drop httpS basic auth"
date: "2010-06-11"
categories: 
  - "free-sw"
tags: 
  - "elmdentica"
  - "free-sw"
  - "identi-ca"
  - "statusnet"
  - "twitter"
---

As some of you might know, I write a µ-blogging tool called [elmdentica](http://trac.enlightenment.org/e/browser/trunk/elmdentica). It is a client side application developed with [Elementary](http://trac.enlightenment.org/e/wiki/Elementary), an EFL library oriented towards small touchscreen interfaces. I only recently learned that Twitter is dropping Basic Authentication support coming next June 30th. They claim it's insecure because:

1. with http credentials go in the clear (no problem here)
2. with https, some people may think it's too expensive (only **complete idiots**)
3. applications have to store user credentials locally

As an alternative, they are making oauth mandatory for APIs that need authentication. While their reasoning may make sense in the context of massively concentrated web applications (think Twitpic and similars) this is absurd for client application like those running in your cell phones or computers.

### Let's take a look at the problem...

oauth gives you a consumer key and a consumer secret that authenticate **your application**. They don't authenticate the user, they prove Twitter that you're a legitimate and registered application.

If both key and secret became public, anyone could make an application pretending to be yours. While someone making a clone of your program isn't a real problem, if someone writes a trojan horse... then there could be a problem, no?

Well, with oauth, both key and secret need to be known by the application during run time. So at any given moment, the computer running your application will have these two important assets. Either because they are embedded in your code, or because you download them live from a site. The fact remains: they are for all practical effects no longer secrets.

In web applications, no user accesses the only running copy of the software holding both key and secret, so oauth works there.

### What about xauth?

I haven't read **much** about xauth but after reading this [page explaining what xauth is](http://www.reynoldsftw.com/2010/03/using-xauth-an-alternate-oauth-from-twitter/), I'm absolutely convinced the problem remains and wasn't even tackled. The only issue that was solved, by requesting an user's login and password only once, without need of local storage or visiting a web page, was an usability issue for client applications.

**The real problem is still there, so Twitter is wrong and should not drop Basic Authentication from the https interface.**

If they do, elmdentica will very likely not work on Twitter anymore. I don't care much about that, but the users of elmdentica may care. That pisses me off.

### What now?

Fortunately, there is a better alternative to Twitter if you value software freedom called [identi.ca](http://identi.ca/). More than just using, you can have your own "Twitter" by installing the Free Software that makes identi.ca, which is [StatusNet](http://status.net/).

At least [they have no plans of dropping Basic Authentication](http://identi.ca/conversation/35193899#notice-35397768). Hurra!
