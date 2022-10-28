# Run the archinstall script
```
archinstall
```

## Select extra programs to install
Basic setup:
```
bat exa fd firefox fish git github-cli inotify-tools kitty light man neovim reflector ripgrep rustup stow tldr ttf-fantasque-sans-mono ttf-fira-code unzip zoxide zsh
```

If using an X based window manager, may also want:
```
feh polybar rofi xorg-xinput
```

If using a wayland compositor, you may also want:
```
waybar wofi
```

To avoid sound issues on some machines you may want:
```
pulseaudio
```
### Post install for `hyprland`

If using `hyprland`, you will also want these from the `AUR`:
```
hyprland-bin hyprpaper waybar-hyprland
```
See [arch-setup](./arch-setup.md) for details.

## User groups
+ `video` to enable backlight control with the `light` utility

```
sudo usermod -aG video $USER
reboot
```
