# Mounting drives in Linux

Use `df`, `lsblk` or `sudo fdisk -l` to list the available drives on your system.

Tip: use `dmesg` to see what drive was most recently plugged or unplugged,
or, run `ls /dev/sd*` before and after plugging in a drive.

Make a directory under `/mnt`. This will be your mount point. For instance:
```
mkdir /mnt/sandisk
```

Mount the drive with `sudo mount /dev/<drive-name> /mnt/<mount-point>`. For instance:
```
sudo mount /dev/sdc2 /mnt/sandisk
```

Unmount with `sudo umount /mnt/<mount-point>`.
