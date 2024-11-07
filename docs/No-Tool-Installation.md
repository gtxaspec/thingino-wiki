The [[Installation]] page provides general information that's independent of SoC and vendor on how to install Thingino.

Certain cameras allow the installation by leveraging the vendor's firmware update process without requiring tools to open the device.
Be aware that this process may be changed by the vendor, so there's no guarantee that this method will continue to work.  
Nevertheless, we share instructions for certain devices.

## Cinnado D1 based on T23N or T31L SoC

- Last update: 3 November 2024

You can also follow along with this Youtube video! https://www.youtube.com/watch?v=40MUbIXVBNI


### Verifying the SoC Model of Cinnado D1

To verify which of the known SoCs was used in the Cinnado D1 the case needs to be opened. The case is divided into two parts and the upper case is clipped into the bottom. You don't need to unscrew your camera. Carefully remove the upper case perhaps with a small tool. After that you can adjust the camera to see the board and which chipset has been used. You can follow this Youtube video to see how to open the cam. https://www.youtube.com/watch?v=94NXZh3LTSo

<img src="https://github.com/user-attachments/assets/80766e30-c062-45f7-96e8-506066560639" alt="Cinnado D1" width="500">


### Update Process

The [Cinnado D1](https://www.cinnado.com/D1) stock bootloader will look for a file `v4_all.bin` which if present, will be used to replace the device's firmware.

The steps would be as follows:

First, download the appropriate firmware image for the processor model you identified.

For T23: https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-cinnado_d1_t23n.bin

For T31: https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-cinnado_d1_t31l.bin

Now, rename the firmware file to v4_all.bin and place it on the SD card.

Eject the card, put it in the camera, turn it on and wait two minutes, then follow the [[Wifi Portal Setup Process|Configuring-Wi‐Fi-Access#captive-portal]].

## Wansview W6 / T21
- Coming soon

## Information about other cameras that support a No Tool Install

> [!WARNING]  
> The following installers **DO NOT** create a **full backup** and require technical know-how to revert back to the stock firmware.

Josh from [WLTechBlog](https://www.youtube.com/@wltechblog) published a number of videos describing the process for multiple cameras:

- [Wyze Cam V2](https://www.youtube.com/watch?v=1pSx_jaXfoE) Docs: https://github.com/wltechblog/thingino-installers/tree/main/wyze-cam-2
- [Wyze Cam V3](https://www.youtube.com/watch?v=SX637mrp0R0) Docs: https://github.com/wltechblog/thingino-installers/tree/main/wyze-cam-3
- [Wansview W7](https://www.youtube.com/watch?v=jCRiIljSWlw) Docs: https://github.com/wltechblog/thingino-installers/tree/main/wansview-w7
- [WUUK Y0510](https://www.youtube.com/watch?v=PhXbeY-PBgg) Docs: https://gist.github.com/wltechblog/bcc30aca647ee8eac5cb80c6b7368b98
- [Cinnado D1](https://www.youtube.com/watch?v=40MUbIXVBNI)