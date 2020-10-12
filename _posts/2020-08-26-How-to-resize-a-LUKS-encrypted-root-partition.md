---
status: published
published: true
title: How to resize a LUKS encrypted root partion
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
The Ubuntu standard setup for an encrypted root file system is quite complex as the following output shows:

```bash
root@ephiphany~# lsblk
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
vda                 252:0    0     1T  0 disk
├─vda1              252:1    0     1M  0 part
├─vda2              252:2    0     1G  0 part  /boot
└─vda3              252:3    0  1024G  0 part
  └─dm_crypt-3      253:0    0  1024G  0 crypt
    └─epiphany-root 253:1    0  1024G  0 lvm   /
``` 

Basically we have a disk (`vda`) with the root partition on the `vda3` partion which holds the encrpyted LUKS device which is decrypted as `dm_crypt-3`. On top of `dm_crypt-3` we have a physical LVM volume with volume group `epiphany` and the logical volume `root`.

Consequently, growing the root filesystem requires:
 1. extending the vda3 paritition which is done using fdisk (please refer to a the the following [guideline](https://access.redhat.com/articles/1190213) for more information)
 2. resizing the LUKS parition
 3. resizing the physical device, 
 4. resizing the logical device, and finally
 5. growing the file system

as outlined below:

```bash
# resize the LUKS parititon (dm_crypt-3)
cryptsetup resize dm_crypt-3

# resize the physical device on top of it
pvresize /dev/mapper/dm_crypt-3 

# resize the logical device (epiphany-root)
lvextend -l +100%FREE /dev/mapper/epiphany-root

# grow the file system accordingly
resize2fs /dev/mapper/epiphany-root
```


