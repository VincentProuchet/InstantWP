#  Creating the IWPServer qcow2 file

Open a terminal/command/bash/powershell

Create a new image using qemu-img, 20G in size:
```text
qemu-img create -f qcow2 iwpserver.img 20G
```
Download the Alpine Virtual iso image:
be sur to place it in same file as qemu exe
Then boot the image using qemu-system-i386 and install Alpine:
```text
./qemu-system-i386 \
-m 1024 \
-hda ./iwpserver.img -boot c \
-cdrom ./alpine-virt-3.5.0-x86.iso
-net nic \
-net user,hostfwd=tcp::10022-:22 \
-redir tcp:10080::80 \
-redir tcp:10020::20 \
-redir tcp:10021::21 \
-monitor telnet:127.0.0.1:1234,server,nowait 
```

Change the root password to 'root'.
when prompted

restart the server with reboot command
running 
```
setup-alpine
```
will give you a step by step alpine setup configuration
you can leave most of it by default but the disc must be a "sys" type

Add a user 'iwp' with password 'iwp'.
```
setup-user
```
you will need to setup repositories for alpine package manager
```
setup-apkrepos -cf
```
then update the package list
```
apk update
```
this will take somme time but you won't need to edit any repository

install lastest php version for your alpine linux version
```
apk add php
```

Ssh into the virtual server and install the packages as listed in the installed-packages.md file using the pkg command.

Copy over the files from 2.0.0 via SFTP and reboot.

Also install PHP Composer and WP-CLI.




