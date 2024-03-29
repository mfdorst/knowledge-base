# Get up and running quickly on Ubuntu

It is best to follow these steps in order, so that all dependencies will be installed before their
dependents.

## Install nala
```
sudo apt install nala
```

## Install packages
```
sudo nala install clang curl bat btop fish fd-find gh git gnome-tweaks man ripgrep kitty stow tldr unzip zoxide
```

## Install fish PPA
The version of `fish` in the Ubuntu repos may be very out of date, and configs for newer versions
of fish may not work. Installing the fish PPA will allow us to upgrade to the latest 3.x release.
```
sudo add-apt-repository ppa:fish-shell/release-3
sudo nala update
sudo nala upgrade
```

## Change shell to fish
```
exec fish
chsh -s $(which fish)
```

## Set hostname
```
sudo hostname <hostname>
```
You may also want to edit `/etc/hostname`

## Setup GitHub
See [git.md](./git.md)

## Install scripts
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
or look through `.cfg` and stow the items that you need. For instance, on a server one might want:
```
cd .cfg
stow bash git nvim tmux vim zsh
```

## Run install scripts
```
install-omz
install-starship
install-rustup
```

## Add user
```
adduser <username>
usermod -aG sudo <username>
```

## Fix naming of `bat` command
### Note: as of Ubuntu 23.04 this is no longer needed.

Ubuntu renames `bat` to `batcat` to avoid conflicts with another packages.
We could rename it, but this would be overwritten whenever `bat` gets updated.
Instead, we can symlink it to someplace in our `PATH` with the name `bat`.
```
mkdir -p ~/.local/bin
ln -s /usr/bin/batcat $HOME/.local/bin/bat
```

## Install exa
### Note: As of Ubuntu 23.04 this is no longer needed.
Ubuntu's `exa` package does not include support for the `--git` flag, so we compile it ourselves.
```
cargo install exa
```

## Set default terminal to kitty
```
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator $(which kitty) 50
```

`Ctl+Alt+T` should now open kitty.

# Past configurations
Tools I no longer use.

## Install Doom Emacs
```
git clone --depth 1 https://github.com/hlissner/doom-emacs ~/.emacs.d
~/.emacs.d/bin/doom install
```

## Install alacritty

### Dependencies
```
sudo apt install cmake pkg-config libfreetype6-dev libfontconfig1-dev libxcb-xfixes0-dev python3
```

### Install
```
cargo install alacritty
```

## Set default terminal to alacritty
```
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator $(which alacritty) 50
```

`Ctl+Alt+T` should now open alacritty.

# Install pyenv
```
curl https://pyenv.run | bash
```

# Pyenv

## List avaliable python versions
```
pyenv install -l | less
```

## Install prerequisites for installing python versions
```
sudo apt install build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```

## Install a python version
```
pyenv install 3.9.2   # or other desired version
```

## Set a global python version
```
pyenv global 3.9.2
```

# Install marked (for markdown preview in emacs)
```
npm i -g marked
```
