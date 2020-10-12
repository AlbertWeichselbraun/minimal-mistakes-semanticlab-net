---
status: published
published: true
title: Setting up Gnome CalDAV and CardDAV support with Radicale
categories:
- Sysadmin
- Linux
tags:
- CalDAV
- CardDAV
- Gnome
comments: []
---
Although Gnome supports CalDAV and CardDAV, it currently only allows configuring them for Nextcloud servers. Their is a long standing [Bug Report](https://bugzilla.gnome.org/show_bug.cgi?id=720519) which describes this issue but hasn't yet (as of October 2020) been properly addressed.

Florian Apolloner has, therefore, developed a [webapp](https://gist.github.com/apollo13/f4fc8f33a2700dffb9e11c1b056c53ba) which uses redirects to map requests meant for Nextcloud servers to other CalDAV/CardDAV servers.

If you run an Apache Web server you can instead use `mod_rewrite` to replicate his solution:

```apache
   # redirect used for caldav and carddav compatibility with owncloud & nextcloud
   RewriteEngine on
   RewriteRule "^/.well-known/caldav" "/dav/caldav/" [R]
   RewriteRule "^/.well-known/carddav" "/dav/carddav/" [R]
   RewriteRule "^/remote.php/webdav/" "/dav" [R]
   RewriteRule "^/remote.php/caldav" "/dav/caldav/" [R]
   RewriteRule "^/remote.php/carddav" "/dav/carddav/" [R]
``` 

The redirects' targets need to point to the path or URL of your caldav and carddav servers (I use [Radicale](https://radicale.org) so in my case the proper URLs are `/dav/caldav` and `/dav/carddav`). The `/webdav` redirect can either point to your WebDAV server (if you plan on using WebDAV remote storage) or to a simple Web page on your system.

Once the redirects are set up, you can configure your CalDAV/CardDAV server as *NextCloud* server in *Gnome Online Accounts*. If your server does not support WebDAV you need to disable the `Documents` and `Files` sharing settings as outlined below.

![Gnome Nextcloud Settings](/assets/images/2020/nextcloud-settings.png "Gnome Nextcloud Settings")

Once you have completed this setup applications such as *Gnome To Do* and *Gnome Calendar* will be able to synchronize with your CalDAV server.


# Resources

* [Gnome Bug Report #720519](https://bugzilla.gnome.org/show_bug.cgi?id=720519) -  Add separate components for CalDAV and CardDAV accounts 
* [OwnCloud/Nextcloud Emulator by Florian Apoller](https://gist.github.com/apollo13/f4fc8f33a2700dffb9e11c1b056c53ba)
* [Radicale CalDAV/WebDAV Server](https://radicale.org)

