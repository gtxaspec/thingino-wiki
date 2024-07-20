This page reflects some notes from the development of Thingino for devices sold under the Galayou G2 brand. It is accurate as of July 2024.

The Galayou G2 comes in 2 variations. One uses a T31LC SoC and the 
other a T23N SoC.  This page discusses only the T23N variant.

## Stock firmware update notes
 
Unlike the Cinnado D1, which is also T23N based, the G2 does not accept unsigned firmware updates via the SD card.  
The bootloader includes a command `gvsdupdate` which checks for files `jzt23Nall.bin`, `jzt23Nsd.bin`, and `jzt23Nota.bin`
on the FAT partition of a SD card.  The format of these files appears to be:

- a 4-byte header that must be `gvfw` or `gsfw`
- a 64-byte signature
- followed by the firmware 

It appears to be using some kind of HMAC algorithm, perhaps a variation of HMAC-RS256.  
There is also a program `/app/bin/update` whose purpose is to allow firmware updates from user mode. This program was reverse engineered
with Qiling's user mode emulation to determine the information above, in combination with Ghidra.

Unfortunately, this requires that the device be opened in order to install Thingino. Either in-circuit flashing can be attempted, or a UART connection must be made.

## UART

The UART can be found here:

<img src="https://github.com/user-attachments/assets/25fc9137-381d-49f1-9af3-0ffdf1bebeb3" width="400">

## In-circuit flashing

Different developers have had different success with in-circuit flashing with a CH341 device and clip.
If attempting it, do not connect pin 8. The device appears to be using a [P25Q64H](https://www.puyasemi.com/download_path/%E6%95%B0%E6%8D%AE%E6%89%8B%E5%86%8C/Flash/P25Q64H_Datasheet_V1.4.pdf) 8MB nor flash chip surface mounted next to the 
SD card on the side of the board that has the SoC.  

## MMC oddity - 1-bit mode only

During testing, it was found that the MMC device does not operate in 4-bit mode.  Normally, an SD card provides 4 data lines (D0 to D3),
but in this device it appears to operate in 1-bit mode.  This is odd because the existing code did not even provide an option for this mode - the default capability of the host controller was set to 4 bits.  This was solved by adding a [`isvp_t23n_sfcnor_mmc1bit`](https://github.com/gtxaspec/u-boot-ingenic/commit/40303cc4e9c4f790ca235f972066c5c9a2bb778e) configuration to Thingino UBoot and a corresponding kernel configuration option to Thingino's Linux kernel [CONFIG_JZMMC_V12_MMC0_1BIT](https://github.com/gtxaspec/thingino-linux/commit/a4417fd29af2f77a2b303bccb969b49c105fedc0).
