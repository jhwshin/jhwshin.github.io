---
title: "Arch Linux - Base Install"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# BASE CONFIG

> ## 1. Run Chroot

Run chroot from newly installed arch mount point (settings it as a new root):
```sh
$   arch-chroot /mnt
```

> ## 2. Locale

Uncomment your locale:

`/etc/locale.gen`
```sh
$   nano /etc/locale.gen
```

```sh
...
en_US.UTF-8 UTF-8
...
```
Update the locale:
```sh
$   locale-gen
```

Set locale ENV variable:
```sh
$   echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

> ## 3. Timezone

Create a symlink to `/etc/localtime` with preferred timezone:
```sh
$   ln -s /usr/share/zoneinfo/<REGION>/<CITY> /etc/localtime
```

> ## 4. Hostname

Name your machine:
```sh
$   echo "<HOSTNAME>" > /etc/hostname
```
> ## 5. Hosts

Set hosts (useful for network domain names):

`etc/hosts`
```sh
$   nano /etc/hosts
```
```conf
127.0.0.1   localhost
::1         localhost
```

> ## 6. Add User

Create USER and add to them to group `wheel`:
```sh
$    useradd -m <USERNAME> -G wheel
```

* NOTE: users no longer need to be put into groups (e.g audio, video, storage, etc ...) as `systemd` handles this through `udev`

> ## 7. Setup Password

Set password for USER:
```sh
$   passwd <USERNAME>
```

Set password for root:
```sh
$   passwd
```

> ## 8. Add Sudoers

Add USER GROUP to sudoer to enable them to run with commands with root privilege:
```sh
$   EDITOR=nano visudo
```

Uncomment `wheel` group:
```
...
%wheel ALL=(ALL) ALL
...
```

> ## 9. 32-bit Applications

Uncomment line to allow 32-bit mirrors:

`/etc/pacman.conf`
```sh
$   nano /etc/pacman.conf
```
```conf
[multilib]
Include=...
```

Also I usually like to enable these misc options:
```conf
# Misc options
UseSyslog
Color
#NoProgressBar
CheckSpace
VerbosePkgLists
ParallelDownloads = 5
```

Refresh new mirrors:
```sh
$   pacman -Syy
```
