# Wyze v2 / Neos SmartCam /ATOM Cam 1

<img src="https://github.com/user-attachments/assets/aef89340-0abe-48df-80a7-9c5b00b8e0d9" width="150">

These cameras are very popular and have been hackable for quite some time via a numerous other (mostly defunct?) projects. There are much better contemporary cameras that offer greater value for the cost, so don't go out and buy these, but if you already own them they are relatively easy to get up on Thingino firmware.

## Features
* Ingenic T20X
* 16 MB of NOR SPI (ZB25VQ128ASIG)


## Support status
This camera is fully supported by Thingino. Grab the latest release from [releases](https://github.com/themactep/thingino-firmware/releases/latest), or use `sysupgrade -p` for an in-place upgrade if you're already running Thingino.

## Which Firmware Version Do I Need?
There are 2 image sensors used in these cameras ([JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) and [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf23.bin)).  Identifying which version you have is difficult, but it's very easy to switch to the "right" version for your particular camera.  Installing the "wrong" version is just fine, and won't brick your device.  You can access the device and interact with it, the only problem is that you won't see an actual image from the camera.  If this is the case, just switch to the other version

1. Install one of the versions - just pick one.  If you're not sure, or can't flip a coin to choose, just grab the [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) version.
2. Follow the standard Thingino install instructions.
3. Log into the camera via web interface.
4. If you don't see an image from your camera, you need to switch to the other version.
5. Connect via SSH
6. Edit `/etc/os-release` to point to the new version
7. Run the upgrade process with the `sysupgrade -p` command, which will auto-switch you to the other firmware version.  After that process finishes, check again and images should show correctly.

## Installation from stock firmware using "No Tools" method
This method leverages the vendor's firmware update process without requiring tools to open the device. Be aware that this process may be changed by the vendor, so there's no guarantee that this method will continue to work.
* Written instructions [here](https://github.com/wltechblog/thingino-installers/tree/main/wyze-cam-2)
* Video of process [here](https://www.youtube.com/watch?v=ifXObp2jhO0&start=0)

## Installation from stock firmware using cloner (Optional, not normally required method)
In order to use this tool, you'll need to open the camera. This usually breaks the seals, so it's possible the camera won't be "exterior proof" anymore.

If you want a video tutorial to watch before you start, you can [watch this](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner).

To install Thingino firmware with this method, it's recommended you flash following the detailed instructions on the [generic tutorial](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner) 

Things to note about the process specific to this camera:
1. You will need a USB-A to USB-A cable to use cloner to flash this camera.  The regular micro-usb cable that powers your camera will not work.  You can either [make your own](https://www.instructables.com/Male-to-Male-A-to-A-USB-Cable/) or buy them online for cheap. 

2. The SPI flash chip is located on the underside of the main board, and you'll need to bridge its 5th and 6th pins while powering the camera up, as shown here (note where the mark is for pin 1 for proper orientation):

[<img src="https://github.com/user-attachments/assets/1729af3b-43a1-4152-9cb5-1d9a4ea02d0d" width="200">](https://github.com/user-attachments/assets/1729af3b-43a1-4152-9cb5-1d9a4ea02d0d) <img src="https://camo.githubusercontent.com/851273986d66f0f08eedf08a68ab25da4d4acacd14912a5995d5a90dd0bae7b5/68747470733a2f2f7468696e67696e6f2e636f6d2f612f666c6173682d636869702d73686f72742e706e67" width="200">
