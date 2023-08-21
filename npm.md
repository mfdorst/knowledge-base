# NPM

## Global package permissions issue
When installing NPM from a package manager e.g. `apt` or `pacman`, there will be a permissions
issue when installing packages globally with the `-g` flag, because the default location for
storing global packages is owned by `root`.

There are two ways to fix the permission issue.

1. **Reinstall NPM with NVM.**
```
install-nvm
```
Note: this will not work with some shells. `bash` and `zsh` are supported.
If using `fish`, run `install-nvm-fish`.

```
nvm install --lts   # Installs the latest LTS version
nvm use --lts
```

2. **Relocate global NPM package store.**

Create a directory wherever you would like it to go.
```
mkdir -p ~/.local/share/npm
```
Tell NPM to use that directory to store global packages.
```
npm config set prefix ~/.local/share/npm
```
Make sure to add the `~/.local/share/npm/bin` directory to your `PATH`.
`.zshrc`
```
export PATH="~/.local/share/npm/bin:$PATH"
```
