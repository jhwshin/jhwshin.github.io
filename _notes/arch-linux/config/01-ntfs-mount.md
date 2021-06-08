---
title: "Dual Boot - Windows"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# NTFS MOUNT

Install ntfs package:
```sh
$   pacman -S ntfs-3g
```

Edit `fstab` file to auto mount at boot:
```sh
$   nano /etc/fstab
```

Add entry:

`/etc/fstab`
```
UUID=<UUID>   <MOUNT_PT>   ntfs-3g   defaults,rw,uid=<UID>,gid=<GID>,nofail,windows_names	0	0
```

Sometimes when mounting NTFS it may mount as a read-only system:

```
...
Metadata kept in Windows cache, refused to mount.
Falling back to read-only mount because the NTFS partition is in an
unsafe state.
...
```

> * NOTE: You can not write to files in hibernated Windows partition as it may corrupt. If you want to mount to write Windows OS partitions you need to disable Hibernation from Windows.

To fix, run:
```sh
$   sudo ntfsfix /dev/<sdXY>
```

If above fails and you get a hibernation error:
```sh
$   sudo mount -t nfts-3g -o remove_hiberfile /dev/<sdXY> <MOUNT_PT>
```
