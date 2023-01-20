# WSL

## Install
Open `PowerShell` and type `wsl --install`

## Access WSL files from Explorer
Navigate to `\\wsl$`

## Windows Terminal
Download `Windows Terminal` from the Microsoft Store.

### Disable `alt+space` menu
1. Press `Ctl+,` to open Settings.
2. In the bottom left, click `Open JSON file`.
3. In the `actions` section, add the following object:
```
{
    "command": "unbound",
    "keys": "alt+space"
}
```

## Potential issues

In Zsh, you may get a message like:
`manpath: can't set the locale; make sure $LC_* and $LANG are correct`

If so, run
```
sudo locale-gen "en_US.UTF-8"
sudo dpkg-reconfigure locales
```
Then run `exec zsh` to test that it worked.
