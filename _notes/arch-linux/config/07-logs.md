---
title: "Troubleshooting"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# Logs and Info

> ## >> Systemd - `journalctl`

The most useful and widely used logging  tool is `journactl`

### Log Levels

|0|Emergency|emerg|Servere Kernel BUG|
|1|Alert|alert|Data loss|
|2|Critical|crit|Crash and coredumps|
|3|Error|err|Error reports|
|4|Warning|warning||
|5|Notice|notice||
|6|Informational|info||
|7|Debug|debug||

### Commands
```sh
-e              #   follow
-f              #   tail
-r              #   reverse
-x              #   verbose
-n N            #   N lines
--no-pager      #   no pages

#   levels
$   journalctl -p err..alert
#   kernel only
$   journalctl -k

#   boot
$   journalctl --list-boots
$   journactl -b [-N]

#   timeframe
$   journalctl --since= "20 min ago"

#   unit file
$   journalctl -u SERVICE
$   journalctl _PID=<PID>
```

### Log Size

```sh
$   journalctl --disk-usage
$   journalctl --vacuum-size=100M
$   journalctl --vacuum-time=2weeks
```

`/etc/systemd/journald.conf`
```ini
SystemMaxUse=50M
```

### Kernel Boot - Log Parameters

`systemd.log_level=debug`

---

> ## >> `/var/log`

Sometimes non-systemd logs can be found in `/var/log`, for example:
* `/var/log/Xorg.log`
* `~/.local/share/xorg/Xorg.log`

---

> ## System Information

### ls*

|`lspci`|PCI|
|`lsdev`|Devices|
|`lscpu`|CPU|
|`lsblk`|Block Devices|
|`lsusb`|USB|
|`lshw`|Hardware|
|`lsmod`|Modules|

### Other

|`uname`|Machine Details|
|`hwinfo`|Hardware Info|
|`inxi`|Hardware Info|
|`modinfo`|Module Info|
|`dmidecode`|BIOS/Powersupply|
|`glxinfo`|GPU Info|
|`netstat`|Network Info|
|`htop`|Process Info|
|`df`|Disk Usage|
|`du`|Dir Usage|
|`free`|Swap Usage|
