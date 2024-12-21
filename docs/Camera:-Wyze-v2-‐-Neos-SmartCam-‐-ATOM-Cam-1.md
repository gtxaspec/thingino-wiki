# Wyze v2 / Neos SmartCam /ATOM Cam 1

<img src="https://github.com/user-attachments/assets/aef89340-0abe-48df-80a7-9c5b00b8e0d9" width="150">

These cameras are very popular and have been hackable for quite some time via a numerous other (mostly defunct?) projects. There are much better contemporary cameras that offer greater value for the cost, so don't go out and buy these, but if you already own them they are relatively easy to get up on Thingino firmware.
## Features
* Ingenic T20X
* 16 MB of NOR SPI (ZB25VQ128ASIG)

The device itself is very simple, it has an SD card slot, a Setup button and a Status light to the right of the power input. There is a USB-A socket for accessories and debugging and a MicroUSB for power.  
## Support status
This camera is fully supported by Thingino. Grab the latest release from [releases](https://github.com/themactep/thingino-firmware/releases/latest), or use `sysupgrade -p` for an in-place upgrade if you're already running Thingino.

#### Which method should I use to install?
That's entirely upto you, the first method is the simplest and the second allows a user to revert back to the legacy firmware and backup the SOC version. The intrusive method requires opening up the camera and should be used when the other methods are no longer working.  

## Non-intrusive 1 Disk Installation method. 
This consolidated installer takes our 4 step method, combines these together into one card and includes firmware for both SOC types and automatically chooses the correct one. 

1. Download [this Zip file](https://github.com/wltechblog/thingino-installers/blob/main/wyze-cam-2/wyze-cam-2.zip), extract it to your computer. 
2. Format the SD card as FAT32, copy the contents of the Zip file to the root of the SD card. 
3. Insert the SD card into the Camera. 
4. Press and Hold the SETUP button, and power on the camera.
5. After 5 seconds and the light changes, release the button.
6. Wait for the flash process to complete. The process takes just under 4 minutes all up.

Congratulations, thingino should now be installed.  
Press the setup button and you should hear a beep. Power cycle the device or Hold the Setup button to create the temporary Wifi network for configuration. Be patient, this device can take almost 30 seconds to reboot entirely.  
#### Wifi setup. 
Use your mobile or Computer, search for a Wifi network called Thingino_xxxx and connect to it. 
Goto your browser and browse to the thingino.local address or 172.16.0.1 

Configure a device name, root password, Wifi SSID + Password, click save, confirm the details and save to let the device reboot. 

Use the short link on the redirect page or goto your router/networking device to determine which IP the camera got.  Goto that url and login with the username root and the password you provided during the setup. 

## Non-intrusive 4 Disk Installation method. 
We have created these instructions to use as a guide for a non-Intrusive method to flash the camera. It consists of a Zip file with 3 Images and the 3rd Image will be needed to determine the correct firmware file to download from the website. 

You will need a computer, Micro SD card(s) depending if you want to reuse and reformat each time.  

Download this zip file and extract it to your computer.  
 [niti-wyze_c2_cp1.7z](https://thingino.com/dl/niti-wyze_c2_cp1.7z)

#### Disk 1 
`
This step in the process will upgrade the bootloader to the one that can load a custom kernel for use in Disk 2.
`
1. Format the first SD card to FAT32.
2. Copy content of the `card1/` directory to the card.
3. Insert the card into the camera.
4. Press and Hold the SETUP button, and power on the camera. 
5. After 5 seconds and the light changes, release the button.
6. Wait for the device to click and reboot. 
`The camera lights will change througout the process. Its initially Yellow while the bootup occurs, after you lift your finger from the setup button the light will be solid blue. First click, then the camera completes the flash with a flashing lightshow. You will hear a click and the light will go off then solid yellow.  This process can take anywhere between 1-2minutes`

#### Disk 2
`
This step in the process will flash a compatible version (Wyze v2 4.9.8.1002) onto the camera to complete the next steps of backing up the firmware and extracting the sensor and board details. 
`
1. Format the second SD card to FAT32.
2. Copy content of the `card2/` directory to the card.
3. Insert the card into the camera.
4. Press and Hold the SETUP button, and power on the camera. 
5. After 5 seconds and the light changes, release the button.
6. Wait for the device to click and reboot. 

`The lights will show yellow momentarily, then solid blue.  Wait for the camera to click and reboot. The camera will show a flashing yellow light once complete.  
`

#### Disk 3
`
This step is about backing up the firmware you just installed and dumping the details about the board and sensor and preparing the camera to flash Thingino
`
1. Format the second SD card to FAT32.
2. Copy content of the `card3/` directory to the card.
3. Insert the card into the camera.
4. Press and Hold the SETUP button, and power on the camera. 
5. After 5 seconds and the light changes, release the button.
6. Wait for the device to click and reboot. 
`The camera lights will change througout the process. Its initially Yellow while the bootup occurs, after you lift your finger from the setup button the light will be solid blue. First click, then the camera completes the flash with a flashing lightshow. You will hear a click and the light will go off.  This process can take anywhere between 1-2minutes`
At this point the camera does not have a light when powered on and does not respond to the setup button being pushed. 

The camera has now dumped some additional files on the SD card. Take it out of the camera and inspect it on the computer. 

Goto the folder `WYZE_BACKUP_XXX`
Inspect the file `SENSOR_VER` and look for the value returned from the Sensor detection. 
Inspect the file `SOC_VERSION` and look for the value returned for the SOC. 

Goto the [Thingino Main](https://thingino.com/) page and find the model > and Sensor / SOC version to download. 

Download this file you will need it to create disk 4. 

#### Disk 4
`
This step is where you will actually flash the thingo image.  Use the specific file you downloaded from the previous step. 
`
1. Format the second SD card to FAT32.
2. Copy the file to the SD card and rename the file to `autoupdate-full.bin`
3. Insert the card into the camera.
4. Power on the camera. 
6. Wait for the device to click and reboot. This process can take 2-3minutes. 

Your camera now has the custom firmware installed. You can confirm this by pressing the setup button and you will hear a beep.
#### Wifi Setup. 

The camera wifi needs to be configured and will only remain active for (x) minutes initially on boot for security reasons.  

Use your mobile or Computer, search for a Wifi network called Thingino_xxxx and connect to it. 
Goto your browser and browse to the thingino.local address or 172.16.0.1 

Configure a device name, root password, Wifi SSID + Password, click save, confirm the details and save to let the device reboot. 

Use the short link on the redirect page or goto your router/networking device to determine which IP the camera got.  Goto that url and login with the username root and the password you provided during the setup. 

Congrats, you now have Thingino installed. 

## Camera Bricked/Not Responding?! Use this method to flash the device directly via USB.  
In order to use this tool, you'll need to open the camera. This usually breaks the seals, so it's possible the camera won't be "exterior proof" anymore. 

#### Software setup. 
First you will need to configure the [Cloner tool](https://thingino.com/cloner) on your computer.  Download the file, extract it, somewhere on your machine. 

Connect the USB socket and ensure the device is connected and device driver is detected correctly. Reference to this here in the [Cloner wiki](https://github.com/themactep/thingino-firmware/wiki/Ingenic-USB-Cloner).  

Open the cloner tool, Open Config. 
In the Info tab, select Platform T and T20, for board select `writer_full`
In the Policy tab, click the 3 dot menu, select the thingino firmware file you want to flash. 
Click Save for the Config.  

#### Physical Setup
Now you need to open the device. [Here is a video tutorial.](https://www.youtube.com/watch?v=RV6-kR1KCwU&t=3s) 

Disassembly Instructions:
1. Flip the device over, remove the two silver screws. 
2. Pry from the front/lens side of the device, the bottom has 2 clips to the rear that hold the movable foot and base in place. 
3. Gently pry the edges of the back panel from the two side panels, there are 4 clips per side and two at the top. You my need to apply some force. 
4. Gently maneuver the backplate out of the way being mindful of the speaker cable and backplate. 

Now you need to understand a little bit about how to get the device into bootloader mode. On this device there is a small chip beside the Ingenic chip where we need to bridge the Pins 5&6 while booting to initialize correctly.  

[<img src="https://github.com/user-attachments/assets/1729af3b-43a1-4152-9cb5-1d9a4ea02d0d" width="200">](https://github.com/user-attachments/assets/1729af3b-43a1-4152-9cb5-1d9a4ea02d0d) <img src="https://camo.githubusercontent.com/851273986d66f0f08eedf08a68ab25da4d4acacd14912a5995d5a90dd0bae7b5/68747470733a2f2f7468696e67696e6f2e636f6d2f612f666c6173682d636869702d73686f72742e706e67" width="200">

The device has 2 USB sockets on it, a Micro-USB for power and a USB-A connection for accessories and debug/flashing.  You will need to find a USB cable to connect the USB-A to your computer.  You may need a USB-A to USB-A or you may need to create one yourself.  Shorting the pins above enables this USB-A socket, the Micro-USB cannot be used to flash the device.  

Now you have the device ready and understand how to short the pins, the driver ready and the cloner software ready.  Lets get ready to flash. 
#### Flashing instructions 

1. Remove the camera from USB. 
2. Click Start on the USB cloner device, tail the log/window, observe the `start burner` message. (note: the device should not be connected to the computer yet) 
3. Bridge the pins 5&6 listed above. 
4. Connect the USB device to the computer. 
5. Wait 5-10 seconds with the connected pins, Observe the boot progress bar moving 
6. Wait for both `boot` and `full image` progress bars to complete 
7. Remove the USB 

Power on the device, congratulations Thingino should be installed, follow the Wifi setup details from the non-intrusive Disk 4 step above to get it connected to Wifi.  

Here is a more generic guide of this in [Video form. ](https://youtu.be/nqjejNizvC0?si=1LRzRBdrxkOgQxHa)

## Which Firmware Version Do I Need?
There are 2 image sensors used in these cameras ([JXF22](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) and [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf23.bin)).  Identifying which version you have is difficult, but it's very easy to switch to the "right" version for your particular camera.  Installing the "wrong" version is just fine, and won't brick your device.  You can access the device and interact with it, the only problem is that you won't see an actual image from the camera.  If this is the case, just switch to the other version

1. Install one of the versions - just pick one.  If you're not sure, or can't flip a coin to choose, just grab the [JXF23](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wyze_c2_jxf22.bin) version.
2. Follow the standard Thingino install instructions.
3. Log into the camera via web interface.
4. If you don't see an image from your camera, you need to switch to the other version.
5. Connect via SSH
6. Edit `/etc/os-release` to point to the new version
7. Run the upgrade process with the `sysupgrade -p` command, which will auto-switch you to the other firmware version.  After that process finishes, check again and images should show correctly.

-----
### Q & A  

#### Thingino seems to be installed but I cant see it on my Wifi? How can I reset the configuration? How do I reset the Wifi ? 
You might just need to reset the device.  
Power the device on, click the setup button once and you will hear a beep. 
Hold down the setup button until you hear a longer beep, you will hear the device click and reboot and the Blue light will begin flashing. 

The camera wifi needs to be configured and will only remain active for (x) minutes initially on boot for security reasons.  

Use your mobile or Computer, search for a Wifi network called Thingino_xxxx and connect to it. 
Goto your browser and browse to the thingino.local address or 172.16.0.1 

Configure a device name, root password, Wifi SSID + Password, click save, confirm the details and save to let the device reboot. 

Use the short link on the redirect page or goto your router/networking device to determine which IP the camera got.  Goto that url and login with the username root and the password you provided during the setup. 

#### I tried the non-intrusive method but my device does not respond when I connect to power? No lights and no beep or message when I press setup. 

The firmware on the device may be corrupt.  Please follow the instructions above to open the device and connect the USB to the computer to flash manually. 

#### Do you support the Wyze Sensors?
No not yet,  we are looking for community contributions to continue to support this hardware. 

-----

### Videos

#### NEOS/Wyze V2 "No Tools" Installer Thanksgiving Update - Faster, easier, more reliable!

[![NEOS/Wyze V2 "No Tools" Installer Thanksgiving Update - Faster, easier, more reliable!](https://img.youtube.com/vi/Ax6usUOjxkY/0.jpg)](https://youtu.be/Ax6usUOjxkY)

#### Neos SmartCam - Continue using this camera after they shut it down! ONVIF & Home Assistant support!

[![Neos SmartCam - Continue using this camera after they shut it down! ONVIF & Home Assistant support!](https://img.youtube.com/vi/YTFl2VkCLbM/0.jpg)](https://youtu.be/YTFl2VkCLbM)

#### Neos SmartCam - firmware free upgrade to open source Thingino

[![Neos SmartCam - firmware free upgrade to open source Thingino](https://img.youtube.com/vi/RkxzdsKsP8M/0.jpg)](https://youtu.be/RkxzdsKsP8M)