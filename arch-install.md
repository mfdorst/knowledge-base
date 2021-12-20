# Notes for installing arch

## Connect to wifi

```
iwctl
```

Type `help` for help commands, but if you know your SSID just do

```
station list
```
to find the name of your wireless interface, and
```
station <wlan> connect <SSID>
```

## Setup Btrfs

```
mkfs.btrfs /dev/sdXX
```
Add `-f` if there is already a filesystem on the partition

Mount the partition
```
mount /dev/sdXX /mnt
```

Create btrfs subvolumes for root (/) and home
```
btrfs sub create /mnt/@
btrfs sub create /mnt/@home
```

Unmount the partition
```
umount /mnt
```

Mount the subvolumes
```
mount -o noatime,commit=120,compress=zstd,subvol=@ /dev/sdXX /mnt
mkdir -p /mnt{boot,home}
mount -o noatime,commit=120,compress=zstd,subvol=@home /dev/sdXX /mnt/home
mount /dev/sdXX /mnt/boot # sdXX should be the EFI partition here
```

`noatime`: No access time. Improves system performace by not writing time when thefile was accessed.

`commit`: Peridoic interval (in sec) in which data is synchronized to permanent storage.

`compress`: Choosing the algorithm for compress. `zstd` has good compression level and speed.

Run `lsblk` to check that everything is mounted correctly

## Run reflector before pacstrap to increase download speed

```
reflector --save /etc/pacman.d/mirrorlist --protocol https --country US --latest 5 --sort rate
```

## Pacstrap

```
pacstrap /mnt base linux linux-firmware btrfs-progs neovim
```

If you want LTS or Zen, do `linux-lts` or `linux-zen` in place of `linux`.

Install whatever editor you want as well. You can also include other packages here if you want.

## Generate an fstab from your current mount points

```
genfstab -U /mnt >> /mnt/etc/fstab
```

The `-U` option tells it to use UUID's to name the drives.

Then verify that it contains the mountpoints you want with the options you like.

## chroot into the system

```
arch-chroot /mnt
```

## Set your timezone

```
ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
```

## Sync the system clock

```
hwclock --systohc
```

## Set the locale

```
nvim /etc/locale.gen
```
and uncomment the line that says `en_US.UTF-8`.

then generate the locale with

```
locale-gen
```

And also do

```
echo LANG=en_US.UTF-8 >> etc/locale.conf
```

## Network configuration

Set the hostname to whatever you like:

```
echo ComputerName >> /etc/hostname
```

and set up `/etc/hosts` to look like

```
127.0.0.1   localhost
::1         localhost
127.0.1.1   ComputerName.mylocaldomain  ComputerName
```

## Set your password

```
passwd
```

## Install other packages

To speed this up, either rerun `reflector` or copy over the `mirrorlist` file from the live usb to the new drive

```
pacman -S grub grub-btrfs efibootmgr base-devel linux-headers networkmanager wpa_supplicant dialog os-prober reflector snapper git zsh exa bat
```

## Add btrfs to mkinitcpio

In `/etc/mkinitcpio.conf` find the `MODULES=()` line and add `btrfs` i.e.:
```
MODULES=(btrfs)
```

Now recreate the image:
```
mkinitcpio -p linux
```
If you installed a custom kernel, name the kernel you installed e.g. `linux-zen`.

## Install GRUB

```
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=Arch
grub-mkconfig -o /boot/grub/grub.cfg
```

## Create a user

```
useradd -mG wheel michael
passwd michael
```

Give your user sudo access:

```
EDITOR=nvim visudo
```

Uncomment the line that says
```
%wheel ALL=(ALL) ALL
```

## Setup ssh server (if desired)
```
pacman -S openssh
```

## Enable services

```
systemctl enable NetworkManager

# If you installed openssh:
systemctl enable sshd
```

## Boot into arch

```
exit
umount -l /mnt
reboot
```


