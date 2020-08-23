---
title: Handling Disk Errors
layout: single
alias: index.php/Handling_Disk_Errors
categories: sysadmin
---

You can verify that your hard disk does not contain any defect sectors
by performing a disk selftest using SMART (replace /dev/sda in the
examples with your drive):

``` bash
  smartctl -t long /dev/sda
```

After some time you can access the results with

``` bash
  smartctl -a /dev/sda
```

A faulty block will be indicated by a "read failure":

```
 SMART Self-test log structure revision number 1  
 Num  Test_Description    Status                  Remaining  LifeTime(hours)  LBA_of_first_error  
 # 1  Extended offline    Completed: read failure       40%      7516         976697037
```

What you need to do is forcing your disk to reallocate this sector.

This also means that the **data** on this sector will be **lost** (which is the reason why the disk does not automatically reallocate the sector). 
{: .notice--warning}

A detailed guide for how to deal with this situation is provided by the
[Bad block HOWTO](http://smartmontools.sourceforge.net/badblockhowto.html) for
smartmontools.

Strangely, the steps suggested in the HOWTO did not work with my drive,
so that I performed the following steps:

``` bash
hdparm --yes-i-know-what-i-am-doing --repair-sector 976697037 /dev/sdb
sg_verify --lba=976697037
```

Which finally fixed the defect sector.
