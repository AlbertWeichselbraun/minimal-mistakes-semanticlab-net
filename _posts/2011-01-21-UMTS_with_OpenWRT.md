---
title: UMTS with OpenWRT
alias: index.php/UMTS_with_OpenWRT/
layout: single
categories: ["Sysadmin", "Linux", "OpenWrt"]
---

These are some random notes on how to use a ZTE MF180 with OpenWRT and
Linux

Required OpenWRT Packages
-------------------------

Required packages:

-   kmod-usb-serial
-   kmod-usb-serial-option
-   ppp
-   usbutils

### Verifying that the ZTE MF180 has been recognized

`lsusb` should yield the following output:

` Bus 001 Device 004: ID 19d2:0117 ONDA Communication S.p.A.`

Enabling the USB Modem
----------------------

In the default configuration the USB Modem mimics a CDROM device.

The following lines disable the CDROM device and enable the UMTS modem:

``` bash
sdparm --command=eject //dev/sg0
insmod usbserial vendor=0x19d2 product=0x0117
insmod option
```

Preparing the Modem for regular use
-----------------------------------

To prepare the modem for regular use I will

1.  disable the PIN and
2.  permanently enable the UMTS modem (by enabling the download mode
    which disables the CDROM device)

### Disable the PIN

Replace `XXXX` with your PIN code.

``` bash
  echo AT+CLCK="SC",0,"XXXX" >/dev/ttyUSB1
```

### Disable CD mode

``` bash
  echo AT+ZCDRUN=E >/dev/ttyUSB1
```

Using UMTS with OpenWRT
-----------------------

Edit `/etc/modules.d/60-usb-serial` the umtserial module at startup

``` text
usbserial vendor=0x19d2 product=0x0117
option
```

Edit `/etc/config/network` to include the following section

``` text
config 'interface' 'wan'
        option 'ifname'  'ppp0'
        option 'device'  '/dev/ttyUSB2'
        option 'apn'     'bob.at'
        option 'service' 'umts'
        option 'proto'   '3g'
        option 'username' 'data@bob.at'
        option 'password' 'ppp'
```

Test the configuration with

``` bash
  ifup wan
```

If everything works out, make the changes persistent by adding `ifup`
`wan` to your `/etc/rc.local`.

Resources
---------

-   [OpenWRT Network Network
    Configuration](http://wiki.openwrt.org/doc/uci/network#protocol.3g.ppp.over.ev-do.cdma.umts.or.grps)
-   [Using a ZTE MF180 on GNU
    Linux](http://christian.amsuess.com/tutorials/zte_mf180/)
-   [AT Command Set for GPRS/3G/UMTS/HSDPA
    Modems](http://www.expertcore.org/viewtopic.php?t=1274)

