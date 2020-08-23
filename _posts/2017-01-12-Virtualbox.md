--- 
title: Installing virtual appliances and VirtualBox
layout: single
categories: virtualization
--- 

How to install virtual appliances on VirtualBox.

## Install VirtualBox

Download VirtualBox from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) (please use the amd64 versions)

## Install the virtual appliance:

* Download the virtual appliances:
  1. Database Management Systems (DBMS): Postgresql, PhpPgAdmin and example databases 
     [Download](http://drive.switch.ch/index.php/s/CiG5t0Xo1wFAnMU){: .btn} [Mirror](https://mega.nz/#!kZg3EDiJ!6B5FSJeAeEUWIxFlW0DWs3nX0Pi2MM-5z4Gw_A71j_k){: .btn .btn--inverse}
  2. Semantic Technologies (GSET): RDF4J and example linked data 
     [Download](https://drive.switch.ch/index.php/s/ovWLcJddEqq91N0){: .btn} [Mirror](https://mega.nz/#!VFZn3J6L!rkJ_KRvwpUBoCNUhDfWkuH2v5e0K4N9U0g-Udj5yCr8){: .btn .btn--inverse}
 * Install the virtual appliance by double-clicking the downloaded `.ova` file.

## Virtualbox Troubleshooting

On some systems virtualization is disabled in the computer's BIOS/UEFI. You need to enable this feature as outlined in the following articles:

 1. http://www.fixedbyvonnie.com/2014/11/virtualbox-showing-32-bit-guest-versions-64-bit-host-os/ 
 2. Most systems allow you to change into the BIOS/UEFI by pressing `ESC`, `F2` or `F10` during startup.
 3. Windows 8 and higher might require you to follow the following instructions: [BIOS/UEFI for Windows 8+](https://support.lenovo.com/at/en/documents/ht081446)

