---
title: "Using Let's Encrypt with getssl and minimal root usage #letsencrypt"
date: "2018-02-09"
categories: 
  - "free-sw"
tags: 
  - "lets-encrypt"
  - "security"
  - "tips"
---

[![Let's Encrypt](images/letsencrypt-logo-horizontal.png)](https://letsencrypt.org) is an amazing initiative to have X.509 certificates for your website, or even your email servers, but most instructions just tell you to run (some more some less) complicated programs as root in order to run the periodic certificate renewal workflows, and that is sub-optimal as it substantially increases the number of attack vectors your already exposed system is susceptible to.

This article is just a way to enjoy the benefits of Let's Encrypt while minimizing the need for **root** privileges in your system,and thus keeping it reasonably secure, and this example is doing it with [getssl](https://github.com/srvrco/getssl) (don't be scared it hasn't changed much for some time, they're working on the [new APIv2 support](https://github.com/srvrco/getssl/tree/APIv2)).

It's taking in account a typical CentOS/Red Hat 7 server, your mileage might vary with other systems but it should mostly be the same.

You can start setting up your environment by adding a non privileged user, let's say... **acme**... who will run the renewal workflow:

\# useradd acme

Then you can proceed to installing getssl and setting up directories for your files:

\# curl https://raw.githubusercontent.com/srvrco/getssl/master/getssl > /usr/local/bin/getssl
# chmod 0755 /usr/local/bin/getssl
# mkdir -p /etc/letsencrypt/acme/ssl.{crt,key,pem}
# chown -R acme:acme /etc/letsencrypt/acme
# chmod -R 0755 /etc/letsencrypt
# chmod 0750 /etc/letsencrypt/acme/ssl.{key,pem}
# mkdir -p /var/www/html/letsencrypt/.well-known/acme-challenge
# chown letsencrypt:letsencrypt /var/www/html/letsencrypt/.well-known/acme-challenge
# echo 'letsencrypt yourhostname=NOPASSWD: /usr/bin/systemctl restart httpd' >> /etc/sudoers.d/letsencrypt

**That last line adding a sudo rule is part of the magic** and the single root command that is executed.  You can also make it restart Postfix, Dovecot, or any other service you use a certificate and that needs restarting in order to take the new certificate.

In order to let you read it all from this article, I'll borrow the example's from getssl's github page and then add in my own suggestions.

Now you want to prepare the environment (as the user **acme**) for your domain:

getssl -c yourdomain.com

This will create a **~/.getssl/yourdomain.com** directory, the main files you want are called **getssl.cfg**, there's a global file on **~/.getssl/getssl.cfg** and then more specific files per domain, **~/.getssl/yourdomain.com/getssl.cfg**

In the main file, ~/.getssl/getssl.cfg, you'll need to set up the values accordingly to your needs (I won't dive into how to get an account), **but  for this setup** you'll want to change the following:

RELOAD\_CMD="/usr/bin/sudo systemctl restart httpd"
ACL=('/var/www/html/letsencrypt/.well-known/acme-challenge')
CA\_CERT\_LOCATION="/etc/letsencrypt/acme/ssl.crt/lets-encrypt-x3-cross-signed.pem
RENEW\_ALLOW="30"

And that **RELOAD\_CMD** right there is part of the magic...

Now edit  **~/.getssl/yourdomain.com/getssl.cfg** and change the following:

DOMAIN\_CERT\_LOCATION="/etc/letsencrypt/acme/ssl.crt/yourdomain.com.crt"
DOMAIN\_KEY\_LOCATION="/etc/letsencrypt/acme/ssl.key/yourdomain.com.key"

Now all you need is to set up a cron job:

45 6 \* \* \* /home/letsencrypt/getssl -u -a -q

And finally you configure Apache httpd to use the files paths for the CERTificate and its KEY:

(...)
SSLCertificateFile /etc/letsencrypt/acme/ssl.crt/blog.1407.org.crt
SSLCertificateKeyFile /etc/letsencrypt/acme/ssl.key/blog.1407.org.key
SSLCertificateChainFile /etc/letsencrypt/acme/ssl.crt/lets-encrypt-x3-cross-signed.pem
Alias /.well-known/acme-challenge /var/www/html/letsencrypt/.well-known/acme-challenge
(...)

And you're done: the cron job will run every day, and when you reach the 30 days to renew threshold your certificate will be renewed with minimal root usage.
