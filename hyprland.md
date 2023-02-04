# Hyprland

## Display manager
Works best with SDDM. Currently, the latest SDDM shipped with Arch has a bug where it hangs on
shutdown, so use `sddm-git` from the AUR.

```
paru -S sddm-git
systemctl enable sddm.service --force
```

See the [SDDM Arch Wiki page][1] for details.

Then, edit the `Exec` field of the Hyprland desktop entry to run a wrapper script.

`/usr/share/wayland-sessions/hyprland.desktop`:
```
Exec=/home/michael/scripts/hyprland-launch
```
Or, for an Nvidia system,
```
Exec=/home/michael/scripts/hyprland-launch-nvidia
```

**NOTE:** Your package manager will likely overwrite the `hyprland.desktop` file every time you
upgrade Hyprland, so you will need to do this again each time.

See my [scripts][2] repo on GitHub.

[1]: https://wiki.archlinux.org/title/SDDM
[2]: https://github.com/mfdorst/scripts
