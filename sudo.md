# Enable passwordless sudo

Edit `/etc/sudoers`. It is recommended to use `visudo`, e.g.
```
sudo EDITOR=nvim visudo /etc/sudoers
```
Find the line reading `@includedir /etc/sudoers.d` (likely at the bottom), and below it, add
```
me ALL(ALL) NOPASSWD:ALL
```
Where `me` is your username.
