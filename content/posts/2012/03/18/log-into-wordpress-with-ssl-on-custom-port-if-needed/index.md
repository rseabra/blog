---
title: "Log into WordPress with SSL (on custom port if needed)"
date: "2012-03-18"
categories: 
  - "free-sw"
tags: 
  - "haspatch"
  - "ssl"
  - "wordpress"
---

Don't you wish you could use SSL for logging into your WordPress site, but your standard https port is unavailable? Well, I hope to help you with that... do read on :)

In order to login into WordPress with SSL you just need to add the following to wp-config.php:

> define('FORCE\_SSL\_LOGIN', true); define('FORCE\_SSL\_ADMIN', true);

But that redirects you to https://www.yourDomain.org/. What if you need to redirect into https://www.yourDomain.org:8443/ ? What then?

Well, the following patch will allow you to add a property called CUSTOM\_PORT which you will define as your desired port. In case of my small example, 8443 like this:

> define('CUSTOM\_PORT', 8443);

I registered this patch as [enhancement 20253](http://core.trac.wordpress.org/ticket/20253) on WordPress's trac.

Happy hacking!

\--- old/wp-includes/link-template.php    2011-10-24 20:13:23.000000000 +0100
+++ new/wp-includes/link-template.php    2012-03-18 00:06:38.000000000 +0000
@@ -1931,8 +1931,10 @@
else
$url = get\_blog\_option( $blog\_id, 'siteurl' );

-    if ( 'http' != $scheme )
+    if ( 'http' != $scheme ) {
$url = str\_replace( 'http://', "{$scheme}://", $url );
+        if(defined('CUSTOM\_PORT')) $url .= ":" . CUSTOM\_PORT;
+    }

if ( !empty( $path ) && is\_string( $path ) && strpos( $path, '..' ) === false )
$url .= '/' . ltrim( $path, '/' );
