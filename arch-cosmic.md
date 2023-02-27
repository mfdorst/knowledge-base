_See also: [cosmic-epoch-git (AUR)]_

# Building Cosmic DE from source
_Cosmic DE is still under development, so these instructions may change._
_Check the README for up-to-date info: [Cosmic DE]_

## Install dependencies
This is a non-exhaustive list.
Translated from the Debian packages listed on the `[Cosmic DE]` repo.
+ `just`
+ `rust`
+ `wayland`
+ `mesa`
+ `seatd`
+ `libxkbcommon`
+ `libinput`
+ `gtk4`
+ `dbus`
+ udev is listed, but there is no package for it on Arch

### Optional dependencies
May be required by the build system.
+ `systemd-libs`
+ `libpulse`
+ pop-launcher is listed, but there is no package for it on Arch
+ `expat`
+ `fontconfig`
+ `freetype2`
+ `lld`

### Previously required
I listed these packages previously, maybe they used to be requirements and aren't anymore?
+ `libadwaita`
+ `meson`

## Clone the repo
```
git clone git@github.com:pop-os/cosmic-epoch --recurse-submodules
```

## Build
From the `cosmic-epoch` directory:
```
just sysext
```

## Copy the system extension
```
sudo mkdir -p /var/lib/extensions
sudo cp cosmic-sysext /var/lib/extensions
```

## Start the sysext service
```
sudo systemctl enable --now systemd-sysext
sudo systemd-sysext refresh
```

[Cosmic DE]: https://github.com/pop-os/cosmic-epoch
[cosmic-epoch-git (AUR)]: https://aur.archlinux.org/packages/cosmic-epoch-git
