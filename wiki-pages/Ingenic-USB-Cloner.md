The Ingenic USB Cloner application is a PC side utility that interfaces with the "USB-Boot" mode built into Ingenic SOCs.
By placing the SOC into "USB-Boot" mode, you are able to use the Ingenic USB Cloner to directly flash the firmware chip
without physically removing, or interfacing to the flash chip.

Download Cloner bundle for your operating system using the links below. Extract the bundle to a working directory on your computer.

- [Ingenic Cloner for Linux](https://thingino.com/dl/cloner-2.5.43-ubuntu_alpha_thingino.tar.gz) (recommended)
- [Ingenic Cloner for Windows](https://thingino.com/dl/cloner-2.5.43-windows_alpha_thingino.zip) (not recommended)

Navigate to the `cloner-2.5.xx-ubuntu_alpha` directory, with "xx" indicating your downloaded version of Cloner.

Create a folder named `0_Firmware_Root` inside the Cloner directory.

Open the Cloner application. Ensure you are using version 2.5.43 for compatibility.

![](https://thingino.com/a/cloner-0-1.png)

- Download extra configuration files [from here](https://thingino.com/dl/cloner_profiles.ingenic)
or [from here](https://github.com/gtxaspec/ingenic-cloner-profiles/releases/download/latest/cloner_profiles.ingenic).

Click "Load Image" and select the downloaded `cloner_profiles.ingenic` file.

![](https://thingino.com/a/cloner-0-2.png)

If the lock level became "2", change it back to "0".

![](https://thingino.com/a/cloner-0-3.png)

Enter _!@#_ (_exclamation mark_, _"at" symbol_, _number sign_) as the password.

![](https://thingino.com/a/cloner-0-4.png)

The **Config** button should reappear.

![](https://thingino.com/a/cloner-0-5.png)

Click the **Config** button in the top-right corner.

In the **Config** window, under the **INFO** tab, access various configuration menus.

In the **Platform** dropdown menu, select _T_. Choose the appropriate SOC version for your device next to _Platform T_.

![](https://thingino.com/a/cloner-0-6.png)

In the **Board** dropdown menu, select the relevant operation: _sfc_nor_writer_full.cfg_ for the selected SoC.

![](https://thingino.com/a/cloner-0-7.png)

On the **POLICY** tab, click "..." (_three dot_) button in the setting column and select the firmware image file you want to write.

![](https://thingino.com/a/cloner-0-8.png)

![](https://thingino.com/a/cloner-0-9.png)

Click **Save** button to return to the main screen.

![](https://thingino.com/a/cloner-0-10.png)

Click **Start** button on the main screen.

![](https://thingino.com/a/cloner-0-11.png)

Plug the USB cable into the device, leaving the other end unplugged.

If you are flashing a blank flash memory chip, or the bootloader is not installed, the Ingenic SoC will default to "USB-Boot" mode. Shorting pins on the flash chip is **not** required in this case.

Otherwise, locate the flash memory chip on the camera circuit board. Typically this is a square chip with 8 pins labeled _25Q64_ or _25Q128_, rarely _25L64_ or _25L128_. If you have trouble locating the chip, try taking some pictures of your board from both sides.

Pins 5 and 6 of the SOIC8 chip are on the opposite corner of pin 1, indicated by the embossed or drawn dot next to it.

![](https://thingino.com/a/flash-chip-dot.png)

Once you are ready to begin, short-circuit pins 5 and 6 of the flash chip with a small metal object, a screwdriver or tweezers.

Short pins 5 and 6 ON THE FLASH CHIP, not SoC or any other chip, use the photos as a reference, as described in this document.

__Do not try to short-circuit any random chip! It will most likely burn your camera circuit.__

![](https://thingino.com/a/flash-chip-short.png)

While maintaining the short, connect the USB cable to the computer. Wait 2 seconds, then release the short.

It may take up to 30 seconds for Cloner to recognize the device. Check your Device Manager, or `dmesg` for the Ingenic Cloner device.

![](https://thingino.com/a/windows-device-manager-libusb.png)

Once all progress bars turn green, the operations are complete.

Carefully follow these steps to ensure the Cloner application is set up correctly and operates as expected.

[Quick Guide PDF](https://thingino.com/dl/USBCloner_The_Burn_tool_Quick_Guide.pdf)
