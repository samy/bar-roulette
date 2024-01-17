# Configuration of USB sound card

Use this command to list audio devices:
```
aplay -l
```
It gives you something like that:
```
card 0: vc4hdmi [vc4-hdmi], device 0: MAI PCM i2s-hifi-0 [MAI PCM i2s-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: Device [USB PnP Sound Device], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```
We want to use the second audio device (the USB), so you need to edit the ALSA configuration.

Edit the configuration file:
```
sudo touch /etc/asound.conf && sudo nano /etc/asound.conf
```
In our case the configuration must be:
```
defaults.pcm.card 1
defaults.pcm.device 0
```
Edit and save the file.

To test if it works, you can use the `aplay` command:
```
aplay test.mp3
```

You should have something like that (and sound on the headphones plugged on your USB sound card):
```
test.mp3:

 File Size: 5.32M     Bit Rate: 320k
  Encoding: MPEG audio    Info: 2018
  Channels: 2 @ 16-bit
Samplerate: 44100Hz
Replaygain: off
  Duration: 00:02:13.00

In:11.6% 00:00:15.42 [00:01:57.58] Out:740k  [  ====|===-  ]        Clip:0
```
