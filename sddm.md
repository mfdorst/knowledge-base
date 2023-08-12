# SDDM

Install and enable SDDM
```
sudo pacman -S sddm
systemctl enable sddm --force
```

See the [SDDM Arch Wiki page][1] for details.

## Autologin
Edit `/etc/sddm.conf.d/autologin.conf`. You may need to create the directory first.
```
[Autologin]
User=me
Session=hyprland
```

[1]: https://wiki.archlinux.org/title/SDDM
