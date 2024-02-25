# General Linux knowledge

## Check ram info
For information about how much ram is available:
```
cat /proc/meminfo
```
For detailed hardware information about your ram:
```
nix shell nixpkgs#dmidecode -c sudo dmidecode --type 17
```

## Check what filesystems are supported
```
cat /proc/filesystems
```
