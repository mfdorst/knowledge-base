# Installing Neovim

## Using my script
The script essentially just follows the steps outlined here.
```
install-nvim-ubuntu
```

## Build from source

_See [building neovim] for complete instructions._

### Why build from source?

Neovim is currently very unstable (it is pre-1.0), and each new release brings breaking changes. If
you install it with your package manager, it will be updated with each new release, and your
plugins may break.

### Clone the repo
```
git clone git@github.com:neovim/neovim
```

### Install dependencies

#### Ubuntu
```
sudo nala install ninja-build gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip curl doxygen
```
#### Arch
```
sudo pacman -S base-devel cmake unzip ninja tree-sitter curl
```

### Check out the desired version

For the latest stable version:
```
git checkout stable
```
Or checkout a version that is known to work with your config.
```
git checkout v0.8.2
```

### Build and install
From the `neovim` directory, run
```
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```

### Install packer
```
install-packer
```

### Initialize packer
```
packer-sync
```

[building neovim]: https://github.com/neovim/neovim/wiki/Building-Neovim
