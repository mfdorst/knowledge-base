# WSL

## Install
Open `PowerShell` and type `wsl --install`

## Access WSL files from Explorer
Navigate to `\\wsl$`

## Potential issues

In Zsh, you may get a message like:
`manpath: can't set the locale; make sure $LC_* and $LANG are correct`

If so, run
```
sudo locale-gen "en_US.UTF-8"
sudo dpkg-reconfigure locales
```
Then run `exec zsh` to test that it worked.
