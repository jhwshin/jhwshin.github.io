---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
---

# Samba

Install package:
```sh
$   yay -S samba
```

From the SERVER side, create config file `/etc/samba/smb.conf`:
```ini
[<SAMBA_SHARE_NAME>]
comment=Description goes here...
path=<PATH_TO_SHARE>
read only = no
browsable = yes
```

* Allows full permission = rw

Enable systemd UNIT file:
```sh
$   systemctl enable smb
$   systemctl enable nmb
```

Samba requires you to create a USER and PASSWORD:
```sh
$   smbpasswd -a <USER>
$   smbpasswd <USER>
```

Finally from CLIENT side to access SHARE_SAMBA_FOLDER:

You may use Nautilus to connect:
```sh
smb://IP//<SAMBA_SHARE_NAME>
```

OR

Write a script/cmd to hotmount when necessary:
```sh
$   sudo mount -t cifs -o "credentials=/home/hws/.smb,uid=<UID>,gid=<GID>" //IP/<SAMBA_SHARE_NAME> <MOUNT_PATH>
```

You could safely store credentials with permissions for better security in `~/.smb`:
```conf
username=<USER>
password=<PASSWORD>
# default domain=WORKGROUP
domain=<DOMAIN>
```
