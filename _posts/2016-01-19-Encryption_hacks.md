---
title: Encryption hacks
permalink: wiki/Encryption_hacks/
layout: single
alias: /index.php/Encryption_hacks
excerpt: Secure encryption settings for Apache, Firefox, SSH and LUKS.
categories: ["linux", "sysadmin", "encryption"]
tags: 
- luks
- encryption
- linux unified key setup
---
{% include toc %}

Secure encryption settings for Apache, Firefox, SSH and LUKS.

Apache SSL
==========

-   generate custom dh values using the following command

``` bash
   openssl dhparam -rand file:/dev/random -outform pem -out /etc/ssl/dh/dhparam4096.pem 4096
```

-   put all ssl configuration parameters into a global configuration
    file at `/etc/apache2/ssl/gnutls.conf`:

``` apache
        # Set HSTS header
        Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"

        # disable insecure SSL protocols
        SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1

        # Enable OCSP response stabling
        SSLUseStapling on
        SSLStaplingResponderTimeout 5
        SSLStaplingReturnResponderErrors off
        SSLStaplingCache "shmcb:${APACHE_RUN_DIR}/stapling_cache(128000)"

        # Enable custom DH parameters
        SSLOpenSSLConfCmd DHParameters "/etc/ssl/dh/dhparam4096.pem"
```

SSH Hardening
=============

-   Disable the SSH 1 protocol
-   Only allow strong ciphers by adding the following directive to
    `/etc/ssh/sshd_config` (maximum keylength and CTR rather than CBC
    since a theoretical attack has been discovered for the later).

``` apache
  Ciphers aes256-ctr
```

-   Configure your SSH client to solely allow `aes256-ctr` by putting
    the following directive into your `~/.ssh/config` file.

``` apache
  Ciphers aes256-ctr
```

Disk Encryption
===============

I highly encourage encryption, especially of removable media, since it
protects yourself of disclosing possibly sensitive data. This page
contains hacks and resources relevant for Linux Hard Disk Encryption.

Encrypted Swap Partition
------------------------

Place an entry for your swap device in `/etc/crypttab` and use the swap
devicemapper device (`/dev/mapper/swap`) in your `/etc/fstab`.

``` bash
  echo "swap /dev/{swapdevice} /dev/urandom swap" >>/etc/crypttab
```

Create a Serpent encrypted LUKS partition
-----------------------------------------

### Step 1: Fill the disk with random data

Use one of the following methods to fill your hard disk with random
data. This makes it harder for an attacker to guess the amount of data
actually stored on the disk.

``` bash
# option 1 - use openssl and aes encryption
#            (pv -pterb is optional, but adds a nice progress bar to the output)
openssl enc -aes-256-ctr -pass pass:"$(dd if=/dev/urandom bs=256 count=1 2>/dev/null | base64)"  < /dev/zero | pv -pterb | dd of=/dev/{device} bs=1M

# option 2 - use python to generate _pseudo_ random data
#            requires python and python-numpy to be installed
python -u -c $'import sys,numpy\nwhile True: sys.stdout.write(numpy.random.bytes(1000000))' | dd of=/dev/{device} bs=1M

# option 3 - use /dev/urandom (slower)
dd if=/dev/urandom of=/dev/{device} bs=1M

# hint - if you still want to work on the system, I recomment to reduce
#        the IO priority of the writer process to 3 using renice.
ps xuaww |grep dd    # determine the PID of the dd process
ionice -c 3 -p PID   # and set it's io priority to idle (only get disk time when no other program has asked for it
```

### Step 2: Encrypt your disk using the serpent algorim

``` bash
  cryptsetup -v --cipher serpent-cbc-essiv:sha256 --key-size 256 luksFormat /dev/{device}   # old encrypten schema
  cryptsetup -v --cipher serpent-xts-plain64      --key-size 512 luksFormat /dev/sdb        # new encryption schema; uses the more advanced xts cipher mode
                                                                                            # and a larger keysize
  cryptsetup -v --cipher serpent-xts-plain64      --key-size 512 --hash sha512 --iter-time 5000 --use-random
                                                                 luksFormat /dev/sdb        # user sha512 for hashing; 5x longer iter time
                                                                                            # use better random source
```

References
==========

-   [Encrypting an existing Debian Lenny
    Installation](http://www.debian-administration.org/article/Encrypting_an_existing_Debian_lenny_installation)
-   [Linux Unified Key
    Setup (LUKS)](http://code.google.com/p/cryptsetup/) at google code.
-   [Secure deletion](http://en.gentoo-wiki.com/wiki/Secure_deletion) -
    contains information on how to fill your hard disk with random data
-   [German Gentoo Wiki](http://de.gentoo-wiki.com/wiki/DM-Crypt) -
    contains interesting information on different cipher modes
-   [Strong SSL Security on
    Apache2](https://raymii.org/s/tutorials/Strong_SSL_Security_On_Apache2.html)

