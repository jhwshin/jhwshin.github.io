---
title: "Troubleshooting"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# Packages

> ## >> `pacman`

`$  pacman -v`
```sh
Root      : /
Conf File : /etc/pacman.conf
DB Path   : /var/lib/pacman/
Cache Dirs: /var/cache/pacman/pkg/
Hook Dirs : /usr/share/libalpm/hooks/  /etc/pacman.d/hooks/
Lock File : /var/lib/pacman/db.lck
Log File  : /var/log/pacman.log
GPG Dir   : /etc/pacman.d/gnupg/
```

```sh
--noconfirm
--debug
```

### (-Q) Query = LOCAL
```sh
$ pacman -Q [<PACKAGE>]           # list local packages
$ pacman -Qem                      # list explictly and manually installed package
$ pacman -Qii <PACKAGE>           # (-ii) detailed info
$ pacman -Qs <STRING>             # (-s) search
$ pacman -Qkl <PACKAGE>           # (-k) check files
                                  # (-l) list files
```

### (-S) Sync = REMOTE
```sh
$ pacman -S <PACKAGE>             # install package
$ pacman -Syyu                    # (-yy) force refresh database
                                  # (-u) upgrade

$ pacman -Si <PACKAGE>            # (-i) info
$ pacman -Ss [<STRING>|'<REGEX>'] # (-s) search
$ pacman -Sg <PACKAGE>            # (-g) print group packages
$ pacman -Sp <PACKAGE>            # (-p) print group packages links

$ pacman -Fyy <PACKAGE>           # Search Only
$ pacman -Sw package_name         # download but dont install - /var/cache/pacman/pkg/
$ pacman -U <PACKAGE>.pkg.tar.zst # Manual install
```

### (-R) Remove
```sh
$ pacman -R <PACKAGE>             # remove package
$ pacman -Rsn <PACKAGE>           # (-s) remove unused dep
                                  # (-n) remove configs
$ pacman -Rs $(pacman -Qdt)       # remove orphaned files (not req as dep)
                                  # (-d) dependencies
                                  # (-t) not required
$ pacman -Scc                     # remove all cache
```

List package dependencies as tree:
```sh
$   pactree <PACKAGE>
```

To ignore certain packages:

`/etc/pacman.conf`
```
...
IgnorePkg=linux
...
```

### Keys - TODO

```sh

```

> ## >> `downgrade`

Since Arch is bleeding edge rolling release, some new packages may be less stable.
Hence sometimes you may need to downgrade a package to older versions.
