# Write an ISO to a USB stick with `dd`

```
sudo dd if=path/to/iso of=/dev/<device> bs=1M status=progress
```
Note: `<device>` must be the device, not the partition, so `/dev/sdc`, not `/dev/sdc2`.
