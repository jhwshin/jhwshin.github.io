---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
---

# Syncthing

Install Syncthing and tray:
```sh
$   pacman -S syncthing syncthingtray
```

Run syncthing then tray:
```sh
$   syncthing
$   syncthingtray
```

Open syncthingtray `Settings`, in tab `Connection`, click `Insert values from local Syncthing configuration` and apply `Connect automatically on startup`

Then enable syncthing:
```sh
$   systemctl enable syncthing@<USER>
```

Allow systemd UNIT files to run REGARDLESS of USER login:
```sh
$   loginctl enable-linger hws
```

Finally, to start tray icon in `i3`:
```sh
exec syncthingtray
```

* NOTE: Don't forget to set password for syncthing!
