# Building Cosmic DE from source
_Cosmic DE is still under development, so these instructions may change._
_Check the README for up-to-date info: [Cosmic DE]_

## Install dependencies
```
sudo pacman -S dbus gtk4 just libadwaita libinput libpulse libxkbcommon meson seatd systemd-libs wayland
```

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
