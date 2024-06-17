### I use Windows...

Don't.

### SD card is not recognized at boot

There are two factors that can affect SD card detection during the boot sequence.

One is that the GPIO pins for powering the SD card slot and detecting the presence of a card are not set.
You can fix this by setting these pins in the environment.
You need to set at least the `gpio_mmc_power` and `gpio_mmc_cd` pins.

Another factor is that not every card is detected correctly.
You can try different cards (different class, size, etc) to find the one that works.

### autoupdate-full.bin and/or uEnv.txt not picked up on boot

This is most likely an extension of the above problem.
If your camera cannot detect the SD card during boot, then none of these files can be accessed and processed by U-Boot.

Interrupt the boot process with `Ctrl-C` and get into the boot shell.
Once in the shell, set the GPIO pin to power up MMC bus, and reinsert the card. 
Make sure it is recognized correctly and you can access the files

```
gpio clear 48;
mmc rescan;
mmcinfo;
fatls mmc 0;
```

then install the firmware as follows

```
setenv baseaddr 0x82000000;
setenv flashsize 0x1000000;
mw.b ${baseaddr} 0xff ${flashsize};
fatload mmc 0:1 ${baseaddr} autoupdate-full.bin;
sf probe 0; sf erase 0x0 ${flashsize};
sf write ${baseaddr} 0x0 ${filesize};
reset
```

You will still need to set the correct environment for your hardware.
Interrupt the boto process once again, set the GPIO pin for MMC,
check the card is recognized

```
gpio clear 48;
mmc rescan;
mmcinfo;
fatls mmc 0;
```

and import the environment settings from the file on the card

```
fatload mmc 0 ${baseaddr} uEnv.txt;
env import -t ${baseaddr} ${filesize};
saveenv;
reset
```

Alternatively, import the enviroment settings from within Lunux:

```
sed 's/=/ /' /mnt/mmcblk0p1/uEnv.txt > env.txt;
fw_setenv -s env.txt
```

### Failsafe Mode

Failsafe mode provides a safety net for systems that may encounter issues during the normal boot process. Accessible exclusively via UART console, this mode allows users to intervene manually before the system completes its regular startup sequence. 

To enter failsafe mode, users must connect to the device through a UART interface. During the initial stages of boot, a prompt appears on the console: 

`Press the [f] key to enter failsafe mode`

By pressing 'f' within this window, the boot process is halted, and the user is granted access to a minimal emergency shell. This shell can be used to perform troubleshooting tasks, modify system configurations, or recover from errors that prevent the system from booting correctly. If the failsafe mode is not invoked within the given timeframe, the system proceeds to boot normally. This feature is crucial for enabling system accessibility during scenarios where the system may not be operating properly during a normal boot.

### Image in my prevew appears pink-ish

Your IRCUT filter maybe controlled in reverse. To check the camera's IRCUT mode. Point the camera at a reflective surface. Run ircut on; irled on in the console. You should see slightly visible IR LEDs on the camera. 

![image](https://github.com/themactep/thingino-firmware/assets/37488/eb0baeac-d882-4029-85f8-e633354e5ea8)

If, instead, you see brightly glowing IR LEDs, the order of your IR cut filter pins in the environment needs to be reversed.

![image](https://github.com/themactep/thingino-firmware/assets/37488/c9660287-502b-4c3a-91cc-e5f9950c0c29)

Read the values from the environment and then save them in the reverse order as shown below.

```
[root@wyze-v3-test ~]# fw_printenv -n gpio_ircut
25 26
[root@wyze-v3-test ~]# fw_saveenv gpio_ircut 26 25
```