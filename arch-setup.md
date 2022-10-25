# General setup instructions for Arch

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
git clone git@github.com:mfdorst/.conf
git clone git@github.com:mfdorst/scripts
```

## Install dotfiles

Note: this requires the `stow` package
```
.conf/install.sh
```

## Install other stuff

```
install-lvim
install-omp # Oh my posh
install-omz # Oh my zsh
install-paru
install-starship
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

```
systemctl enable reflector
```

To run immediately:

```
systemctl start reflector
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

Edit `/etc/lightdm/lightdm.conf`
```
display-setup-script = /path/to/monitor-setup-script
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

