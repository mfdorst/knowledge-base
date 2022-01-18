# Setup KDE on Manjaro

## Install `libinput-gestures`

Provides trackpad gestures.

```
pacman -S libinput-gestures
```

Configure with `~/.config/libinput-gestures.conf`.

## Start and stop

To run the daemon immediately:
```
libinput-gestures-setup desktop start
```

To enable on startup:
```
libinput-gestures-setup autostart
```

If it's broken, try:
```
libinput-gestures-setup stop autostop destkop start
```

Note: using `service` rather than `desktop` is theoretically possible, but doesn't seem to work on
Manjaro.

