--- 
title: Creating cross-platform portable Virtual Machines with Docker
layout: single
categories: virtualization
--- 

1. create a docker virtualbox machine and connect to it 
   ```bash
   docker-machine create dbms
   eval "$(docker-machine env dbms)"
   ```
2. build the docker image
   ```bash
   docker build --rm --tag albert/dbms:current .
   ```

3. modify the machine to start the docker image at startup
   ```
   docker-machine ssh dbms
   vi /mnt/sda1/var/lib/boot2docker/bootlocal.sh
   ```
   with content
   ```bash
   #!/bin/sh
   
   # wait until docker has been started
   while ! docker version; do sleep 1; done
   
   docker run --network=host albert/dbms:current
   ```
4. make the startup script executable with `chmod a+x /mnt/sda1/var/lib/boot2docker/bootlocal.sh`.

5. convert the boot2docker iso file to the `vdi` format.
   ```
   VBoxManage convertdd ~/.docker/machine/cache/boot2docker.iso ~/.docker/machine/cache/boot2docker.vdi --format VDI
   ```
   
   This step is required since VirtualBox does not include `.iso` files in `.ova` archives and without the file your machine does not boot.
   {: .notice--info}

6. Setup port forwarding, to expose services to localhost:
   * Open the VM network settings in VirtualBox
   * Choose `Advanced` and open the `Port Forwarding` dialog
   * Setup the relevant port forwarding rules with host IP `127.0.0.1`


7. finalize and export
   * open the created virtual machine in VirtualBox
   * open the machine's `Settings > Storage` and 
     - delete the `Optical Drive` in the Storage tree
     - select `Add Hard Disk` > `Choose existing disk` and choose the vdi file created above (`~/.docker/machine/cache/boot2docker.vdi`).
   * use `File > Export Appliance` to export the virtual machine


### Literature

* [VirtualBox Docker Machine  Howto](http://linoxide.com/linux-how-to/host-virtualbox-docker-machine/)
* [boot2docer FAQ on local customizations](https://github.com/boot2docker/boot2docker/blob/master/doc/FAQ.md#local-customisation-with-persistent-partition)



