--- 
title: Headless Seafile server on a Raspberry Pi 2 with dynamic DNS
layout: single
categories: ["linux", "seafile", "raspberry pi"]
--- 

The Raspberry Pi is operated from at home keeping noise and power consumption in mind.


### Install Raspbian on Pi

 1.Download and install [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) on the SD card. Before rebooting the device mount the `boot` partition and create an empty file named `ssh` on the partition.
 2. Put the SD card into the Raspberry Pi, boot the system and determine its IP address with
    ```bash
    nmap -sn 192.168.1.0/24
    ```
 3. Log into the PI (`user`: `pi`, `password`: `raspberry`) and run `sudo raspi-config` to
    * Change the login password
    * Maximize the rootfs with `expand_rootfs`.

### Change the root file system to F2FS

  * mount the SD card and copy the content of the root filesystem to a temporary directory
  * unmount the rootfs file system and format its partition (e.g. `/dev/mmcblk0p2`)
  * restore the root partitions content

  ```bash
  mkdir /tmp/rpi
  cp -a /media/{user}/root_fs /tmp/rpi
  umount /media/{user}/root_fs
  mkfs.f2fs /dev/mmcblk0p2
  mount /dev/mmcblk0p2 /mnt
  cp -a /media/{user}/root_fs/ /mnt/
  ```

  * adapt `cmdline.txt` and `fstab` to reflect the changed file system type:
    * `/media/{user}/boot_fs/cmdline.txt`: change `rootfstype=ext4` to `rootfstype=f2fs`
    * `/mnt/etc/fstab`: change the file system type for `/dev/mmcblk0p2` to `f2fs` and add the `discard` option
      ```
      /dev/mmcblk0p1  /boot  vfat    defaults          0       2
      /dev/mmcblk0p2  /      f2fs    defaults,noatime,discard  0       1
      ```

### Remove unnecessary components and reduce power consumption

 1. remove unnecessary services
    ```bash
    apt-get remove --purge avahi-daemon triggerhappy`
    ```
 2. disable HDMI (-25 mA) and LEDs (-5 mA per LED) by adding the following commands to `/etc/rc.local`:
    ```
    # disable hdmi (25 mA)
    /usr/bin/tvservice -o
    
    # disable leds (5 mA per LED)
    echo 0 |tee /sys/class/leds/led0/brightness
    echo 0 |tee /sys/class/leds/led1/brightness
    ```

### Dynamic DNS with dynu.com
[Dynu.com](https://www.dynu.com/) offers a dynamic DNS service which lets you (optionally) use your own domain name for dynamic DNS. The following steps refer to this case.

* set the `NS` entries for the chosen name to the dyno name servers:
  ```
  myname.semanticlab.net    3600    IN  NS ns1.dynu.com.
  myname.semanticlab.net    3600    IN  NS ns2.dynu.com.
  myname.semanticlab.net    3600    IN  NS ns3.dynu.com.
  myname.semanticlab.net    3600    IN  NS ns4.dynu.com.
  myname.semanticlab.net    3600    IN  NS ns5.dynu.com.
  myname.semanticlab.net    3600    IN  NS ns6.dynu.com.
  ```
* setup a dynu account and configure the given account for dynamic dns.
* use the dynu dynamic dns client or setup your router to update the dynamic dns address when required.


### Install Seafile and nginx

* Prerequisites: install the necessary dependencies for running seafile and nginx
  ```bash
  apt-get install -y nginx mysql-server python-request python-mysqldb python-pil
  ```
* Download the [Seafile server for Raspberry Pi](https://www.seafile.com/en/download/) and follow the provided install instructions.
* Optional: to enable webdav with nginx change `./seafile/conf/seafdav.conf` to
  ```
  [WEBDAV]
  enabled = true
  port = 8080
  fastcgi = false
  share_name = /seafdav
  ```
  and add the following section to your nginx configuration
  ```
  # webdav
  location /seafdav {
  	proxy_pass         http://127.0.0.1:8080;
  	proxy_set_header   Host $host;
  	proxy_set_header   X-Real-IP $remote_addr;
  	proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
  	proxy_set_header   X-Forwarded-Host $server_name;
  	client_max_body_size 0;
  
  	proxy_connect_timeout  36000s;
  	proxy_read_timeout  36000s;
  	proxy_send_timeout  36000s;
  
  	send_timeout  36000s;
    proxy_request_buffering off;
  }
  ```

### Port forwarding and split DNS

* Log into the configuration interface of your router and
  1. setup a fixed IP address for your Raspberry Pi
  2. enable port forwarding to forward the following ports to the Raspberry Pi:
     * external 80 to Raspberry 80 (http)
     * external 443 to Raspberry 443 (https)
  3. optional: if you can access the Raspberry's Web service from the Internet but not from within your network your router does not support NAT loopback. In this case we need to setup split DNS to ensure that the Raspberry is accessible with the same DNS name from internal as well.
     * install unbound with `apt-get install unbound`
     * add the following changes to `/etc/unbound/unbound.conf` to enable network-wide access to the name server as well as split dns:
       ```
       # network wide access
       interface: 0.0.0.0
        
       # overwrite dns responses
       local-zone: myname.semanticlab.net transparent
       local-data: "myname.semanticlab.net A {your-pi-ip}"
       ```
    * restart unbound with `service unbound restart` 
    * change the DNS server on your router to the ip address of your pi


### HTTPS with letsencryt

Install certbot with `apt-get install python-certbot-nginx` and then follow the instructions on the [EFF Certbot page](https://certbot.eff.org/).


### References

 1. [Headless Raspberry Pi Setup](https://hackernoon.com/raspberry-pi-headless-install-462ccabd75d0)
 2. [Howto: Replace the micro SD card's ext4 partition with f2fs](http://whitehorseplanet.org/gate/topics/documentation/public/howto_ext4_to_f2fs_root_partition_raspi.html)
