# Installation

## Set up WiFi on bootable USB

Find out what your wifi device is called with
```
iwctl device list
```
often it will be called `wlan0`.

Connect to a WiFi network with
```
iwctl station <device> connect <SSID>
```
If you do not know your network's SSID, use
```
iwctl station <device> scan
```

## Run the archinstall script
```
archinstall
```

## Select extra programs to install
Basic setup:
```
bat
btop
exa
fd
firefox
fish
git
github-cli
hyprland
inotify-tools
kitty
lazygit
light
man-db
man-pages
neovim
openssh
pipewire
pipewire-alsa
pipewire-audio
pipewire-pulse
reflector
ripgrep
rustup
stow
sudo
tldr
ttf-fantasque-sans-mono
ttf-firacode-nerd
ttf-joypixels
unzip
zoxide
zsh
```

If using a Wayland compositor, you may also want:
```
swaybg waybar wl-copy wofi
```

If using hyprland, you may want `sddm`.

If using an X based window manager, may also want:
```
feh polybar rofi xorg-xinput
```

## Hyprland
Hyprland works best with [SDDM].

[SDDM]: sddm.md


## Audio
See the ArchWiki page for [PipeWire].

You may want a GUI tool for managing audio sources and syncs.
`qpwgraph` and `helvum` are two options for this.

[PipeWire]: https://wiki.archlinux.org/title/PipeWire#Installation

## User groups
+ `video` to enable backlight control with the `light` utility

```
sudo usermod -aG video $USER
reboot
```

## Change shell to fish
```
exec fish
chsh -s $(which fish)
```

## Setup SSH keys and register them with git
```
ssh-keygen -t ed25519
```

Note: this step requires the `github-cli` package
```
gh auth login
```

## Pull down dotfiles and scripts from GitHub

```
git clone git@github.com:mfdorst/.cfg
git clone git@github.com:mfdorst/scripts
git clone git@github.com:mfdorst/wallpaper
```

## Install dotfiles

Note: this requires the `stow` package
```
.cfg/install
```

If you have a hidpi display, you may also want to
```
cd ~/.cfg
stow hidpi
```

## Install other stuff

```
install-lvim
install-omp # Oh my posh
install-omz # Oh my zsh
install-paru
install-starship

paru -S nerd-fonts-fira-code
```

If using `hyprland`:
```
paru -S hyprland-bin hyprpaper waybar-hyprland
```

## Make updates faster with Reflector

```
sudo pacman -S reflector
```

### Configure the arguments `reflector` will run with on startup

```
sudoedit /etc/xdg/reflector/reflector.conf
```

To make the updates faster, use only the 5 latest US mirrors.

```
--save /etc/pacman.d/mirrorlist
--protocol https
--country 'United States'
--latest 5
--sort rate
```

### Enable `reflector.service` to run on startup

The `--now` flag will make it run immediately.
```
systemctl enable --now reflector
```

Note: the service will not run until you are connected to the internet, so give it a second. If you
want to check if the mirrorlist has updated recently, check the timestamps in
`/etc/pacman.d/mirrorlist`.

## SSH Server

```
sudo pacman -S openssh
sudo systemctl enable sshd
```

If you don't want information about your previous login popping up every time you log in, do
```
touch ~/.hushlogin
```

## Fix monitors switching sides randomly
Create a script that runs an appropriate `xrandr` command, for instance:
```
#!/usr/bin/env bash
xrandr --output DP-4 --mode 1920x1080 --left-of HDMI-0
```
Make it executable
```
chmod +x monitor-setup-script
```

Assuming you are using LightDM:

Edit `/etc/lightdm/lightdm.conf`. In the `[Seat:*]` section, add:
```
display-setup-script = /path/to/monitor-setup-script
```

## Enable backlight keys
```
sudo pacman -S light
usermod -aG video <user>
reboot
```

## Printer setup (Canon PIXMA MG6100)

Install the printer and scanner drivers from the AUR:
```
paru -S canon-pixma-mg6100-complete
```

Get the network address (make sure the printer is on and on the correct network for this step):
```
cnijnetprn --installer --search auto
```

Should print something like:
```
network cnijnet:/00-1E-8F-A4-95-E4 "Canon MG6100 series" "IP:10.0.0.9"
```

Use the `cnijnet:/` address in the following command:
```
sudo lpadmin -p "Canon MG6120 -m canonmg6100.ppd -v cnijnet:/<address> -E
```

