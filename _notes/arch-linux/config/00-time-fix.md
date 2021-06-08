---
title: "Dual Boot - Windows"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
redirect_from:
  - /notes/arch-linux/config/
prev-section: /notes/arch-linux/install/12-post-install/
---

# TIME FIX

Windows and Linux may show different times. When dualbooting, configure Windows to use UTC and Arch to use localtime:

* In Windows settings disable “Set time automatically”

* In Arch Linux:
```sh
$   timedatectl set-local-rtc 1 --adjust-system-clock
$   hwclock --systohc --localtime
```
