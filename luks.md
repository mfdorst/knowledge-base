# Full-drive encryption with LUKS

All of the following commands must be run as root or with `sudo`.

## Encrypt a disk using a password
```
cryptsetup luksFormat <device>
```

Where `<device>` might be `/dev/sdb1`

## Encrypt a disk using a keyfile
```
cryptsetup luksFormat <device> /path/to/keyfile
```

## Unlock and mount a disk for reading/writing
```
crypstetup open <device> <name>
mount /dev/mapper/<name> /mnt
```
`<name>` may be any name, e.g. `root` or `data`

### Unlock with keyfile
```
cat <keyfile> | cryptsetup open <device> <name>
```

## Unmap a disk
Removes the mapping and wipes the key from kernel memory.
```
umount /mnt
cryptsetup close <name>
```
