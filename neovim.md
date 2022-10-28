# Installing Neovim

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

The latest stable release as of this writing (9/22) is v0.7.2, and that is working well.
```
git checkout v0.7.2
```

### Build and install
From the `neovim` directory, run
```
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```

[building neovim]: https://github.com/neovim/neovim/wiki/Building-Neovim
