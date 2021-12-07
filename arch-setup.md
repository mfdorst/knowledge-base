# General setup instructions for Arch

## Pull down dotfiles and scripts from GitHub

```
git clone https://github.com/mfdorst/cfg .cfg
git clone https://github.com/mfdorst/scripts
```

## Install dotfiles

```
.cfg/install
```

## Install Oh-My-Zsh and Starship Prompt and Rustup

```
scripts/install-omz
scripts/install-starship-prompt
scripts/install-rustup
```

## Install quality-of-life tools for the terminal

```
sudo pacman -S alacritty neovim tty-fira-code hub
```

## Install useful rust utilities

```
cargo install paru bat fd-find ripgrep
```

## Install brave browser

```
paru -S brave-bin
```

## For rust development

```
cargo install cargo-edit
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

Note: the service will not run until you are connected to the internet, so give it a second. If you want to check if the mirrorlist has updated recently, check the timestamps in `/etc/pacman.d/mirrorlist`.

