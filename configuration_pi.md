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

To test if it works, you can install and use the `mpg123` command:
```
sudo apt install mpg123
mpg123 test.mp3  
```

You should have something like that (and sound on the headphones plugged on your USB sound card):
```
High Performance MPEG 1.0/2.0/2.5 Audio Player for Layers 1, 2 and 3
        version 1.26.4; written and copyright by Michael Hipp and others
        free software (LGPL) without any warranty but with best wishes


Terminal control enabled, press 'h' for listing of keys and functions.

Playing MPEG stream 1 of 1: sample-15s.mp3 ...

MPEG 1.0 L III vbr 44100 j-s
```
