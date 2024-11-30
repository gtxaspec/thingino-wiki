The Ingenic USB Cloner application is a PC side utility that interfaces with the "USB-Boot" mode built into Ingenic SOCs.
By placing the SOC into "USB-Boot" mode, you are able to use the Ingenic USB Cloner to directly flash the firmware chip
without physically removing, or interfacing to the flash chip.  This method simplifies firmware backup and installation on capable devices.

This guide provides step-by-step instructions for completing a full backup and writing a firmware binary to your device. It is designed to walk you through the process, helping you become familiar with the Ingenic Cloner tool. However, please note that this guide is not intended to be an all-inclusive reference and does not cover all features of Cloner. It focuses on the basic steps needed to perform the outlined tasks, offering a foundation for using the utility effectively.

## Downloading Cloner  
> [!TIP]
> For better success and compatibility, we strongly recommend using the Linux version of Ingenic USB Cloner.

Download the Cloner application for your operating system using the links below. Extract the program to a working directory on your computer.

- [Ingenic Cloner for Linux](https://github.com/gtxaspec/ingenic-cloner-profiles/releases/download/latest/cloner-2.5.43-ubuntu_thingino.tar.xz)
- [Ingenic Cloner for Windows](https://github.com/gtxaspec/ingenic-cloner-profiles/releases/download/latest/cloner-2.5.43-windows_thingino.7z)

Navigate to the `cloner-2.5.xx-yyyyy_thingino` directory, with "xx" indicating your downloaded version of Cloner and "yy" is your OS.

> [!IMPORTANT]  
> Windows users may need to install additional drivers for support.  See the [[Vendor Documentation|Ingenic-USB-Cloner#vendor-documentation]] PDF Guide for additional details.

Open the Cloner application.

<a href="https://github.com/user-attachments/assets/4b187183-f176-405c-81b8-ae7f616f3075">
  <img src="https://github.com/user-attachments/assets/4b187183-f176-405c-81b8-ae7f616f3075" width="720" alt="Cloner Main Window">
</a>

> [!IMPORTANT]  
> The options described in the screenshots will not match if you did not load the `cloner` bundle as outlined in the previous steps.

## Enable configuration mode  

If the **Lock Level** is not 0, change the **Lock Level** from **2**, to **0**

<a href="https://github.com/user-attachments/assets/3e67b890-d8ab-46a4-b60d-48f26ae1e645">
  <img src="https://github.com/user-attachments/assets/3e67b890-d8ab-46a4-b60d-48f26ae1e645" width="720" alt="Cloner Main Window Lock Menu">
</a>

Enter **_!@#_** (_exclamation mark_, _"at" symbol_, _number sign_) as the password.  Click OK.

![](https://thingino.com/a/cloner-0-4.png)

## Cloner configuration

After entering the password in the previous step, the **Config** button should now appear in the main screen. Click the **Config** button in the top-right corner.

<a href="https://github.com/user-attachments/assets/b7316719-9cfe-4d43-9eb8-f17a12630a3a">
  <img src="https://github.com/user-attachments/assets/b7316719-9cfe-4d43-9eb8-f17a12630a3a" width="720" alt="Cloner Main Window Lock Menu">
</a>

In the **Config** window, under the **INFO** tab, you have various configuration menus available:

In the **Platform** dropdown menu, select **_T_**. Choose the appropriate SOC version for your device next to **_Platform T_**.

> [!IMPORTANT]  
> Selecting the correct SOC for your device is crucial. If you choose incorrectly, the cloner program won't recognize your device, halting the process. Be sure to accurately identify and select the appropriate version (e.g., t20, t21, t23, t30, t31) for your specific hardware. This step is essential for the cloner to function properly and allow you to proceed with the operation.

<a href="https://github.com/user-attachments/assets/156a1275-5642-44c3-b010-f50e5d40abce">
  <img src="https://github.com/user-attachments/assets/156a1275-5642-44c3-b010-f50e5d40abce" width="720" alt="Cloner SOC Selection Menu">
</a>

Next, you can proceed with either performing a [[backup|Ingenic-USB-Cloner#backup]] or [[writing firmware|Ingenic-USB-Cloner#writing-firmware]].

## Cloner Function Setup

### Backup

> [!WARNING]  
> We **strongly recommend** using Cloner to create a **full backup** of the existing stock firmware. This is an essential step if you ever need to restore the original functionality or analyze the stock firmware for compatibility.

In the **Board** dropdown menu, choose the appropriate _**reader**_ operation based on your device's SoC submodel (t31a, t31nl, t31x for example) and flash chip size. The available options are 8MB, 16MB, and 32MB.

For the example below, we will select: _sfc_nor_reader_16M.cfg_ for the specific SoC.
<a href="https://github.com/user-attachments/assets/e8c5c62f-560c-4a2b-8efd-43aa8e7fc975">
  <img src="https://github.com/user-attachments/assets/e8c5c62f-560c-4a2b-8efd-43aa8e7fc975" width="720" alt="Cloner Board Selecttion Menu">
</a>

Click the **Save** button to save your choice and return to the main menu.

<a href="https://github.com/user-attachments/assets/4691e59d-c97a-483d-9737-96412a4b67c7">
  <img src="https://github.com/user-attachments/assets/4691e59d-c97a-483d-9737-96412a4b67c7" width="720" alt="Cloner Main Menu">
</a>

You may now begin [[the backup operation.|ingenic-usb-cloner#starting-cloner-operations]]

### Writing Firmware

In the **Board** dropdown menu, select the appropriate _**writer**_ operation based on your device's SoC submodel (t31a, t31nl, t31x for example) and specific needs. The available options are:

- **_sfc_nor_writer.cfg**: for writing individual partitions  
- **_sfc_nor_writer_full.cfg**: for writing full firmware images

<a href="https://github.com/user-attachments/assets/d97a57f8-41e4-4423-b5ab-e43a635df577">
  <img src="https://github.com/user-attachments/assets/d97a57f8-41e4-4423-b5ab-e43a635df577" width="720" alt="Cloner Board Selection Menu">
</a>

Find and click on the **POLICY** tab, then click **...** (_three dot_) button in the setting column to open the file selection dialog.

<a href="https://github.com/user-attachments/assets/7ba05397-ae87-4dbe-9f48-ec86029eec22">
  <img src="https://github.com/user-attachments/assets/7ba05397-ae87-4dbe-9f48-ec86029eec22" width="720" alt="Cloner Policy Firmware File Select Button">
</a>

Select the firmware image file you want to write, and click Open.  

![image](https://camo.githubusercontent.com/6693f348a02a45c5ec826867e415febfb0542fd7ca6698c6635f73511c6d1a5f/68747470733a2f2f7468696e67696e6f2e636f6d2f612f636c6f6e65722d302d392e706e67)  
Once you have selected your firmware image file for writiing, click the **Save** button to return to the main screen.

<a href="https://github.com/user-attachments/assets/73ad4ded-7ab4-42ca-bcfb-e7965d7c42db">
  <img src="https://github.com/user-attachments/assets/73ad4ded-7ab4-42ca-bcfb-e7965d7c42db" width="720" alt="Cloner Policy Firmware File Select Button">
</a>  

### Starting Cloner Operations

Click **Start** button on the main screen.

![image](https://github.com/user-attachments/assets/af05e268-060d-4ccc-aea1-d9a047302e2f)

At this stage, ensure your device is unplugged from your computer.

Connect the USB cable to the device, but leave the other end disconnected.

> [!IMPORTANT]  
> If you are flashing a blank flash memory chip, or the bootloader is not installed, the Ingenic SoC will default to "USB-Boot" mode. Shorting pins on the flash chip is **not** required in this case.

Locate the flash memory chip on the camera circuit board. Typically this is a square chip with 8 pins labeled _25Q64_ or _25Q128_, rarely _25L64_ or _25L128_. If you have trouble locating the chip, try taking some pictures of your board from both sides.  You can then try and reach out to our [[community|Resources-and-Links#information]] for further assistance.

Pins 5 and 6 of the SOIC8 chip are on the opposite corner of pin 1, indicated by the embossed or drawn dot next to it.

![](https://thingino.com/a/flash-chip-dot.png)

Once you are ready to begin, short-circuit pins 5 and 6 of the flash chip with a small metal object, a screwdriver or tweezers.

Short pins 5 and 6 ON THE FLASH CHIP, not SoC or any other chip, use the photos as a reference, as described in this document.

> [!CAUTION]
> __Do not try to short-circuit any random chip! It will most likely burn your camera circuit.__

![](https://thingino.com/a/flash-chip-short.png)

While maintaining the short, connect the USB cable to the computer. Wait 5 seconds, then release the short.

It may take up to 30 seconds for Cloner to recognize the device. On Windows, you can check if the device is detected via Device Manager, and on Linux, you can use dmesg to verify detection of the Ingenic Cloner device.

![](https://thingino.com/a/windows-device-manager-libusb.png)

Once the device is recognized, the progress bars will change from purple to green. When all bars are green, the operations are complete.

> [!IMPORTANT]  
> We strongly recommend running the backup process at least _**twice**_ to ensure data integrity. After completing a backup, be sure to copy **all** files from the `0_Firmware_Root` directory to a secure location, otherwise they **_will_** be overwritten!  Keep _**both**_ backup copies for safekeeping and future reference.  

Carefully follow these steps to ensure the Cloner application is set up correctly and operates as expected.

## Vendor Documentation

Refer to the vendor documentation for additional in-depth information.  

[Quick Guide PDF](https://thingino.com/dl/USBCloner_The_Burn_tool_Quick_Guide.pdf)

## Tips and tricks

### Borrow USB port from the WiFi

If your camera is equipped with a USB wireless module, the USB port will most likely not be OTG compatible and therefore cannot be used for Cloner. However, you can still make a makeshift connection by borrowing the USB data wires from the wireless module. Locate the `DP/D+` and `DN/D-` pads on the USB wireless module and solder the data wires from a stripped USB cable to them like shown below.

<a href="https://github.com/user-attachments/assets/3ba22645-a9c4-408d-97aa-b475774d5568">
  <img src="https://github.com/user-attachments/assets/3ba22645-a9c4-408d-97aa-b475774d5568" width="320" alt="USB wifi module pins">
</a>

### Force the system to go into cloner mode

To initiate a Cloner session from a running system, you need to damage the bootloader to force SoC to expose USB connection on boot.

> [!CAUTION]
> This action is irreversible, so you need to know what you are doing, and be ready to revive a possible brick!

To erase bootloder from U-Boot shell, run
```
sf probe; sf erase 0 +1; reset
```

To erase bootloder from Linux shell, run
```
flash_eraseall /dev/mtd0 && restart -f
```

Obviously, you only want to do that for flashing a new firmware. For making a backup of the existing firmware,
short pins 5 and 6 on the flash chip as described above.

### Videos

#### Flashing firmware with Cloner over USB

[![Flashing firmware with Cloner over USB](https://img.youtube.com/vi/nqjejNizvC0/0.jpg)](https://youtu.be/nqjejNizvC0)  

#### Flashing Wyze V3 with cloner in realtime 

[![Flashing Wyze V3 with cloner in realtime](https://img.youtube.com/vi/SJgadXkdwzw/0.jpg)](https://youtu.be/SJgadXkdwzw)  
    
