# Instructions for setting up GNOME 40 on Arch

## Set up multitouch gestures on X11

GNOME Shell extension: X11 Gestures

+ https://extensions.gnome.org/extension/4033/x11-gestures

This extension requires `touchegg` to be running. Touchegg can be acquired from the AUR.

+ https://github.com/JoseExposito/touchegg#readme

```sh
paru -S touchegg
sudo systemctl enable touchegg.service
sudo systemctl start touchegg
```

## Make the dock reappear when you mouse over it

GNOME Shell extension: Dash to Dock

+ https://extensions.gnome.org/extension/307/dash-to-dock

## Make the top bar go away until you mouse over it

GNOME shell extension: Hide Top Bar

+ https://extensions.gnome.org/extension/545/hide-top-bar

By default the top bar will not show at all unless you are in exposee mode. However there is a setting which will make it pop up when you mouse to the top of the screen. With this setting enabled, the top bar is way too transparent, so use the following extension to rectify that:

## Adjust the top bar opacity

GNOME Shell extension: The Transparent Top Bar (Adjustable Transparency)

+ https://extensions.gnome.org/extension/3960/transparent-top-bar-adjustable-transparency

## Disable overview showing at startup

GNOME Shell extension: No overview at startup

+ https://extensions.gnome.org/extension/4099/no-overview
