The Ingenic USB Cloner application is a PC side utility that interfaces with the "USB-Boot" mode built into Ingenic SOCs.
By placing the SOC into "USB-Boot" mode, you are able to use the Ingenic USB Cloner to directly flash the firmware chip
without physically removing, or interfacing to the flash chip.  This method simplifies firmware backup and installation on capable devices.

This guide provides step-by-step instructions for completing a full backup and writing a firmware binary to your device. It is designed to walk you through the process, helping you become familiar with the Ingenic Cloner tool. However, please note that this guide is not intended to be an all-inclusive reference and does not cover all features of Cloner. It focuses on the basic steps needed to perform the outlined tasks, offering a foundation for using the utility effectively.

## Downloading Cloner  
> [!TIP]
> For better success and compatibility, we strongly recommend using the Linux version of Ingenic USB Cloner.

Download the Cloner application for your operating system using the links below. Extract the program to a working directory on your computer.

- [Ingenic Cloner for Linux](https://thingino.com/dl/cloner-2.5.43-ubuntu_alpha_thingino.tar.gz)
- [Ingenic Cloner for Windows](https://thingino.com/dl/cloner-2.5.43-windows_alpha_thingino.zip)

Navigate to the `cloner-2.5.xx-ubuntu_alpha` directory, with "xx" indicating your downloaded version of Cloner.

> [!IMPORTANT]  
> Windows users may need to install additional drivers for support.  See the [[Vendor Documentation|Ingenic-USB-Cloner#vendor-documentation]] PDF Guide for additional details.

Create a folder named `0_Firmware_Root` inside the Cloner directory.

![](https://github.com/user-attachments/assets/28584a28-394c-47ac-9fd7-14b8e9120be3)

> [!CAUTION]
> The `0_Firmware_Root` directory **MUST** be created and correctly named to ensure backups are completed successfully.  

Open the Cloner application. Ensure you are using version 2.5.43 for compatibility.

![](https://thingino.com/a/cloner-0-1.png)

## Installing configuration bundle 

- Download the latest configuration bundle [from here](https://github.com/gtxaspec/ingenic-cloner-profiles/releases/download/latest/cloner_profiles.ingenic).

Click **Load Image** and select the downloaded `cloner_profiles.ingenic` file.
 
![](https://thingino.com/a/cloner-0-2.png)

> [!IMPORTANT]  
> The options described in the screenshots will not match if you did not load the `cloner_profiles.ingenic` bundle as outlined in the previous steps.

## Enable configuration mode  

Change the **Lock Level** from **2**, to **0**

![](https://thingino.com/a/cloner-0-3.png)

Enter **_!@#_** (_exclamation mark_, _"at" symbol_, _number sign_) as the password.  Click OK.

![](https://thingino.com/a/cloner-0-4.png)

## Cloner configuration

After entering the password in the previous step, the **Config** button should now appear in the main screen. Click the **Config** button in the top-right corner.

![](https://thingino.com/a/cloner-0-5.png)

In the **Config** window, under the **INFO** tab, access various configuration menus.

In the **Platform** dropdown menu, select **_T_**. Choose the appropriate SOC version for your device next to **_Platform T_**.

![](https://thingino.com/a/cloner-0-6.png)

Next, you can proceed with either performing a [[backup|Ingenic-USB-Cloner#backup]] or [[writing firmware|Ingenic-USB-Cloner#writing-firmware]].

## Cloner Function Setup

### Backup

> [!WARNING]  
> We **strongly recommend** using Cloner to create a **full backup** of the existing stock firmware. This is an essential step if you ever need to restore the original functionality or analyze the stock firmware for compatibility.

In the **Board** dropdown menu, choose the appropriate _**reader**_ operation based on your device's flash chip size. The available options are 8MB, 16MB, and 32MB.

For the example below, we will select: _sfc_nor_reader_16M.cfg_ for the specific SoC.

![](https://github.com/user-attachments/assets/ced87cec-5ae5-407f-ad43-a4f5d89bcf0f)

Click the **Save** button to save your choice and return to the main menu.

![](https://github.com/user-attachments/assets/a5db14c8-b688-4f52-a3b2-af1fb63d9b14)

You may now begin [[the backup operation.|ingenic-usb-cloner#starting-cloner-operations]]

### Writing Firmware

In the **Board** dropdown menu, select the appropriate _**writer**_ operation based on your specific needs. The available options are:

- **_sfc_nor_writer.cfg**: for writing individual partitions  
- **_sfc_nor_writer_full.cfg**: for writing full firmware images

![cloner writer full profile](https://thingino.com/a/cloner-0-7.png)

Find and click on the **POLICY** tab, then click **...** (_three dot_) button in the setting column to open the file selection dialog.

![](https://thingino.com/a/cloner-0-8.png)

Select the firmware image file you want to write, and click Open.

![](https://thingino.com/a/cloner-0-9.png)

Once you have selected your firmware image file for writiing, click the **Save** button to return to the main screen.

![](https://thingino.com/a/cloner-0-10.png)

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
