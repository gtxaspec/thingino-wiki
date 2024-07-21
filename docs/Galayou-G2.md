This page reflects some notes from the development of Thingino for devices sold under the [Galayou G2](https://www.galayou-store.com) brand. It is accurate as of July 2024.

The Galayou G2 comes in 2 variations. One uses a T31LC SoC and the 
other a T23N SoC.  This page discusses only the T23N variant.

## Attempting to update via the Stock Firmware Update process
 
Unlike the Cinnado D1, which is also T23N based, the G2 does not accept unsigned firmware updates via the SD card.  
The bootloader includes a command `gvsdupdate` which checks for files `jzt23Nall.bin`, `jzt23Nsd.bin`, and `jzt23Nota.bin`
on the FAT partition of a SD card.  The format of these files appears to be:

- a 4-byte header that must be `gvfw` or `gsfw`
- a 64-byte signature
- followed by the firmware 

It appears to be using some kind of HMAC algorithm, perhaps a variation of HMAC-RS256.  
There is also a program `/app/bin/update` whose purpose is to allow firmware updates from user mode. This program was reverse engineered
with [Qiling's user mode emulation to determine the information above](https://gist.github.com/godmar/bf05db4e6e014977ae3f4351d057c36d), in combination with [Ghidra](https://ghidra-sre.org/).

Unfortunately, these facts require that the device must be opened in order to install Thingino. 
Either in-circuit flashing of the flash chip can be attempted, or a UART connection must be made. Both will be explained in turn.

## Opening the device

To open the case, it's not necessary to remove the base. You can use a special tool which most of you have readily available, as shown in this video:

[Instructional video of how to professionally open a G2](https://github.com/user-attachments/assets/7d187996-7663-473d-a047-c3bd146ea6c4)

## Installation via UART + SDCard

The UART can be found here:

<img src="https://github.com/user-attachments/assets/25fc9137-381d-49f1-9af3-0ffdf1bebeb3" width="400">

To flash Thingino we can use the stock UBoot loader.  However, this vendor decided to remove the commands that would
allow us to access the FAT file system.  For this reason, we need to write the image as a raw sequence of blocks onto an
empty SD card, using the following steps. **Pro tip: make sure your SD card is really in `/dev/sda` and not something you still need**!
```
wget https://github.com/themactep/thingino-firmware/releases/download/firmware/thingino-galayou_g2_t23n.bin
sudo dd seek=16 bs=512 if=thingino-galayou_g2_t23n.bin of=/dev/sda oflag=direct conv=fsync
```
This will write the 8MB image at offset 16 (sector) to the device (the offset is chosen so that the partition table is kept intact.)
This will destroy any filesystem on the SD card's first partition, so the card will no longer mount.

Next, insert the SD card into the camera (ideally with the camera turned off).  If the camera is on and running the
stock firmware while a card is inserted, it will try to mount it (which in this case will fail since the FAT filesystem was destroyed).

Now attach a terminal program to your UART adapter (`screen` or `minicom`, as described under [[UART Commands|UART-Connection#commands-for-various-terminal-programs-with-session-logging]]) and turn on the camera.  When you see a message to ``hit any key'', do so.  
You would see:
```
U-Boot SPL 2013.07 (Nov 18 2023 - 10:39:44)
Board info: T23N

apll_freq = 1188000000 
mpll_freq = 1200000000 
sdram init start
DDR clk rate 600000000
image entry point: 0x80100000


U-Boot 2013.07 (Nov 18 2023 - 10:39:44)

Board: ISVP (Ingenic XBurst T23 SoC)
DRAM:  64 MiB
Top of RAM usable for U-Boot at: 84000000
Reserving 215k for U-Boot at: 83fc8000
Reserving 32784k for malloc() at: 81fc4000
Reserving 32 Bytes for Board Info at: 81fc3fe0
Reserving 124 Bytes for Global Data at: 81fc3f64
Reserving 128k for boot params() at: 81fa3f64
Stack Pointer at: 81fa3f48
Now running in RAM - U-Boot at: 83fc8000
MMC:   msc: 0
the manufacturer 85
SF: Detected P25Q64H

In:    serial
Out:   serial
Err:   serial
Net:   ====>PHY not found!Jz4775-9161
Hit any key to stop autoboot:  0 
isvp_t23# 
```
Run `mmc rescan` and `mmcinfo` to make sure your card is recognized.
```
isvp_t23# mmc rescan
isvp_t23# mmcinfo
Device: msc
Manufacturer ID: c8
OEM: 55aa
Name: APPSD 
Tran Speed: 50000000
Rd Block Len: 512
SD version 2.0
High Capacity: No
Capacity: 121 MiB
Bus Width: 1-bit
```
Now you're ready to read the firmware from the SD card into RAM. We pick `0x82000000` as a free address for a temporary buffer.
```
isvp_t23# mmc read 0x82000000 0x10 0x4000

MMC read: dev # 0, block # 16, count 16384 ... 16384 blocks read: OK
```
This will read `0x4000` (16384) sectors of size 512 into RAM at address `0x82000000`, starting at sector `0x10` (16).
Verify that the data was read correctly by looking at the first eight words using `md`:
```
isvp_t23# md 0x82000000 8
82000000: 03040506 55aa5502 00001daa 00003200    .....U.U.....2..
82000010: 00000000 00000000 00000000 00000000    ................
```
Now you're ready to write this block of data to the flash.
First, check that the flash is recognized with `sf probe 0`. You should see
```
isvp_t23# sf probe 0
the manufacturer 85
SF: Detected P25Q64H

--->probe spend 4 ms
```
Then, erase the flash:
```
isvp_t23# sf erase 0x0 0x800000
SF: 8388608 bytes @ 0x0 Erased: OK
--->erase spend 278 ms
```
Now write the new image to the flash (takes 51s in this example):
```
isvp_t23# sf write 0x82000000 0x0 0x800000
SF: 8388608 bytes @ 0x0 Written: OK
--->write spend 51612 ms
```
Now type `reset` and the device should reboot into Thingino.
You'll see it reboot twice before going into portal mode; see [[instructions here|Configuring-Wi‐Fi-Access#captive-portal]].
Set it up via the portal.

Then, your Thingino should be on your network. If your router respects DHCP requested IP addresses, and if `192.168.1.10` is unused in your network, it might be there. If not, get the IP address either from your router or log in as root and check `ip a`.

Two steps remain which you can do via the WebUI:

- Under Settings -> IMP Control, flip the image horizontally and vertically:

![image](https://github.com/user-attachments/assets/541eefde-d94f-4888-adf7-c78821b49db7)

Don't forget to hit `Save`.

- Under Settings -> Time, set your Timezone and reboot.

Finally, you can remove the serial connection and log into the camera:
```
$ ssh root@192.168.1.10
root@192.168.1.10's password: 

  \\   _______ _     _ _____ __   _  ______ _____ __   _  _____
  )\\     |    |_____|   |   | \  | |  ____   |   | \  | |     |
 (  /     |    |     | __|__ |  \_| |_____| __|__ |  \_| |_____|
 / /
       galayou_g2_t23n
       master+aa093d1, 2024-07-19 23:13:50 -0700

[root@ing-galayou-g2-00cc ~]# 
```

## In-circuit Flashing

Different developers have had different success with in-circuit flashing with a CH341 device and clip.
If attempting it, do not connect pin 8. The device appears to be using a [P25Q64H](https://www.puyasemi.com/download_path/%E6%95%B0%E6%8D%AE%E6%89%8B%E5%86%8C/Flash/P25Q64H_Datasheet_V1.4.pdf) 8MB nor flash chip surface mounted next to the 
SD card on the side of the board that has the SoC. You would use a program such as [SNANDer](https://github.com/Droid-MAX/SNANDer) in this case. 

## MMC oddity - 1-bit mode only

During testing, it was found that the MMC device does not operate in 4-bit mode.  (See the output of `mmcinfo` above in the stock UBoot loader). Normally, an SD card provides 4 data lines (D0 to D3),
but in this device it appears to operate in 1-bit mode.  This is odd because the existing code did not even provide an option for this mode - the default capability of the host controller was set to 4 bits.  This was solved by adding a [`isvp_t23n_sfcnor_mmc1bit`](https://github.com/gtxaspec/u-boot-ingenic/commit/40303cc4e9c4f790ca235f972066c5c9a2bb778e) configuration to Thingino UBoot and a corresponding kernel configuration option to Thingino's Linux kernel [CONFIG_JZMMC_V12_MMC0_1BIT](https://github.com/gtxaspec/thingino-linux/commit/a4417fd29af2f77a2b303bccb969b49c105fedc0).
