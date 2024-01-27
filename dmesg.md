# Dmesg

## Show logs of previous boot
```
journalctl -o short -k -b -1
```
`-2` would be the boot before, and so on.
