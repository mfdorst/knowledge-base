# Installing linux on T2 Mac

Installing Linux on a mac with a T2 chip requires special firmware.

Go to wiki.t2linux.org for links to the modified ISO's, as well as special instructions for
installation.

## Installing NixOS
Get ISO's from <github.com/t2linux/nixos-t2-iso>. Do not use the `v6.4.9` or `v6.4.2` ISO's. They
are broken. The `v6.4.2` iso works.


First, follow the [pre-installation guide][1], which will show you how to copy the proprietary
Broadcom firmware from MacOS to the EFI partition, so that it is accessible to Linux.

General instructions for reading the firmware in Linux are [here][2], and specific instructions for
doing this in NixOS are [here][3]. It is not at all clear what order these instructions should be
followed in, but here is what has worked for me.

My drive setup is as follows:
```
nvme0n1p1: EFI (contains the broadcom firmware)
nvme0n1p2: APFS (MacOS)
nvme0n1p3: EFI (/boot for NixOS)
nvme0n1p4: Ext4 (/ for NixOS)
```
You may need to adapt these instructions if your disk layout is different.

Note: If you are re-using an existing config, make sure to run `nixos-generate-config --root /mnt`,
and copy the the new drive UUID's into your existing `hardware-configuration.nix`.

```
sudo mount /dev/nvme0n1p4 /mnt
sudo mkdir /mnt/boot
sudo mount /dev/nvme0n1p3 /mnt/boot
sudo mkdir -p /tmp/apple-wifi-efi
sudo mount /dev/nvme0n1p1 /tmp/apple-wifi-efi
sudo mkdir -p /lib/firmware/brcm
bash /tmp/apple-wifi-efi/firmware.sh
# Make sure to type `y` at the end, if you don't want to erase the firmware from the EFI partition.
sudo systemctl start wpa_supplicant
wpa_cli
```
`wpa_cli` will put you into a shell. These are the commands I run to connect to wifi.
If you already know your network's SSID, you may prefer to skip the first two commands.
```
scan
scan_results
add_network
set_network 0 ssid "<SSID>"
set_network 0 psk "<password>"
enable_network 0
reconnect
status
quit
```

If you don't have an existing config, follow on from instruction 3 of the
[T2 nixos installation guide][3].

[1]: https://wiki.t2linux.org/guides/preinstall
[2]: https://wiki.t2linux.org/guides/wifi-bluetooth/#on-macos 
[3]: https://wiki.t2linux.org/distributions/nixos/installation
