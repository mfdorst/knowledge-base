# Full-drive encryption with LUKS

Examples of substitutions for the following commands:
`<device>`: `/dev/sda2`
`<name>`: `root`

All of the following commands must be run as root or with `sudo`.

## Format a disk
```
cryptsetup luksFormat <device>
```

## Unlock and mount a disk for reading/writing
```
crypstetup open <device> <name>
mount /dev/mapper/<name> /mnt
```
`<name>` may be any name

## Unmap a disk
Removes the mapping and wipes the key from kernel memory.
```
umount /mnt
cryptsetup close <name>
```
