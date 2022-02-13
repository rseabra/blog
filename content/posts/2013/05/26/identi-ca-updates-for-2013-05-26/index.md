---
title: "Identi.ca Updates for 2013-05-26"
date: "2013-05-26"
categories: 
  - "mublog"
---

- Installed my own pump.io instance. June 1 will be a disaster if identica turns out as unstable. I hope @Evan has lots of uncommitted code. [#](http://identi.ca/notice/101087429)
- @evan not this way, I don't think so. [#](http://identi.ca/notice/101087746)
- @evan I'm using wheezy. npm -g install pump.io ; using redis backend. 400 bad request for login in email is requested. [#](http://identi.ca/notice/101087761)
- @evan several times, the interface just freezes. I have to press reload on the browser URL [#](http://identi.ca/notice/101087773)
- @evan some URLs are built using values stored in db so when URL changes they build bad URLs [#](http://identi.ca/notice/101087786)
- @evan then I tried from git but it was even more unstable. [#](http://identi.ca/notice/101087824)
- @evan since I used the master branch it's not entirely unexpected but... [#](http://identi.ca/notice/101087853)
- @evan sure, I'll be one of them in the meanwhile but crickets might be heard ;) [#](http://identi.ca/notice/101087876)
- @evan I'm using node 0.10.5 in usr local bin, not from wheezy [#](http://identi.ca/notice/101087903)
- @evan why not build URLs from the environment variables? Wouldn't that solve the problem? [#](http://identi.ca/notice/101087914)
- @evan it was even worse when I required email. No mail sent, logged in and super unstable. [#](http://identi.ca/notice/101087921)
- @evan sure. [#](http://identi.ca/notice/101087925)
- RT @glynmoody needless to say, #BBC news has not one iota about the 2 million people marching against #monsanto yesterday; the mega-fail ... [#](http://identi.ca/notice/101087931)
- @evan I also need to run it behind Apache because I only have one IP and I can't waste it on one site alone... [#](http://identi.ca/notice/101087965)
- @jankusanagi I don't mind a temp. loss of functionality while new stuff gets added to pump.io, it's the stability of what's there I worry. [#](http://identi.ca/notice/101088187)
- @jankusanagi you really need to check my latest dents exchanged with Evan... [#](http://identi.ca/notice/101088354)
- @evan first log: trying to register for the first time, behind a reverse proxy: [http://ur1.ca/e1tl8](http://ur1.ca/e1tl8) [#](http://identi.ca/notice/101088735)
- @evan second log: [http://ur1.ca/e1tq2](http://ur1.ca/e1tq2) there are reasons to change web sites, like working around the previous issue. [#](http://identi.ca/notice/101088825)
- In retrospection, all my instability issues might be due to the impossibilty to register behind the reverse proxy and working around that. [#](http://identi.ca/notice/101088857)
- It's possible that more URLs are using the alternative port... [#](http://identi.ca/notice/101088864)
- Expecting stability regarding "other" servers in the Internet? Really? [#](http://identi.ca/notice/101089119)
- Unfair? They're not at [http://pump.io/](http://pump.io/) if anyone has "unfair" to shout out it's me. [http://ur1.ca/d6s5g](http://ur1.ca/d6s5g) more useful info [#](http://identi.ca/notice/101089141)
- Sorry. I think it's unfair to cite documentation that's not in plain sight, specially when what seems to me like a design flaw is at stake. [#](http://identi.ca/notice/101089214)
- Ok, urlport might help a lot for this setup, I'll try again from master, and report back soon. [#](http://identi.ca/notice/101089269)
- "if you're insisting on proxying behind Apache or whatever despite warnings not to, you can use this." unfair to people with VPS and 1 IP [#](http://identi.ca/notice/101089353)
- Seems not to work. I get an infinite http 301 redirect loop. [#](http://identi.ca/notice/101089404)
- I realize you care about an URL that doesn't change, but you shouldn't impose that on a design. It should be a best practice, though. [#](http://identi.ca/notice/101089514)
- That configuration definitely results in a 301 redirection loop. GET / HTTP/1.1 Host: pump.1407.org -> Location: [http://pump.1407.org/](http://pump.1407.org/) [#](http://identi.ca/notice/101089561)
- And it's amazing to see what look like bots already trying to abuse it :) [#](http://identi.ca/notice/101089566)
