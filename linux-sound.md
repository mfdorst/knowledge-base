# Sound related issues on Linux

## Fix popping sounds when opening content with audio

See <https://askubuntu.com/a/1230834>.

It may be caused by your sound card's power save feature.

1. Check if the power save feature is enabled:
```bash
cat /sys/module/snd_hda_intel/parameters/power_save
```

2. If it returns `1`, try the following temporary fix:
```bash
echo "0" | sudo tee /sys/module/snd_hda_intel/parameters/power_save
```

3. If the previous step worked, make it permanent by creating a file at `/etc/modprobe.d/audio_disable_powersave.conf` with the following contents:
```
options snd_hda_intel power_save=0
```
