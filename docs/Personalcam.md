# Personal WiFi camera

![image](https://github.com/user-attachments/assets/95762325-e08e-4b1a-9bf1-2ef2dbd214b1)

Sold by Personal (Argentine telecom company), to be used strictly with their paid cloud service and mobile app. The camera itself is a clone of the Wyze Pan Cam v3 and the Atom cam v3, but with several differences, most notably on the GPIO mappings.

## Features
* Ingenic T31X running at 1.4GHz
* 128MB of RAM
* 16 MB of NOR SPI (ZB25VQ128ASIG)
* gc2053 camera
* AltoBeam ATBM6031

## Support status
This camera is fully supported by Thingino. Only missing support is Audio and AI. Grab the latest release from [thingino-personalcam.bin](https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-personalcam.bin), or use `sysupgrade -p` for an in-place upgrade if you're already running Thingino.

## Installation from stock firmware using the Test.tar mechanism
Stock firmware has the backdoor that allows to run any code from a SD card using the Test.tar mechanism. To do so, it's possible to create your own Test.tar and upgrade firmware by just following the instrctions on the [t31-test-tar-upgrader](https://github.com/cocus/t31-test-tar-upgrader) repo.
In short, clone that repository, and run `make`. Grab the resulting zip file and uncompress its contents to a previously-formatted SD card with FAT32.

Then, with the camera powered off, stick the SD card on it, and turn the camera on. Wait for a short while, until it reboots (you might see the camera rebooting when it starts moving). If it doesn't reboot in 10 minutes, reboot it manually (we have observed that some cameras enter a ROM mode rather than rebooting, so waiting for 10 minutes is a safe guess).

When it finishes, it will start broadcasting a new WiFi, similar to "thingino-XXXXX". Connect to it and set up the WiFi you want the camera connect. Save the configuration and wait for it to show on your network!

## Installation from stock firmware using cloner
In order to use this tool, you'll need to open the camera. This usually breaks the seals, so it's possible the camera won't be "exterior proof" anymore.
The SPI flash chip is located on the underside of the main board, and you'll need to bridge its 5th and 6th pins while powering the camera up, as shown here:
![image](https://github.com/user-attachments/assets/0275cdca-0a5e-4726-9502-d6324364a0d7)

Please note that _neither of the provided USB cables have data pins_, so **you can't use them for this**; so grab a previously verified micro USB cable that fits. Then follow the instructions on the [generic tutorial](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner).

## Installation from other firmware
Follow the generic guide [here](https://github.com/cocus/t31-test-tar-upgrader). The u-boot file to use is "u-boot-t31x.bin".