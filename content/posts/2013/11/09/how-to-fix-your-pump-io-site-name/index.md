---
title: "How to fix your pump.io site name"
date: "2013-11-09"
categories: 
  - "mublog"
  - "free-sw"
tags: 
  - "pump-io"
---

A newbie mistake that is quite easy to do on pump.io is to set a name for your instance, then decide to change and... oops, you changed /etc/pump.io.json but **it doesn't change! WTF!?**

In my case I was particularly pissed off because there's a bug on pump.io with certain characters, I had named my instance _1407's Pumps_ but apparently pump.io doesn't like that quote there... displayed instead _1407&#27;s Pumps_. **ANGRRRY!**

After digging through all keys in my instance, I found out that mine was service:urn:uuid:b0f6e849-4a8b-4b8a-9f3d-1ee221d62d58 (faked uuid), but there may be a lot of **service:urn:uuid:** entries (234 when I did this)!

Here's how you can fix it on your database as well (I'm using redis, you'll have to adjust to your particular case if using another DB).

echo "keys service:urn:uuid:\*" | redis-cli > uuids.txt
cat uuids.txt | while read KEY ; do
    echo "set $KEY '$(echo get $KEY | redis-cli)'" >> uuids-set.txt
done
grep "MISTAKEN TITLE" uuids-set.txt > title-fix.txt

So now you can edit title-fix.txt with your favorite text editor and fix the field **displayName** to your pleasure, and after saving your change you are now ready to apply it:

redis-cli < title-fix.txt

I doubt restarting is needed, but I did it anyway, you can try. :)
