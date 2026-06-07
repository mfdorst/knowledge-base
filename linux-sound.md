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

## Fix sound output periodically changing to headphone jack

This was causing a small pop and the volume on screen display to pop up at random every 30 seconds to a mintute.

***Downsides:** This will disable sound automatically switching to your headphones when you plug them in. You will need to manually switch audio outputs.*

1. Install `alsa-tools`.

2. Run
```bash
sudo hdajackretask
```

3. At the top, select the onboard sound card, usually `Realtek`.

4. On the right panel under `Options`, check the box for `Parser hints`.

5. Click on `jack_detect` until the value is set to `no`.

6. Click `Install boot override` and reboot.
