---
title: "Arch Linux - Preparation"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# PRE-INSTALL

## 1. Font Size
To increase font size for HiDPI monitors - _[OPTIONAL]_:
```sh
$   setfont latarcyrheb-sun32.psfu.gz
```

## 2. Sync Hardware Clock
Sync system clock:
```sh
$   timedatectl set-ntp true
```

Check the if the time is correct with service status:
```sh
$   timedatectl status
```

## 3. System Firmware

> ### >> BIOS or UEFI

Check if system is running UEFI firmware (modern standard):
```sh
$   ls /sys/firmware/efi/efivars
```

Otherwise, if it doesn't exist its likely running BIOS (legacy)

> __WARNING:__ This will delete all boot entries! Don't use this command unless you know what this does.
* Sometimes there are residue bootloaders saved in NVRAM not on disk\
To delete UEFI Boot Entries in NVRAM - _[OPTIONAL]_:
```sh
$   rm -rf /sys/firmware/efi/efivars/Boot*
```

## 4. Internet Connection

Internet connection is __REQUIRED__ for an Arch Linux install.

> __WiFi or Ethernet__

List network interfaces:
```sh
$   ip link
```

> ### >> WiFi

```sh
$   iwctl
```

> ### >> Ethernet

Usually not required as ethernet connection is enabled automatically, but incase it doesn't:
```sh
$   systemctl start dhcpcd@<INTERFACE>
```

<br>

Finally check the internet connection:
```sh
$   ping -c 8.8.8.8
```
