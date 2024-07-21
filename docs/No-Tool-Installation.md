The [[Installation]] page provides general information that's independent of SoC and vendor on how to install Thingino.

Certain cameras allow the installation by leveraging the vendor's firmware update process without requiring tools to open the device.
Be aware that this process may be changed by the vendor, so there's no guarantee that this method will continue to work.  
Nevertheless, we share instructions for certain devices.

## Cinnado D1 based on T23N SoC

- last tested: 2024/7/21

The [Cinnado D1](https://www.cinnado.com/D1) devices' bootloader will look for a file `v4_boot.bin` which if present, will be used to replace the device's bootloader.
Therefore, Thingino's bootloader can be installed first, and then Thingino via Thingino's [[auto update process|Installation#from-an-sd-card]].  The steps would be as follows:

First, download the full image
```
wget https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-cinnado_d1_t23n.bin
```
Now, extract the first 256KB:
```
dd if=thingino-cinnado_d1_t23n.bin bs=1k count=256 of=v4_boot.bin
```
Now, assuming that your SD card has been mounted at say `/media/yoursdcard`, copy `thingino-cinnado_d1_t23n.bin` as `autoupdate-full.bin` along with the `v4_boot.bin` file onto it:
```
cp thingino-cinnado_d1_t23n.bin /media/yoursdcard/autoupdate-full.bin
cp v4_boot.bin /media/yoursdcard/
```
Eject the card, put it in the camera, turn it on and wait two minutes, then follow the [[Wifi Portal Setup Process|Configuring-Wi‐Fi-Access#captive-portal]].


