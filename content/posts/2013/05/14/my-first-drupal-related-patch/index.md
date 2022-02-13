---
title: "My first #Drupal related patch"
date: "2013-05-14"
categories: 
  - "free-sw"
  - "me"
tags: 
  - "drupal"
  - "haspatch"
  - "theme"
---

I've recently installed the [Corporate Clean](http://drupal.org/project/corporateclean) theme on [ANSOL's website](https://ansol.org/) because of it's fluid design and top slides.

However, the slides are implemented directly in php code in the page.tpl.php file. I **hated that**. So I pushed my hate towards a positive result: [a fix proposal](http://drupal.org/node/1994972).

So now you just put some PHP block on the Slideshow region, add a custom field to the pages you want to show up there and use the Summary for the content. Seems simple enough and it's possible to change the slides without needing direct access to the code, so you can let less experienced people just post content.
