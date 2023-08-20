# NPM

# Fix permission issue

1. Reinstall NPM with NVM.
2. Relocate global NPM package store.

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
