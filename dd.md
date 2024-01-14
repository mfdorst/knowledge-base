# Write an ISO to a USB stick with `dd`

```
sudo dd if=path/to/iso of=/dev/<device> bs=1M status=progress conv=fsync
```
Note: `<device>` must be the device, not the partition, so `/dev/sdc`, not `/dev/sdc2`.

`conv=fsync` should force the progress report to show the actual buffered writes. Without this, the
progress report will show it completed, and then you'll wait for several seconds while the buffered
writes finish.

If for some reason your progress is not showing, you can check the size of the write buffer with:
```
cat /proc/meminfo | grep Dirty
```
You can run this several times and you should see the number slowly drop. Once it reaches about
100kB, your write should be finished.
