---
status: published
published: true
title: Network-bound disk encryption in Ubuntu 20.04 (Focal Fossa) - Booting servers with an encrypted root file system without user interaction.
categories:
- Sysadmin
- Encryption
tags:
- tang
- clevis
- luks
- linux unified key setup
comments: []
---
Network-bound disk encryption allows unlocking LUKS devices (e.g. the encrypted root file system of an Ubuntu server) without entering the password. Instead a Tang server is queried for a key that can be used in conjunction with a private secret to compute the decryption key. As long as the Tang server is available, the disk can be decrypted without the need to manually enter a password.

Ubuntu 20.04 requires the following components for implementing a network-bound disk encryption:

 1. the LUKS encrypted device(s) that should be automatically unlocked. 
 2. a Tang server that provides the public key required by the client for deriving its LUKS decryption key.
 3. Clevis which provides clients that can use a Tang server for unlocking LUKS partitions.
 4. For unlocking a boot device adjustments to initramfs (automatically provided by the `clevis-initramfs` package) are necessary.


# How does network-bound disk encryption work?

The figures below outline how network-bound encryption works. In the first step we use clevis to bind a LUKS encrypted device to a Tang server, generating a secret JSON Web Key (`cJWK`) on the client which is then combined with the server's public key (`sJWK*`) to generate the key (`dJWC`) that is then added to the LUKS device as a decryption key.

![Bind the LUKS device to the Tang server](/assets/images/2020/clevis-bind-to-tang-server.svg)

Once the device has been bound to the Tang server, it can compute its decryption key with the server's help. The client first generates a ephemeral key (`eJWK`) that is then combined with its secret (`cJWK`) to generate a message (`xJWK`) that is sent to the server. The server combines `xJWK` with its private key `sJWK `to generate the response `yJWK`. Clevis then combines `yJWK `with the server's public key `sJWK`* and `eJWK `to recover the decryption key `dJWK`. 


![Recover the decryption key with the help of the Tang server](/assets/images/2020/clevis-recover-encryption-key.svg)


# Setup

Ubuntu 20.04 provides packages for Tang and Clevis which makes installing them straight forward.

## Setup and start the Tang server
Install Tang and José (an implementation of the JavaScript Object Signing and Encryption standards used by Tang) on the Tang server. 

```bash
apt install tang jose
systemctl enable tangd.socket
systemctl start tangd.socket
``` 
If you install Tang on Ubuntu 18.04 you need to manually generate the Tang keys with `/usr/lib/x86_64-linux-gnu/tangd-keygen /var/db/tang` before the server start.

Execute `tang-show-keys` to determine the signing key's fingerprint.

```bash
tang-show-keys 
TieDkMgbVKzmXl-uyOfIa0U30lo
``` 

## Host with the encrypted LUKS device(s)
Install Clevis on the host system and then use `clevis luks bind` for binding the device to the Tang server. Clevis will ask you to verify the signing key's fingerprint. Afterwards, Clevis can be used to unlock the device.

```bash
# install clevis
apt install clevis clevis-luks

# ensure that the device (e.g. vda1) is encrypted and that the tang server is working
cryptsetup luksDump /dev/vda1            # just to be sure that we encrypt the right disk ;)
curl http://192.168.122.1/adv            # verify that the tang server yields a response

# enable clevis tang decryption for the given LUKS device
clevis luks bind -d /dev/vda1 tang '{"url": "http://192.168.122.1"}'
```

Clevis provides plugins for initramfs, dracut, systemd and udisk2 to automize the unlocking process.


### Automatically unlocking a root device with Clevis

Once Clevis support has been enabled for an encrypted root file system, it can be automatically unlocked by installing the corresponding clevis plugin and rebuilding initramfs.

```bash
# insall the necessary clevis plugin
apt install clevis-initramfs

# reinitialize initramfs to support automatic unlocking of the root device.
update-initramfs -u -k 'all'            
```

## Automatic unlocking of non-root devices with Clevis

Automatic unlocking of non-root devices via systemd is supported by the `clevis-systemd` plugin.

```bash
apt install clevis-system
```

Afterwards the encrypted non-root devices need to be added to `/etc/crypttab` with the `_netdev` option. Crypttab entries consist of the following four columns:
- `target`: the name to be used for the mapped (i.e. decrypted) device
- `source device`: the name of the corresponding encrypted source device
- `key file`: `none`, since we do not specify a key
- `options`: the column must be set to `_netdev` so that systemd is able to automatically mount the device using the `clevis-systemd` plugin.

``` 
encrypted_home	/dev/vdb  none  _netdev
encrypted_opt   /dev/vdc  none  _netdev
```

Afterwards, the devices can be added to `/etc/fstab` for automatic mounting:

```
/dev/mapper/encrypted_home  /home   xfs  defaults,_netdev  0 0
/dev/mapper/encrypted_opt   /opt    xfs  defaults,_netdev  0 0
``` 
Again it is important to add the `_netdev` option to ensure that systemd is able to recognize and automatically mount the encrypted device.

{: .notice--danger}
**Warning:** To the best of my knowledge it is not possible to mount an encrypted `/var` partition using this method, since systemd relies on `/var` for its networking configuration.



# Resources

* Github pages
  - [Tang](https://github.com/latchset/tang) 
  - [Clevis](https://github.com/latchset/clevis)
* [ADMIN Magazine article on Clevis and Tang](https://www.admin-magazine.com/Archive/2018/43/Automatic-data-encryption-and-decryption-with-Clevis-and-Tang)
* [Youtube video by Fraser Tweedale on Clevis and Tang](https://www.youtube.com/watch?v=Dk6ZuydQt9I)
