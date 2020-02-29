---
title: "Systemd Nspawn Raspbian"
date: 2018-07-12T23:30:42+02:00
draft: false
tags: [linux, lxd, systemd-nspawn, qemu, raspberry, embedded]
---

# use systemd-nspawn to boot raspbian image

The setup is a bit tricky and some things might have to be changed, but it
should basically work.

1. setup the loopback devive using: `loosetup -f -P <path_to_img>.img` as root
   and lets assume the output is /dev/loop1.
2. make sure you have the prerequistes:

* qemu-user-static
* binfmt-support

3. run `sudo update-binfmts --enable qemu-arm` or something similar
4. create a mount point, lets assume mnt in the current directory
5. mount the image `mount /dev/loop1p1 mnt`
6. try to start a chroot using `systemd-nspawn --bind /lib64  --bind /usr/bin/qemu-arm-static -D mnt /bin/bash` as root. if it works you can add the boot option and see if that works as well

On issues check the output of file mnt/bin/bash to see if you use the correct qemu

## Update

It seems that systemd-nspawn can despite all this not boot some images, the
chroot however should work for all.
