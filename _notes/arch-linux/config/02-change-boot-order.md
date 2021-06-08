---
title: "Dual Boot - Windows"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# CHANGE BOOT ORDER

Changing boot order remotely through SSH.

Lets say you remotely boot your system with WoL (Wake on LAN).

You want to boot into Linux, but system boots into Windows (or vice versa) and connect via SSH.

The only way you could get the system to boot a specific OS is to boot into anyone of them first, and then change the boot order in your Bootloader.

Firstly SSH into either system:
```sh
$   ssh <IP>
```

> ## >> Windows to Linux:

Run `diskpart` and mount EFI partition:
```powershell
$   diskpart

# List Mounted Volumes
$   list vol

# List Disks
$   list disk
$   sel disk <DISK_NUM>

# List Partitions in Disk
$   list part
$   sel part <PART_NUM>
$   assign letter=<LETTER>
```

Run bash in Windows:
```powershell
$   bash
```

* Edit `refind.conf` (my bootloader) to change boot order:
```sh
$   nano EFI/refind/refind.conf
```
OR

* Simply run a script (you can write yourself):
```sh
$   sh EFI/refind/changeboot.sh [windows|arch|default]
```

Finally, unmount EFI partition, or simply reboot:
```powershell
$   diskpart
$   list vol
$   sel vol <VOL>
$   remove letter=<LETTER>

$   reboot
```

> ## >> Linux to Windows:

* Much simpler as boot is already mounted in Linux:
```sh
$   nano /boot/efi/EFI/refind/refind.conf
```
OR

* Simply run the script (if you have one):
```sh
$   sh /boot/efi/EFI/refind/changeboot [windows|arch|default]
```

Simply, reboot:
```sh
$   reboot
```
