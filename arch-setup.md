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

