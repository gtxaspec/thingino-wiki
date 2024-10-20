# Background

I had previously flashed a camera with Dafang and also flashed the boot loader in order to enable 1080 video feeds.  When I came to replace Dafang with Thingino I found that the normal install process of putting in an SD card and holding down the button didn't work.

With the help of the developers on Discord I was able to get the camera working again and here is what I had to do.  Your mileage may vary.

# Before you start

If you still have a working Dafang camera and associate SD card then make a backup of that SD card.  You need to be able to get a shell on to the Dafang in order to complete this process so keeping a copy of the existing card image might allow you to get back to a shell in order to try flashing again.

Ideally find another SD card so that you can leave your working Dafang card alone for now.

You need to be able to get a working shell on to the Dafang install running on the camera.

# Downloads needed

You need to download:
 - The [Uniflasher](https://raw.githubusercontent.com/themactep/thingino-firmware/refs/heads/master/scripts/uniflasher.sh) script from Thingino
 - [A compiled Busybox with `flashcp` enabled](https://github.com/gtxaspec/wz_mini_hacks/raw/refs/heads/master/SD_ROOT/wz_mini/bin/busybox).  The version that ships with Dafang is missing flashcp. Use the version from wz_mini_hacks.
 - The correct firmware for your camera.  In my case it was [thingino-wyze_c2_jxf23.bin](https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-wyze_c2_jxf23.bin)
 
Copy all these files to the root of Dafang SD card (or a clone of it, if you have a spare card).

# Process

With those files copied to the SD card, insert the card in to the camera and boot normally in to Dafang.

SSH in to the camera.

## Replace busybox

First we need to replace the stock `busybox` with the version from `wz_mini_hacks`.  From the shell:

```bash
cd /system/sdcard
chmod u+x busybox
cd bin
cp busybox busybox.ori
cp ../busybox .
reboot
```

Once the camera has reboot you should be able to go back in to the shell and run `busybox`.  You should see something like:

```text
BusyBox v1.35.0 (2022-05-14 10:38:19 UTC) multi-call binary.
BusyBox is copyrighted by many authors between 1998-2015.
Licensed under GPLv2. See source distribution for detailed
copyright notices.
```

In the `Currently defined functions:` section you should see `flashcp`.  If you do, proceed to the next step.

## Flashing the new image

The `uniflasher` script uses `flashcp` to write the firmware to the device.

To do that, in a shell:

```bash
cd /system/sdcard
chmod u+x uniflaser.sh
./uniflasher thingino-wyze_c2_jxf23.bin
```

If that works you should see:

```text
killall: majestic: no process killed
killall: httpd: no process killed
killall: ntpd: no process killed
killall: crond: no process killed
mtd0
----------
 Extracting block of  bytes starting at 0
8+0 records in
8+0 records out
262144 bytes (256.0KB) copied, 0.001988 seconds, 125.8MB/s
 Flashing partition mtd0
Erasing block: 8/8 (100%) 
Writing kb: 256/256 (100%) 
Verifying kb: 256/256 (100%) 

mtd1
----------
 Extracting block of 262144 bytes starting at 262144
64+0 records in
64+0 records out
2097152 bytes (2.0MB) copied, 0.039155 seconds, 51.1MB/s
 Flashing partition mtd1
Erasing block: 64/64 (100%) 
Writing kb: 2048/2048 (100%) 
Verifying kb: 2048/2048 (100%) 

mtd2
----------
 Extracting block of 2097152 bytes starting at 2359296
106+0 records in
106+0 records out
3473408 bytes (3.3MB) copied, 0.077025 seconds, 43.0MB/s
 Flashing partition mtd2
Erasing block: 106/106 (100%) 
Writing kb: 3392/3392 (100%) 
Verifying kb: 3392/3392 (100%) 

mtd3
----------
 Extracting block of 3473408 bytes starting at 5832704
20+0 records in
20+0 records out
655360 bytes (640.0KB) copied, 0.011769 seconds, 53.1MB/s
 Flashing partition mtd3
Erasing block: 20/20 (100%) 
Writing kb: 640/640 (100%) 
Verifying kb: 640/640 (100%) 

mtd4
----------
 Extracting block of 655360 bytes starting at 6488064
148+0 records in
148+0 records out
4849664 bytes (4.6MB) copied, 0.066953 seconds, 69.1MB/s
 Flashing partition mtd4
Erasing block: 148/148 (100%) 
Writing kb: 4736/4736 (100%) 
Verifying kb: 4736/4736 (100%) 

mtd5
----------
 Extracting block of 4849664 bytes starting at 11337728
64+0 records in
64+0 records out
2097152 bytes (2.0MB) copied, 0.043287 seconds, 46.2MB/s
 Flashing partition mtd5
Erasing block: 64/64 (100%) 
Writing kb: 2048/2048 (100%) 
Verifying kb: 2048/2048 (100%) 

mtd6
----------
 Extracting block of 2097152 bytes starting at 13434880
20+0 records in
20+0 records out
655360 bytes (640.0KB) copied, 0.021077 seconds, 29.7MB/s
 Flashing partition mtd6
Erasing block: 20/20 (100%) 
Writing kb: 640/640 (100%) 
Verifying kb: 640/640 (100%) 

mtd7
----------
 Extracting block of 655360 bytes starting at 14090240
64+0 records in
64+0 records out
2097152 bytes (2.0MB) copied, 0.047924 seconds, 41.7MB/s
 Flashing partition mtd7
Erasing block: 64/64 (100%) 
Writing kb: 2048/2048 (100%) 
Verifying kb: 2048/2048 (100%) 

mtd8
----------
 Extracting block of 2097152 bytes starting at 16187392
8+0 records in
8+0 records out
262144 bytes (256.0KB) copied, 0.002157 seconds, 115.9MB/s
 Flashing partition mtd8
Erasing block: 8/8 (100%) 
Writing kb: 256/256 (100%) 
Verifying kb: 256/256 (100%) 

mtd9
----------
 Extracting block of 262144 bytes starting at 16449536
8+0 records in
8+0 records out
262144 bytes (256.0KB) copied, 0.005844 seconds, 42.8MB/s
 Flashing partition mtd9
Erasing block: 8/8 (100%) 
Writing kb: 256/256 (100%) 
Verifying kb: 256/256 (100%) 

mtd10
----------
 Extracting block of 262144 bytes starting at 16711680
2+0 records in
2+0 records out
65536 bytes (64.0KB) copied, 0.000660 seconds, 94.7MB/s
 Flashing partition mtd10
Erasing block: 2/2 (100%) 
Writing kb: 64/64 (100%) 
Verifying kb: 64/64 (100%) 

Done. Please reboot.

```

Then type `reboot`

## Booting in to Thingino - or not...

In theory you should now be in Thingino.  Using your phone check for a Thingino wifi access point.  If you can see one, then connect to it and finish the configuration.  You're done!

If not... I had a strange problem which meant that the camera wouldn't boot to a shell.  When powering on the camera the LED didn't flash at all.  To fix this I downloaded the [wyze-cam-2](https://github.com/wltechblog/thingino-installers/raw/refs/heads/main/wyze-cam-2/wyze-cam-2.zip) file from thingino-installers.  I formatted the SD card as FAT32 and copied to contents of that wyze-cam-2 zip file to the root of the SD card.
Then power off the camera, insert the card, and power on again - but without holding down the button.

If the LED starts flashing then you're very likely good to go.  Check for the Thingino wifi access point and you can configure the camera and connect it to your network.  Done!
