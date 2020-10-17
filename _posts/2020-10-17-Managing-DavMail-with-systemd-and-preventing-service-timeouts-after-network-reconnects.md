---
status: published
published: true
title: Managing DavMail with systemd and preventing service timeouts after network reconnects.
categories:
- Desktop
- E-Mail
- Linux
- Sysadmin
tags:
- NetworkManager
- DavMail
comments: []
---
[DavMail](https://davmail.sourceforge.net) enables access to Exchange servers over standard protocols such as IMAP, SMTP and Caldav. 
It, therefore, allows you to check your company e-mail from popular mail clients such as Mailspring, Thunderbird and Geary. 

The following sections outline how to (i) automatically start DavMail via systemd, and (ii) ensure that the service stays operable, even after network reconnects.

# Starting DavMail via systemd

If your distribution does not provide a systemd configuration file for DavMail, you can paste the following snippet into `/etc/systemd/system/davmail.service`. 

```ini
[Unit]
Description=Davmail Exchange gateway
Documentation=man:davmail
Documentation=https://davmail.sourceforge.net/serversetup.html
Documentation=https://davmail.sourceforge.net/advanced.html
Documentation=https://davmail.sourceforge.net/sslsetup.html
After=network.target

[Service]
Type=simple
User=davmail
PermissionsStartOnly=true
ExecStartPre=/usr/bin/touch /var/log/davmail.log
ExecStartPre=/bin/chown davmail:adm /var/log/davmail.log
ExecStart=/usr/bin/davmail -server /etc/davmail.properties
SuccessExitStatus=143
PrivateTmp=yes

[Install]
WantedBy=multi-user.target
```

Afterwards, you need to add the DavMail user and enable the script with

```bash
adduser --system davmail
systemctl daemon-reload
systemctl enable davmail
systemctl start davmail
```

# Coping with network reconnects

One major problem with DavMail are network reconnects (e.g., if you change the network or move between VPNs) since they require a restart of the service to prevent timeouts when accessing your e-mail. One way of solving this issue is the use of the `NetworkManager-dispatcher` service, which can be enabled with

```bash
systemctl enable NetworkManager-dispatcher
systemctl start NetworkManager-dispatcher
```

Once enabled, the dispatcher service allows you to specify scripts that are executed if network connectivity is lost or becomes available again. The following script stops DavMail if networking becomes unavailable and restarts the service after the network is up again.

```bash
#!/bin/sh

# stop davmail, if no network connectivity is available and restart it once
# the network becomes available.

interface=$1 status=$2

case $status in
  up)
      systemctl restart davmail
      ;;
  down)
      systemctl stop davmail
      ;;
esac
```

You can enable automatic restarts of the DavMail service by copying the script to `/etc/NetworkManager/dispatcher.sh` and making it executable with `chmod a+x /etc/NetworkManager/dispatcher.sh`.


# Resources

* [DavMail](https://davmail.sourceforge.net) - DavMail POP/IMAP/SMTP/Caldav/Carddav/LDAP Exchange and Office 365 Gateway
* [DavMail GitHub repository](https://github.com/mguessan/davmail)
* [ArchWiki on managing network services with NetworkManager dispatcher](https://wiki.archlinux.org/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher)

