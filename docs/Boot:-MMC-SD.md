### Booting from SD/MMC

Most Ingenic-based devices will attempt to boot from alternative sources if the SoC chip fails to load the bootloader from the onboard flash memory (NOR or NAND). 

This means that if your device's bootloader is damaged, you may be able to recover it using an SD card. Ingenic SoC devices are designed to search for a bootloader at a specific offset on the SD card. If a valid bootloader is found, it will load it automatically.

> [!IMPORTANT]  
> On certain devices, including Wyze and Atom models, the SD card is powered via a GPIO switch. This requires activating a specific GPIO in U-Boot or the Linux system to supply power to the SD card. Without this step, you cannot use the SD card for recovery unless you make physical modifications to the hardware. If your device is configured this way, consider using an alternative recovery method.

#### Preparing the SD Card

To boot your device from an SD card, you'll need a U-Boot binary specifically built for your SoC using the `msc` profile. Prebuilt U-Boot binaries for Ingenic devices are available at [u-boot-ingenic GitHub repository](https://github.com/gtxaspec/u-boot-ingenic).

#### Writing U-Boot to the SD Card

1. Insert the SD card into your PC.
2. Run `fdisk -l` to identify the SD card. For example, you might see something like this:
   ```
   Disk /dev/sdb: 29.72 GiB, 31914983424 bytes, 62333952 sectors
   ```
3. **Ensure you have selected the correct device** (`/dev/sdX`) to avoid data loss on other drives.

4. Use the following command to write the U-Boot binary to the SD card:
   ```bash
   sudo dd if=./u-boot-isvp_t31_msc0_ddr128M.bin of=/dev/sdb bs=512 seek=34
   ```
   This command writes the bootloader to the SD card at an offset of 34 KB from the start (0x0).

> [!CAUTION]  
> Double-check that `/dev/sdX` corresponds to your SD card to avoid overwriting data on other devices.

#### Booting the Device

1. Insert the prepared SD card into your device.
2. Power on the device.
3. The device should attempt to boot from the SD card. If successful, it will load the bootloader from the card.

This method provides a recovery path for devices with damaged onboard bootloaders. If it does not work, verify the GPIO power requirements or try alternative recovery methods.