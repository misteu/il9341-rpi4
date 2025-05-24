# il9341-rpi4

Display: TJCTM24024-SPI (uses il9341 Chipset)

Raspberry: Raspberry Pi 4 Model B

## Connect Display

Connect everything as mentioned here: https://bytesnbits.co.uk/retropie-raspberry-pi-0-spi-lcd/

## Download / install drivers

Download .zip archive as mentioned here: https://forums.raspberrypi.com/viewtopic.php?t=358240#p2151405

(or just clone this repo)

and copy the files into your `/boot` folder

```
git clone https://github.com/misteu/il9341-rpi4.git
cd il9341-rpi4/
sudo cp *.dtbo /boot/overlays/
sudo cp *.dts /boot/overlays/
sudo cp wavesku18366.bin /lib/firmware/
```

modify your `/boot/config.txt` as following and make sure `dtparam=spi=on` is enabled (i.e. uncommented) as well.

```
# 320x240pixels Waveshare SKU18366 2.8in display
dtoverlay=mipi-dbi-spi,speed=48000000
dtparam=compatible=wavesku18366\0panel-mipi-dbi-spi
dtparam=write-only,cpha,cpol
dtparam=width=320,height=240,width-mm=57,height-mm=43
dtparam=reset-gpio=25,dc-gpio=24
```

Make sure the `dtparam=reset-gpio=24,dc-gpio=25` is according to your connection. When following the link above, it is `reset-gpio=25,dc-gpio=24` in case you followed the wiring on the raspberry forum it's flipped.

# Reboot your Pi
`sudo reboot`