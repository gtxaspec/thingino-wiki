The [[Installation]] page provides general information that's independent of SoC and vendor on how to install Thingino.

Certain cameras allow the installation by leveraging the vendor's firmware update process without requiring tools to open the device.
Be aware that this process may be changed by the vendor, so there's no guarantee that this method will continue to work.  
Nevertheless, we share instructions for certain devices.

## Cinnado D1 based on T23N SoC

- last tested: 2024/7/21

### Verifying the SoC Model of Cinnado D1

To verify which of the known SoCs was used in the Cinnado D1 the case needs to be opened. The case is divided into two parts and the upper case is clipped into the bottom. You don't need to unscrew your camera. Carefully remove the upper case perhaps with a small tool. After that you can adjust the camera to see the board and which chipset has been used.

The procedure below works only if the D1 uses the T23N SoC.

<img src="https://github.com/user-attachments/assets/80766e30-c062-45f7-96e8-506066560639" alt="Cinnado D1" width="500">


### Update Process

The [Cinnado D1](https://www.cinnado.com/D1) stock bootloader will look for a file `v4_boot.bin` which if present, will be used to replace the device's bootloader.
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

## Information about other cameras that support a No Tool Install

> [!WARNING]  
> The following installers **DO NOT** create a **full backup** and require technical know-how to revert back to the stock firmware.

Josh from [WLTechBlog](https://www.youtube.com/@wltechblog) published a number of videos describing the process for multiple cameras:

- [Wyze Cam V2](https://www.youtube.com/watch?v=1pSx_jaXfoE)
- [Wyze Cam V3](https://www.youtube.com/watch?v=SX637mrp0R0)
- [Wansview W7](https://www.youtube.com/watch?v=jCRiIljSWlw)
- [WUUK Y0510](https://www.youtube.com/watch?v=PhXbeY-PBgg)
- [Cinnado D1](https://www.youtube.com/watch?v=40MUbIXVBNI)