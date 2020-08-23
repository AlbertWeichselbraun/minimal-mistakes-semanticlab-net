---
title: KVM increase CPU and RAM during runtime
alias: index.php/KVM_increase_CPU_and_RAM_during_runtime/
layout: single
categories: ["virtualization", "sysadmin", "linux"]
---

KVM - Increase CPU and RAM during runtime
=========================================

The page summarises the necessary steps for increasing the amount of
CPUs and RAM allocated to KVM guests during runtime.

Increase RAM during runtime
---------------------------

-   activate the kernel module *Virtio balloon driver* on the guest
    system (maybe also on the host)

` modprobe virtio_balloon`

-   connect to the virtual machine

` ssh user@hostmaschine -L 5900:localhost:5900 `  
` xvncviewer localhost`

-   in the opening qemu window press *Ctrl+Alt+2* (press ''Ctrl+Alt+1
    to return)

` info ballon - shows the allocated memory`  
` balloon 256 - sets the memory to 256MB`

CPU hotpluging
--------------

-   start virtual machine with the maximum of cores

<!-- -->

-   disable a cpu (in Debian)

` echo 0 > /sys/devices/system/cpu/cpu1/online`

-   to enable a CPU (in Debian)

` echo 1 > /sys/devices/system/cpu/cpu1/online`

Ressources
----------

-   [Geraetetreiber - Memory
    Ballooning](http://qemu-buch.de/de/index.php/QEMU-KVM-Buch/_Virtuelle_Hardware/_Paravirtualisierte_Ger%C3%A4tetreiber#Memory_Balloning%7CParavirtualisierte)
-   [Hotplug a
    CPU](http://www.cyberciti.biz/faq/debian-rhel-centos-redhat-suse-hotplug-cpu/%7CLinux)

