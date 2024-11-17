The Wuuk Y0510 is an inexpensive camera with a great price point for the quality of the camera.  It's currently seen with two different sensors, either the original, SC4336p or the less common SC401AI. 

# Flashing the device

## Formatting
You **must** use a MBR type formatted sd-card, this will not work with a GPT formatted card.


## Installation script 
Once your sd card is formatted then your should create a directory called `FACTORY` in the root of the sd card, and in the `FACTORY` directory place this [script](https://gist.github.com/wltechblog/bcc30aca647ee8eac5cb80c6b7368b98), naming it`factory_install.sh`.   

At the time of writing the script is as follows, but I'd recommend checking the link above for the upstream source.

```bash
#!/bin/sh
# WUUK Y0510 https://amzn.to/4dFlKv1
#
# Instructions
#
# Note: If we increase uboot beyond 256k this needs to be adjusted.
# Build thingino firmware, up to make pack_full, or grab full firmware file from github releases

# -- UPDATE --
# There are now 2 versions of this camera. Most use the sc4336p sensor, a few have the sc401ai sensor.
# if you install the sc4336p file and don't have video, grab the sc401ai file, rename it to autoupdate-full.bin,
# remove autoupdate-full.done, and reboot the camera to flash the new one.
# ------------

# Copy full thingio image to sd as /autoupdate-full.bin
# Put this script on sd as /FACTORY/factory_install.sh
# Insert SD card and power on camera, wait about 10 minutes, it will reboot a few times along the way.


mount -t vfat /dev/mmcblk0p1 /mnt
if [ ! -f /mnt/autoupdate-full.bin ]
then
	echo "Missing update file, aborting"
	exit
fi
echo "Extracing uboot"
dd if=/mnt/autoupdate-full.bin of=/mnt/u-boot-t31x.bin bs=1k count=256

if [ -f /mnt/u-boot-t31x.bin ] && [ -f /mnt/autoupdate-full.bin ]
then
	rm -f /mnt/autoupdate-full.done
	echo "Flashing uboot"
	flashcp /mnt/u-boot-t31x.bin /dev/mtd0
	echo "Rebooting"
	reboot
else
	echo "Files missing, not flashing"
fi
```

## Firmware

As mentioned above this camera comes with two different sensor varieties.  Don't worry too much about this, the easiest thing to do is pick a firmware, flash it, and get into the web interface of Thingino, if you happen to have picked the wrong one, you won't get any preview video stream and just repeat the process from this point using the alternative firmware.

Links to the two versions to download from the Thingino website, are included here for convenience.

[T31X, SC401AI, SSV6158, 16MB](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wuuk_y0510_sc401ai.bin)

[T31X, SC4336p, SSV6158, 16MB](https://github.com/themactep/thingino-firmware/releases/latest/download/thingino-wuuk_y0510_sc4336p.bin)

In the root folder of the sd card place the `.bin` you download, having renamed it `autoupdate-full.bin` 

## Final check & Flashing

Your SD card should be MBR formatted and contain the following
```                                             
├── autoupdate-full.bin
└── FACTORY
    └── factory_install.sh
```

With your camera powered down insert the SD card and power it on.  

The sequence I observed was as follows:

 - Solid red light ~ 15s
 - No light ~ 1m 40s
 - Solid blue light ~ 10s
 - Rapidly flashing blue light ~ 3s
 - Slowly flashing blue light & camera motors moving ~ 15s
 - No lights

When I had an unsuccessful flash (due to using a GPT formatted SD card I would observe slowly flashing blue lights (I had never paired the camera to the Wuuk app or services)

## Accessing the camera

You should now see a wireless access point available with the format:

**THINGINO-xxxx**

Connect to this and you should be able to see the following screen.

![setup](https://github.com/user-attachments/assets/6bf46f9d-6daa-43f2-946f-07c64fc9f808)

Fill in the data and click "Save credentials" then check the details on the following screen are correct and click "Proceed"

![verification](https://github.com/user-attachments/assets/20afb777-0e8f-44e3-abeb-7734b6f36d66)

