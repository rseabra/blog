---
title: "Fixing the FirefoxOS default search provider"
date: "2013-06-01"
categories: 
  - "firefox-os"
  - "free-sw"
tags: 
  - "code"
  - "firefox-os"
  - "free-sw"
---

WTF? FirefoxOS uses Bing as default search provider?

Yuck, I must fix that. Finally after almost a week I have had some time for me and that's the first thing I **must** fix. Thanks to the very helpful comment from Mathieu [in this blog post](http://ruk.ca/content/how-change-search-provider-firefox-os-phones-bing-google), I wrote a [very small shell script that replaces the search provider](http://files.1407.org/ffos/fix-ffos-search-provider.sh) to your favorite one, defaulting to Google.

It uses sudo for the privileged commands but doesn't need to completely run as root. Its your choice, run **./fix-ffos-search-provider.sh** or **sudo ./fix-ffos-search-provider.sh** taking as optional arguments (in this order), the Title, the URL and it's Favicon url. Miss one and the Google default will be used :) eg:

./fix-ffos-search-provider.sh \\
  "Duck Duck Go" https://duckduckgo.com/ https://duckduckgo.com/favicon.ico

First, it sets the options, then starts adb-server and fetches the browser application (note that you need the **android-tools** package in Fedora or the Android SDK):

#!/bin/sh

TITLE=${1:-Google}
URL=${2:-www.google.com/m}
ICO=${3:-https://www.google.com/favicon.ico}

sudo adb start-server

sudo adb pull \\
  /system/b2g/webapps/browser.gaiamobile.org/application.zip
sudo chown $USER:$GROUP application.zip

mkdir application
cd application/
unzip ../application.zip

Then, it does the magic with the help of Perl:

perl -pi -e " \\
    s|(DEFAULT\_SEARCH\_PROVIDER\_URL: ?)'.\*?'|\\$1'$URL'|; \\
    s|(DEFAULT\_SEARCH\_PROVIDER\_TITLE: ?)'.\*?'|\\$1'$TITLE'|; \\
    s|(DEFAULT\_SEARCH\_PROVIDER\_ICON: ?)'.\*?'|\\$1'$URL'|; \\
    " js/browser.js gaia\_build\_defer\_index.js

Finally, it rebuilds the browser application and pushes it back to the phone and reboots it (it shouldn't need a reboot, maybe there's a way to avoid this?):

zip -fr ../application.zip .
cd ..

sudo adb remount
sudo adb push application.zip \\
   /system/b2g/webapps/browser.gaiamobile.org/application.zip
sudo adb reboot

So, here it is, finally fixed :) Well, temporarily (it will be better fixed following the results of [https://github.com/mozilla-b2g/gaia/pull/9454](https://github.com/mozilla-b2g/gaia/pull/9454) and [https://github.com/gasolin/gaia/commit/47072a825d9e7c2859f4f8de4fb200cc7450e10b](https://github.com/gasolin/gaia/commit/47072a825d9e7c2859f4f8de4fb200cc7450e10b) or something similar) at least.

\[caption id="attachment\_1750" align="aligncenter" width="168"\][![Screenshot of FirefoxOS browser googling for 'test'](images/2013-06-01-09-58-50-168x300.png)](http://blog.1407.org/wp-content/uploads/2013/06/2013-06-01-09-58-50.png) Googling for 'test'\[/caption\]

[![CC0](images/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)To the extent possible under law, [Rui Miguel Silva Seabra](http://blog.1407.org/) has waived all copyright and related or neighboring rights to Fix FirefoxOS Default Search Provider. This work is published from Portugal.
