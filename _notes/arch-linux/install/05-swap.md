---
title: "Arch Linux - Disk Partition"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# Swap - [RECOMMENDED]

Swap is REQUIRED if you want to enable HIBERNATION.

> __File or Partition__

Swap files are more flexible as they are resizable, however swap partitions are less prone to corruption as they are allocated their own partitions and are known to be slightly faster.

> ## >> File

> I prefer settings up swapfile AFTER installation.

"Zero-Fill" format swap file - Important that swap file has 'no holes':

* bs=1M x count=512 = 512MB

```sh
$   dd if=/dev/zero of=/swapfile bs=<SIZE> count=<COUNT> status=progress
```

Change permission (600 = o+rw) for security, format swapfile with `mkswap` and then finally turn on swap:
```sh
$   chmod 600 /swapfile
$   mkswap /swapfile
$   swapon /swapfile
```

Add entry to:

`/etc/fstab`
```ini
/swapfile none swap defaults 0 0
```

> ## >> Partition

Make swap partition and then turn it on:
```sh
$   mkswap /dev/<sdXY>
$   swapon /dev/<sdXY>
```

It should automount when generating fstab `genfstab` during step 3 of __Arch Base__

> ## Encryption - [OPTIONAL] - #TODO
