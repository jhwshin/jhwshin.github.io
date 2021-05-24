---
title: "Arch Linux - Disk Partition"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# PARTITION TABLE

List disks and partitions:
```sh
$   fdisk -l
```

## 1. Partition Table

> __GPT or MBR__

Choose disk and partition table then format accordingly:
```sh
$   fdisk /dev/<sdX>
```

* If Dual Booting with Windows and is already installed the boot partition probably already exist, so DO NOT create a new one.

> ### >> GPT [UEFI]

|Label|Mount|Type|Size|
|---|---|---|---|
|boot (BOOT FLAG ON)|`/mnt/boot/efi`|EFI|~300 MB|
|root|`/mnt`|ext4|> 2GB|
|SWAP - [OPTIONAL]|-|swap|> RAM_SIZE|

> ### >> GPT [BIOS]

|Label|Mount|Type|Size|
|---|---|---|---|
|- (BOOT FLAG ON)|-|-|1 MB|
|root|`/mnt`|ext4|> 2GB|
|SWAP - [OPTIONAL]|-|swap|> RAM_SIZE|

* 1 MB at the start only need for GPT/BIOS for GRUB

> ### >> MBR [BIOS]

|Label|Mount|Type|Size|
|---|---|---|---|
|root (BOOT FLAG ON)|`/mnt`|ext4|> 2GB|
|SWAP - [OPTIONAL]|-|swap|> RAM_SIZE|
|-|-|-|16.5 KB|

* 16.5 KB at the end of disk allows GPT conversion if needed incase

## 2. Format Partitions

> Format `boot` Partition (UEFI ONLY) to FAT32

* Again, if Dual Booting DO NOT format otherwise the Windows Bootloader will be deleted and you won't be able to boot Windows.

```sh
$   mkfs.fat -F32 /dev/<sdXY>
```

> Format `root` Partition to ext4

```sh
$   mkfs.ext4 /dev/<sdXY>
```

## 3. Mount Drives

Mount __root__ partition:
```sh
$   mount /dev/<sdXY> /mnt
```

Mount __boot__ partition (UEFI ONLY):
```sh
$   mkdir -p /mnt/boot/efi
$   mount /dev/<sdXY> /mnt/boot/efi
```
