---
title: "Arch Linux - Installation"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
redirect_from:
  - /notes/arch-linux/
  - /notes/arch-linux/install/
toc: false
first-post: true
---

These notes were written for my own reference when installing Arch. They have been updated over time as I learned more about Linux while fixing little bugs and adding details.

These were consolidated from various sources (way too many to list), such as [Arch wiki](https://wiki.archlinux.org/) and a lot of googling.

I've also written a very basic script to automate the install to speed up many reinstalls:

[__Arch Linux Auto - Installer__](https://github.com/jhwshin/arch-install.git)

Otherwise, to install it manually follow the instructions below. This process has helped me understand Linux much better and I hope these notes are as helpful to you as it was to me!

---

> __WARNING:__
* For safety assurances backup your partition/disk.
* DO NOT blindly input these commands but rather refer to [Arch wiki](https://wiki.archlinux.org/) please RTFM.
* Use these notes at your own risk as your systems may vary!

---

# BOOTABLE USB

1. [[Download]](https://www.archlinux.org/download/) - Arch ISO Image

2. Verify image signature for security using `gpg` (LINUX):
```sh
$   gpg --keyserver-options auto-key-retrieve --verify /<PATH_TO_ISO>/archlinux.iso.sig
```

3. Copy ISO to USB using `dd` (Linux) or [ventoy (Open Source)](https://www.ventoy.net/en/download.html) / [YUMI](https://www.pendrivelinux.com/yumi-multiboot-usb-creator/) (Windows):
```sh
$   dd bs=4M if=/<PATH_TO_ISO>/archlinux.iso of=/dev/<sdX> status=progress && sync
```

4. Boot to USB - (disable Secureboot from BIOS if needed)
