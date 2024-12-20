# Installation Guide

## Required Materials
- Galayou G7 (T23)
- Micro SD card
- USB-TTL adapter (optional, for monitoring progress)
- Small tool for shorting flash pins

## SD Card Preparation

1. Format your Micro SD card following [this guide](https://github.com/themactep/thingino-firmware/wiki/Boot:-MMC-SD)

2. Download and write U-Boot to the SD card:
   ```bash
   wget https://github.com/gtxaspec/u-boot-ingenic/releases/download/uboot-xb1-2024-12-19/u-boot-isvp_t23n_msc0_mmc1bit.bin
   dd if=u-boot-isvp_t23n_msc0_mmc1bit.bin of=/dev/sdX bs=512 seek=34
   ```

3. Download the firmware and place it on the SD card:
   ```bash
   wget https://github.com/themactep/thingino-firmware/releases/download/firmware-2024-12-20/thingino-galayou_g7_t23n_atbm6012bx.bin
   ```
   - Rename the downloaded file to `autoupdate-full.bin`
   - Copy it to the root of the SD card

## Flashing Process

1. Open the camera housing

2. Locate the flash memory chip on the PCB

3. Follow these steps in order:
   - Power off the camera
   - Insert the prepared SD card
   - Locate pins 5-6 on the flash memory chip
   - Short pins 5-6 (using a wire/jumper)
   - Power on the camera
   - Quickly release the short after powering on

> 💡 **TIP**: Connecting a USB-TTL adapter to monitor the flashing progress via UART is recommended but not required.

## Success Verification
- The camera should automatically begin the flashing process
- If using UART, you can monitor the progress
- Wait for the process to complete before powering off

## Troubleshooting
- If flashing doesn't start, verify:
  - SD card is properly formatted
  - Files are named correctly
  - Short timing was correct (try again if needed)
  - UART connection for monitoring progress