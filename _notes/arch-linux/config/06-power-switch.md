---
title: "Power Settings"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# Power Switch

> ## >> Power Buttons / Lid Action

`/etc/systemd/login.conf`
```ini
[Login]
#NAutoVTs=6
#ReserveVT=6
#KillUserProcesses=no
#KillOnlyUsers=
#KillExcludeUsers=root
#InhibitDelayMaxSec=5
#UserStopDelaySec=10
#HandlePowerKey=poweroff
#HandleSuspendKey=suspend
#HandleHibernateKey=hibernate
#HandleLidSwitch=suspend
#HandleLidSwitchExternalPower=suspend
#HandleLidSwitchDocked=ignore
#HandleRebootKey=reboot
#PowerKeyIgnoreInhibited=no
#SuspendKeyIgnoreInhibited=no
#HibernateKeyIgnoreInhibited=no
#LidSwitchIgnoreInhibited=yes
#RebootKeyIgnoreInhibited=no
#HoldoffTimeoutSec=30s
#IdleAction=ignore
#IdleActionSec=30min
#RuntimeDirectorySize=10%
#RuntimeDirectoryInodes=400k
#RemoveIPC=yes
#InhibitorsMax=8192
#SessionsMax=8192
```

> ## >> Power Modes

Suspend, Hibernate, Hybrid-Suspend, Suspend-then-Hibernate

`/etc/systemd/system/sleep.conf`
```ini
[Sleep]
#AllowSuspend=yes
#AllowHibernation=yes
#AllowSuspendThenHibernate=yes
#AllowHybridSleep=yes
#SuspendMode=
#SuspendState=mem standby freeze
#HibernateMode=platform shutdown
#HibernateState=disk
#HybridSleepMode=suspend platform shutdown
#HybridSleepState=disk
#HibernateDelaySec=180min
```

> ## >> Wake-on-LAN

`ethtool` allows you to check and enable your network device for WoL feature.

Install package:
```sh
$   yay -S ethtool
```

Check if your device supports WoL:
```sh
$   ethtool <DEVICE>
```

Enable WoL:
```sh
$   ethtool -s <DEVICE> wol g
```

Sometimes WoL feature is disable for a specific Linux Kernel. Hence you may need to manually patch a network device module:

e.g [alx-wol-dkms](https://github.com/jhwshin/alx-wol-dkms)
