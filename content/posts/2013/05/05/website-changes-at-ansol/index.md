---
title: "Setup front slides feature, new theme and Planet ANSOL"
date: "2013-05-05"
categories: 
  - "free-sw"
tags: 
  - "ansol"
  - "drupal"
---

These last few days I've added a theme with slides feature to [ANSOL's website](https://ansol.org/), changed the way it did them so it's much, much more useful, and setup a feed aggregator for ANSOL's members, that is [Planet ANSOL](https://ansol.org/planeta). Read on to know more about what, and how it it changed.

### The theme

...is called [Corporate Clean](http://drupal.org/project/corporateclean), which not only carried a slides feature, but also has a more flexible layout for smaller screens like phones and tablets.

First I tried the default color, but then I changed to warmer colors as it was too cold for my taste, at least, and fixed up the logo which was looking a bit like, well, crap.

Went on to checkout how the slides worked and shrieked... this feature is hard coded on the page template! That will **not** do. So I hacked it in order to contain a region for the slides, duly called Slideshow, where I would be able to put a block.

Next, I added a custom Boolean field to the Basic and Event pages to mark whether that page's Teaser/Summary was to be considered a slide. One only has to edit the Teaser/Summary and check the Slide check box by the end of the node edition page.

Finally, I wrote a small piece of PHP code that uses Entity API to query the database for nodes with that field set to true and display it's teasers in the same manner that the theme had them hard coded.

The result is nice, and now you don't need to hack code in order to make slides, although they do seem a bit too big to me, but maybe it will work.

### The planet

... was very quick to setup with the Views and Feeds modules. I created an aggregation of the blogs I knew some members had, then hammered the view presentation options until I was satisfied with the result.

The main trick is to include all the feed fields you want to use, hide them from visibility and then use a generic text field to display them (using placeholders) in a more adequate form than the default one. Magic!
