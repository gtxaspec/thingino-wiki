# Wyze v2 / ATOM Cam 1 / Neos SmartCam

{Image to come...}

These cameras are very popular and have been hackable for quite some time via a numerous other (mostly defunct?) projects. There are much better contemporary cameras that offer greater value for the cost, so don't buy these, but if you have them they are relatively easy to get up on Thingino.

## Features
* Ingenic T20X
* 16 MB of NOR SPI (ZB25VQ128ASIG)


## Support status
This camera is fully supported by Thingino. Grab the latest release from [thingino-personalcam.bin](https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-personalcam.bin), or use `sysupgrade -p` for an in-place upgrade if you're already running Thingino.

## Which version do I need?
There are 2 image sensors used in these cameras ([JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) and [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf23.bin)).  Identifying which version you have is difficult, but it's very easy to switch to the "right" version for your particular camera.  Installing the "wrong" version is just fine, and won't brick your device.  You can access the device and interact with it, the only problem is that you won't see an actual image from the camera.  If this is the case, just switch to the other version

1. Install one of the versions - just pick one.  If you're not sure, or can't flip a coin to choose, just grab the [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) version.
2. Follow the standard Thingino install instructions.
3. Log into the camera via web interface.
4. If you don't see an image from your camera, you need to switch to the other version.
5. Connect via SSH
6. Edit `/etc/os-release` to point to the new version
7. Run the upgrade process with the `sysupgrade -p` command, which will auto-switch you to the other firmware version.  After that process finishes, check again and images should show correctly.

## Installation from stock firmware using cloner
In order to use this tool, you'll need to open the camera. This usually breaks the seals, so it's possible the camera won't be "exterior proof" anymore.
The SPI flash chip is located on the underside of the main board, and you'll need to bridge its 5th and 6th pins while powering the camera up, as shown here: {Image to come...}

Please note that you will need a USB-A to USB-A cable to use cloner to flash this camera.   Then follow the instructions on the [generic tutorial](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner).

## Installation from other firmware
TBD...