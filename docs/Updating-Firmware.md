## Updating Thingino Firmware

When it comes to installing a newer version of the firmware, there are several ways to do it. Some methods are easier than others, and some are more appropriate for different situations.

### Update vs. Upgrade

First, it’s important to understand the two approaches to updating the camera firmware:

1. **Partial Update (update):** This method updates only the kernel, userland applications, and the overlay partition, leaving the bootloader and its environment settings intact.

2. **Full Update (upgrade):** This method includes the bootloader and environment, leaving the camera in a pristine state, similar to after a hard factory reset.

### From the Development Environment

During development, you may need to update or upgrade your firmware frequently. To make this process easier, two commands have been added to the Thingino makefile: `make update_ota` and `make upgrade_ota`. Both commands require the IP address of the camera as the value of the `IP=` argument. Note that the camera should be online to use this method.

The usual routine to build and install the new firmware would be as follows:

```sh
make update_ota IP=192.168.1.10
```

or

```sh
make upgrade_ota IP=192.168.1.10
```

### From the Camera Itself

When the camera is installed at its final location, the firmware can be upgraded to a newer version directly from within the camera’s Linux system. Log in via `ssh` and use the `sysupgrade` script to install a newer version of the firmware.

#### `sysupgrade`

To use the `sysupgrade` command, you can run it with one of the following options:

```sh
sysupgrade <filename> | [-f | -p] | <URL>
```

#### Options

- **`-f`**: Perform a full upgrade. This option upgrades the entire system, including the bootloader. It is the most thorough update method but will reset the U-Boot environment, which includes settings like your Wi-Fi SSID, password, and root password.

- **`-p`**: Perform a partial upgrade. This is the recommended option for most users as it upgrades the system while preserving the U-Boot environment. Your Wi-Fi SSID, password, and root password will remain intact.

- **`<filename>`**: Perform a full or partial upgrade using a local file. This option is useful if you have already downloaded the firmware binary and want to upgrade without fetching it from a remote source.

- **`<URL>`**: Perform a full or partial upgrade using a URL. This option allows you to specify a direct URL to the firmware binary for the upgrade.

- **`-h`**: Display help information for the `sysupgrade` command.

#### Recommendations

- **Partial Upgrade (`-p`)**: This option is recommended for most users as it preserves critical settings such as the U-Boot environment. Use this option to upgrade your system while keeping your Wi-Fi credentials and root password unchanged.

- **Full Upgrade (`-f`)**: Use this option only when you need to perform a complete system overhaul, including the bootloader. Be aware that this will reset your U-Boot environment, so you may need to reconfigure your Wi-Fi and other settings afterward.

> [!IMPORTANT]
> After a full upgrade is complete, the system may take up to 60 seconds to complete provisioning and be ready for use.  Be patient.

#### How It Works

The `sysupgrade` script automatically downloads the latest precompiled build for your specific device from the Thingino GitHub repository. Whether you choose a full or partial upgrade, the script ensures that you are running the latest available firmware for your device.

#### Example Commands

1. **Partial Upgrade (recommended):**
   ```sh
   sysupgrade -p
   ```
   This command will fetch the latest partial upgrade from the GitHub repository and apply it, preserving your U-Boot environment.

2. **Full Upgrade:**
   ```sh
   sysupgrade -f
   ```
   This command will perform a complete system upgrade, including the bootloader. Use this only when necessary, as it will reset your U-Boot environment.

3. **Upgrade from a Local File:**
   ```sh
   sysupgrade /path/to/firmware.bin
   ```
   Replace `/path/to/firmware.bin` with the actual path to your firmware file. This command will perform the upgrade using the specified file.

4. **Upgrade from a URL:**
   ```sh
   sysupgrade https://example.com/firmware.bin
   ```
   Replace `https://example.com/firmware.bin` with the actual URL of the firmware binary. This command will download the firmware from the URL and perform the upgrade.

- Updating your Thingino device is straightforward with the `sysupgrade` command. Most users will find the `-p` option sufficient for keeping their device up to date while preserving their settings. Reserve the `-f` option for situations where a complete system update, including the bootloader, is required.


### Switching between camera models

If you happen to flash the wrong version of thingino, you can switch to another image from within the system. Change `IMAGE_ID` in `/etc/-os-release` to the one you want to install and run `sysupgrade -p`.


### Troubleshooting

Cameras like Xiaomi MJSXJ03HL with low-end SoC, large sensor resolution, and large flash memory (16MB) can have issues trying to install an update:

```
   \\   _______ _     _ _____ __   _  ______ _____ __   _  _____
   )\\     |    |_____|   |   | \  | |  ____   |   | \  | |     |
  (  /     |    |     | __|__ |  \_| |_____| __|__ |  \_| |_____|
  / /
        xiaomi_mjsxj03hl_t31n_jxq03p
        master+8b67c2e, 2024-10-02 00:02:24 -0400

root@ing-xiaomi-mjsxj03hl-8a0a ~# sysupgrade -p
Partial upgrade from GitHub
Upgrading from GitHub
Not enough free space to download firmware: 16449536 > 13631488
```

To upgrade such a camera from Linux, you first need to change the memory mapping to give the system more space:

```
fw_setenv osmem 52M@0x0; fw_setenv rmem 12M@0x3400000; reboot
```

Then do the upgrade and reset the memory mapping back:

```
fw_setenv osmem 32M@0x0; fw_setenv rmem 32M@0x2000000; reboot
```
